# Minecraft Skills

本仓库专门收录 Minecraft 模组相关的中文 AI 技能，共 7 个，覆盖开发、物品贴图、发布、崩溃诊断、玩法数值、汉化和怪物设计。详细参考资料按需读取。这里提供的是工作流说明，不是可直接安装进游戏的模组，也不包含游戏文件或贴图资产。

## 包含的技能

| 技能 | 用途 |
| --- | --- |
| [minecraft-mod-dev](minecraft-mod-dev/SKILL.md) | 开发、修复、移植 Java 模组与基岩版 Add-On |
| [minecraft-item-art](minecraft-item-art/SKILL.md) | 生成、修改原创物品像素贴图，并按需接入资源 |
| [minecraft-release](minecraft-release/SKILL.md) | 整理模组发布包、安装说明和更新日志 |
| [minecraft-crash-diagnosis](minecraft-crash-diagnosis/SKILL.md) | 分析崩溃日志，给出有证据的排查方案 |
| [minecraft-gameplay-balance](minecraft-gameplay-balance/SKILL.md) | 设计玩法规则、成长曲线和数值验证场景 |
| [minecraft-localization](minecraft-localization/SKILL.md) | 汉化与润色语言文件，检查键及占位符 |
| [minecraft-mob-design](minecraft-mob-design/SKILL.md) | 构思怪物与 Boss 的外观、生态、行为、招式及反制方法 |

开发技能默认采用轻量修改流程：只读相关文件、复用已验证环境、按改动风险选择测试。详细参考资料按需加载，不保证固定的额度节省比例。

## 使用

下载或克隆本仓库，将需要的完整技能文件夹交给支持 `SKILL.md` 的助手，按该助手的技能安装方式安装；保留 `agents/` 及技能中已有的 `references/` 等子目录。仓库根目录不是单个技能。

使用示例：

```text
使用 $minecraft-mod-dev，修改当前 Fabric 项目的血条位置，保持现有游戏版本，只做相关验证。
```

```text
使用 $minecraft-item-art，为我的模组制作一把原创雷电剑，目标为 32×32 透明 PNG。
```

### 更多使用示例

- 模组发布：`使用 $minecraft-release，把当前模组整理成本地发布包，附安装说明与更新日志，先不上传。`
- 崩溃诊断：`使用 $minecraft-crash-diagnosis，分析这份 latest.log，说明原因和最小排查步骤。`
- 玩法数值：`使用 $minecraft-gameplay-balance，设计一把击杀成长的剑，给出公式、阶段数值和防刷取舍。`
- 汉化文案：`使用 $minecraft-localization，把模组语言文件翻译成中文，检查漏翻和占位符。`

- 怪物设计：`使用 $minecraft-mob-design，设计一只原创洞穴怪物，给出外观、行为、招式、弱点和掉落，先不写代码。`

只安装自己需要的技能即可，不要求一次安装全部 7 个。

也可将具体技能文件及相关资料作为助手的任务说明；自动发现和 `$技能名` 调用是否可用，取决于宿主应用。

## 环境与限制

- 开发需要适配目标游戏版本的 JDK、构建工具及加载器依赖；本仓库不捆绑这些工具。
- 贴图生成需要宿主提供图像生成/编辑工具；技能不会增加账号额度、工具权限或免费生图能力。图像工具不可用时，无法仅凭本仓库生成图片。
- 各版本与加载器需分别适配、验证，不承诺支持所有版本或一个 JAR 通用。
- 生成器输出不保证直接符合目标像素尺寸，需要检查真实尺寸、透明度和可读性。
- 构建通过不等于游戏内验收；未执行的检查应明确说明。
- 不自动接受 Minecraft EULA，不操作正式存档或发布产物；需要用户明确授权。
- 技能经过格式与界面配置检查，不代表所有实际使用场景均已测试。

## 仓库范围

只收录直接服务于 Minecraft 模组开发与维护的技能、参考文档和界面元数据；不收录通用视频剪辑、文件整理或学习笔记技能。不提交账号凭据、个人路径、聊天记录、游戏 JAR、开发缓存、测试世界或第三方贴图。提交前仍需检查暂存区；`.gitignore` 不能替代隐私检查。

## 许可证

本仓库原创内容使用 [MIT License](LICENSE)。外链资料与第三方工具不包含在本仓库授权范围内。

本项目与 Mojang、Microsoft 无隶属或官方认可关系。
