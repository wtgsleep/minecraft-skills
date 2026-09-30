# 基岩版 Add-On

官方入口：https://learn.microsoft.com/en-us/minecraft/creator/ 。官方脚本示例：https://github.com/microsoft/minecraft-scripting-samples 。按目标版本选择 stable 或 preview/beta 文档与样例。

先明确基岩版精确版本、平台、行为包/资源包/脚本需求、是否允许实验性开关。基岩版使用 Add-On 和 Script API 工具链，不能输出 Java 加载器 JAR。

根据需求创建行为包和资源包，使用有效且彼此独立的 pack/module UUID；更新现有包时保留身份 UUID。按目标版本核验 manifest schema、版本数组、`min_engine_version`、模块类型、入口及依赖。不要把 manifest 的引擎下限当作所有后续版本的兼容证明。

JSON 中每类内容的 `format_version` 分别核对。资源标识符、命名空间、纹理映射和实体引用保持一致。脚本使用目标游戏支持的 `@minecraft/server` 等模块版本；npm 类型包版本和游戏中可用的 API 必须对应，不盲装 latest。

若使用 TypeScript，构建为游戏支持的 JavaScript，保证 manifest 入口指向打包后的真实文件。不要在游戏脚本中依赖 Node.js 专属内置模块。预览 API 或实验功能必须在交付说明中明确要求。

验证 manifest 与内容 JSON、UUID 和依赖关系，运行项目脚本构建及类型检查，检查打包根目录正确、包含所有引用资源，再按需求输出 `.mcpack` 或 `.mcaddon`。在目标游戏的隔离测试世界中导入并查看 Content Log，验证行为、资源和脚本功能。没有游戏运行条件时，明确仅完成静态/构建验证，并提供导入与复现步骤。

迁移时根据官方变更记录检查 API 移除、事件时机、只读阶段/执行权限及组件格式变化，不能只提高 `min_engine_version`。不要覆盖用户正式世界或声称基岩版包兼容 Java 版。
