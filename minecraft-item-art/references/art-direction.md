# 物品美术与提示词

## 设计决策

先确定能在小尺寸下识别的轮廓，再用少量大色块表达材质与主题。剑需要分清剑刃、护手和握柄；同系列物品沿用边缘明暗、像素密度和材质色阶。雷电、火焰、冰霜等主题应影响可读的轮廓或色块，不依赖微小符文和大量散点。

按照项目参考确定角度；没有参考时，剑可采用柄在左下、尖在右上的平面侧视构图，留少量透明边距防止裁切。不要使用摄影透视、投影或厚重外部辉光代替轮廓。方向是可调整的设计默认，不是游戏强制规则。

原版协调风格优先硬边像素簇、有限且有层次的颜色和清楚的明暗。不要强制所有项目都采用同一色数、黑描边或二值 alpha；按用户风格与目标渲染方式判断。用户要求高清绘画风时尊重其选择。

## 闪电剑示例

以下是可适配的示例，不是每把剑都必须使用的颜色与造型。生成前按用户描述替换设计细节和目标尺寸。

```text
Use case: stylized-concept
Asset type: Minecraft mod inventory and handheld item texture, one isolated 2D sprite
Primary request: An original lightning sword with a clearly readable sword silhouette and a lightning-shaped motif incorporated into the blade.
Scene/backdrop: True transparent background with alpha, no painted checkerboard.
Style/medium: Crisp Minecraft-compatible pixel art, hard square pixel clusters, restrained shading; designed to remain readable at a 16 by 16 pixel target size.
Composition/framing: Flat side view, handle toward bottom-left and tip toward top-right; the entire blade, guard and grip visible with a small transparent margin.
Color palette: Steel-blue blade, pale electric highlights, dark grip; maintain strong contrast between adjacent parts.
Constraints: Exactly one sword; no labels, watermark, character, scenery, pedestal, border or alternate views. No antialiasing, photographic perspective, soft bloom or drop shadow. Lightning detail stays close to the blade and does not obscure the silhouette.
```

“目标像素尺寸”是设计与验收要求，不是生成器保证。取得文件后必须检查实际分辨率、透明像素与缩小可读性。工具只能输出大图时，不把提示词中的数字作为通过验收的证据。

## 修改示例

已有闪电剑改为紫色：把原图作为编辑目标；明确“只将雷电高光改为紫色，保持轮廓、柄、护手、角度、画布和透明背景不变”。检查返回结果是否真的保持这些约束。不要为了改色额外设计不同的剑。

同系列武器：用已选中的物品图作为风格参考，说明保留色阶、描边方式和像素密度，但改变为用户指定的工具轮廓。多资产逐个交付独立图片，避免把整张展示拼图当成每件物品的贴图。

## 动画

先定义帧数、帧大小、循环时序和允许变化的部位。锁定剑的画布、位置与主体轮廓，仅让电弧/高光按需求变化。检查帧间抖动、意外形变以及循环首尾衔接。

动画帧是生产资源，每帧应有相同规格；展示 GIF 不能代替游戏需要的帧序列与元数据。图像工具不保证多帧对齐，必须实际检查。拼接和转换仍遵循当前工具的图像编辑权限，不能因写在技能中就推定获准任意脚本编辑。

只有用户要求动画时才准备它。贴图动画、自发光材质、动态照明和实际粒子/闪电实体分别需要不同支持；用静态亮色像素不代表实现了其他效果。
