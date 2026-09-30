# Java 版开发与排错

## 官方资料入口

这些链接是入口，不是固定版本的 API 契约。打开后切换至目标版本；旧版缺文档时查官方仓库相应标签与实际依赖源码。

| 加载器 | 官方入口 | 需要确认的差异 |
| --- | --- | --- |
| Fabric | https://docs.fabricmc.net/ 、https://fabricmc.net/develop/ 、https://github.com/FabricMC/fabric-example-mod | Loader、Fabric API、Loom、映射选择及对应模板版本 |
| Forge | https://docs.minecraftforge.net/ 、https://files.minecraftforge.net/ 、https://github.com/MinecraftForge/MinecraftForge | 目标版本 MDK、ForgeGradle、注册和事件生命周期 |
| NeoForge | https://docs.neoforged.net/ 、https://neoforged.net/ 、https://github.com/NeoForgeMDKs | 目标模板、Gradle 插件、命名空间和 API；不要视作 Forge 的同名替换 |
| Quilt | https://quiltmc.org/ 、https://github.com/QuiltMC | 目标版本 Loader、API 与模板可用性；不能默认 Fabric 兼容性覆盖所有 Mod |

查找第三方库时优先查该库官方仓库和目标版本发布记录。只引入需求实际用到的依赖；跨加载器框架也是选择项，不是默认前提。

## 探测与创建

读取 `settings.gradle[.kts]`、`build.gradle[.kts]`、`gradle.properties`、`gradle/wrapper/gradle-wrapper.properties` 和项目实际元数据。可能遇到 `fabric.mod.json`、`quilt.mod.json`、`META-INF/mods.toml`、`META-INF/neoforge.mods.toml` 或旧版 `mcmod.info`；结合构建插件判断，不只凭文件名定版本。

检查 `java -version` 和 Wrapper 的 `--version`，区别终端 JVM、Gradle daemon JVM、编译 toolchain 和字节码目标。旧版 Wrapper 不一定能在新 JDK 上运行；现代模板要求的 JDK 也不适用于全部旧版本。不要为了一个项目修改系统全局 Java 配置。

使用空目标目录接收官方模板，不覆盖用户项目。保留完整 Wrapper；缺失的 Wrapper JAR 从可信模板或受支持的生成流程恢复，不能写一个空文件替代。记录模板分支、标签或提交。对模组 ID、包名和元数据中的版本约束按加载器规则检查一致性。

## 功能实现关注点

- 注册：查目标版本的注册 API、注册时机、事件总线和资源键要求。不要混用不同年代的注册示例。
- 物品与方块：实现注册、模型、贴图引用、语言条目；按功能补配方、掉落表、标签、创造模式入口。目录名、模型格式与 JSON schema 以目标版本为准。
- 实体与方块实体：分别处理类型、属性、持久化、同步、菜单及客户端渲染注册。客户端类只在正确的入口和 source set 中加载。
- 网络：服务端决定游戏状态，验证客户端请求的身份、距离、权限和数据范围；按目标 API 安排线程处理。仅在客户端变更状态不等于联机功能完成。
- 数据：核实目标版本使用的 NBT、组件、Codec、附件或能力系统，区分持久化与同步。保留已有注册 ID 和数据语义。
- 世界生成：核对动态注册表、数据驱动格式和维度配置；明确新内容作用于新生成区块还是涉及旧区块迁移。
- Mixin/访问扩展：优先使用可用公共 API；确需注入时核对映射、目标描述符、加载端和混入配置，在打包环境验证。避免用宽泛注入掩盖版本差异。
- 资源生成：使用目标版本数据生成器时确认输出被纳入资源集，避免手写资源与生成资源冲突。

## 验证

从项目根目录优先使用 Wrapper。Windows 使用 `.\gradlew.bat`，其他系统使用 `./gradlew`。复用项目已验证的命令；仅在任务未知时查询可用任务，不每次运行 `tasks --all`。按改动风险选择构建、测试、数据生成或运行任务，留意 `build` 是否自动串联游戏测试；不能假定所有加载器都有同名任务。

检查实际发布任务的输出，而非仅按文件名长短猜测。按该版本工具链核验需要的 remap/reobf 或其他打包步骤；新工具链可能不需要旧流程。查看 JAR 中的入口、元数据、资源与依赖声明，不把 sources、dev 或未处理的中间包当成发行包。

验证与功能有关的场景：物品获取和使用、资源加载、配方和掉落、保存重进、联机同步；双端/服务端功能验证专用服务器。纯客户端 Mod 核实它不要求服务器安装，以及服务端环境不会误加载客户端类。无需 GUI 的环境不能声称完成可视化验收。

测试服务器使用隔离目录和测试世界。若需要 EULA 接受，让用户处理；不要自动改写。涉及开发登录或网络配置时限定在隔离测试环境，不修改用户正式服务器。

## 故障定位

从失败任务和首个有因果关系的异常定位，结合完整 `Caused by` 链、加载器日志、`latest.log` 和 crash report 判断：

| 现象 | 优先检查 |
| --- | --- |
| Wrapper/Gradle 启动失败 | JVM 与 Wrapper/插件兼容性、文件完整性 |
| 依赖无法解析 | 坐标、仓库、目标版本是否发布、网络/代理/TLS；区分不存在与访问失败 |
| 找不到符号或方法 | 源码使用的 API 年代、映射体系、依赖版本 |
| 注册或加载崩溃 | 生命周期、重复 ID、元数据、必需依赖、加载端 |
| 专用服出现客户端类错误 | common 代码的字段、静态初始化及方法签名是否引用客户端类 |
| 贴图/配方/模型失效 | 大小写、命名空间、资源路径、版本 schema、生成资源是否入包 |
| Mixin 应用失败 | 目标签名、映射/转换流程、冲突和目标运行端 |

每次修复针对证据修改并重跑失败检查。不要以清空全部缓存、升级全部依赖或扩大兼容范围作为默认修复。
