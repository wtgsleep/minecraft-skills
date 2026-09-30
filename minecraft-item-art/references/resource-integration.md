# 贴图接入与版本核验

只有用户要求把资产用于项目时才修改项目资源。先读取项目版本、Mod ID、物品 ID、现有模型和资源生成规则，检查手写文件是否会被数据生成器覆盖。游戏版本未知且没有仓库时先交付独立 PNG；不要为了交付图片虚构资源结构。

## Java 版

官方参考入口：

- [Fabric：首个物品](https://docs.fabricmc.net/develop/items/first-item)
- [Fabric：物品模型](https://docs.fabricmc.net/develop/items/item-models)
- [Forge 文档](https://docs.minecraftforge.net/)
- [NeoForge 文档](https://docs.neoforged.net/)

这些文档的默认页面会更新，必须切换至目标游戏版本。不能把现代目录结构用于所有历史版本。

常见现代 Java 版纹理路径是 `src/main/resources/assets/<modid>/textures/item/<item_id>.png`；模型常位于 `assets/<modid>/models/item/<item_id>.json`。核实当前版本后，在模型中使用形如 `<modid>:item/<item_id>` 的纹理标识，不写绝对路径或 `.png` 扩展名。

普通平面物品常用 `minecraft:item/generated`；剑和工具常用 `minecraft:item/handheld` 以获得合适持握变换。优先沿用项目现有父模型。某些新版还需要 `assets/<modid>/items/<item_id>.json` 客户端物品定义，将物品关联到模型；查目标版本，不给每个老版本都创建此文件。特殊三维造型需要几何和 UV，不能只换父模型就宣称已完成。

动画按目标版本核对纹理帧排列和同名 `.png.mcmeta` 中的动画字段，检查帧索引、宽高与时间有效。贴图插值会影响像素风效果，按需求设置。额外自发光层、材质或渲染器支持需要分别核实，不能随意添加文件后就保证有效。

修改尽量采用项目既有的数据生成或手写方式，并检查文件名大小写、命名空间和引用一致。PNG、模型及新式物品定义（适用时）是外观链路；要获得一个全新物品，还需要对应的物品注册，贴图文件本身不会自动注册物品。

## 基岩版

参考 [Microsoft：添加自定义物品](https://learn.microsoft.com/en-us/minecraft/creator/documents/addcustomitems?view=minecraft-bedrock-stable)。选择匹配目标游戏的 stable/preview 文档。

常见物品图像位于资源包的 `textures/items/`，通过 `textures/item_texture.json` 中的映射和物品图标组件引用。核对目标版本字段与既有资源包，不能把 Java 版模型 JSON 放入基岩版并期待工作。三维手持外观可能涉及 attachable、geometry、材质及独立 UV 纹理；库存图标和这些纹理不是同一用途。

## 验证与交付

检查 PNG 可解码、尺寸与透明性、JSON 语法、资源引用和打包内容。资源生成任务执行后再次确认图像和引用仍被纳入输出。按用户任务需要运行构建；构建成功只表示该阶段通过，未必能发现缺失贴图。

有游戏环境时检查物品栏、手持与掉落状态，必要时观察动画循环，查看资源加载日志是否有缺失模型或纹理。游戏无法运行时报告“资源已接入，游戏显示未验证”，给出具体加载步骤，不能声称已经在游戏内正确显示。

最终链接资产与修改文件，说明对应物品 ID、实际图片规格和验证状态。图片本身可以复用，但资源目录、模型格式、动画元数据和发光实现的跨版本兼容性需各自验证。
