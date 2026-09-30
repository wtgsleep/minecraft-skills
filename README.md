# Minecraft Skills

9 个中文 AI 技能，覆盖 Minecraft 模组开发及配套发布、诊断、策划和汉化，并提供视频剪辑方案、文件整理与学习笔记工具。详细参考资料按需读取。这里提供的是工作流说明，不是可直接安装进游戏的模组，也不包含游戏文件或贴图资产。

## 包含的技能

| 技能 | 用途 |
| --- | --- |
| [minecraft-mod-dev](minecraft-mod-dev/SKILL.md) | 开发、修复、移植 Java 模组与基岩版 Add-On |
| [minecraft-item-art](minecraft-item-art/SKILL.md) | 生成、修改原创物品像素贴图，并按需接入资源 |

| [minecraft-release](minecraft-release/SKILL.md) | 整理模组发布包、安装说明和更新日志 |
| [minecraft-crash-diagnosis](minecraft-crash-diagnosis/SKILL.md) | 分析崩溃日志，给出有证据的排查方案 |
| [minecraft-gameplay-balance](minecraft-gameplay-balance/SKILL.md) | 设计玩法规则、成长曲线和数值验证场景 |
| [minecraft-localization](minecraft-localization/SKILL.md) | 汉化与润色语言文件，检查键及占位符 |
| [video-edit-planner](video-edit-planner/SKILL.md) | 规划视频片段、时间轴、旁白和字幕 |
| [safe-file-organizer](safe-file-organizer/SKILL.md) | 预览分类、重命名与查重计划，按授权执行 |
| [study-notes-review](study-notes-review/SKILL.md) | 整理学习笔记、错因和复习题 |

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

也可将具体技能文件及相关资料作为助手的任务说明；自动发现和 `$技能名` 调用是否可用，取决于宿主应用。

## 环境与限制

- 开发需要适配目标游戏版本的 JDK、构建工具及加载器依赖；本仓库不捆绑这些工具。
- 贴图生成需要宿主提供图像生成/编辑工具；技能不会增加账号额度、工具权限或免费生图能力。图像工具不可用时，无法仅凭本仓库生成图片。
- 各版本与加载器需分别适配、验证，不承诺支持所有版本或一个 JAR 通用。
- 生成器输出不保证直接符合目标像素尺寸，需要检查真实尺寸、透明度和可读性。
- 构建通过不等于游戏内验收；未执行的检查应明确说明。
- 不自动接受 Minecraft EULA，不操作正式存档或发布产物；需要用户明确授权。

- 视频技能默认交付剪辑方案，不等于成片；实际导出需要可用的编辑工具和用户授权。
- 文件整理先预览，不默认删除或覆盖；模组发布不会自动上传。
- 技能经过格式与界面配置检查，不代表所有实际使用场景均已测试。

## 仓库范围

只收录技能、参考文档和界面元数据。不提交账号凭据、个人路径、聊天记录、游戏 JAR、开发缓存、测试世界或第三方贴图。提交前仍需检查暂存区；`.gitignore` 不能替代隐私检查。

## 许可证

本仓库原创内容使用 [MIT License](LICENSE)。外链资料与第三方工具不包含在本仓库授权范围内。

本项目与 Mojang、Microsoft 无隶属或官方认可关系。
