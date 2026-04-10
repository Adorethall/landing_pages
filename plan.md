# Meshy × Roblox 开发者 Landing Page 实现方案

## Context

Meshy 需要一个针对 Roblox 开发者的专属 Landing Page，让该群体搜索相关词后进来第一眼觉得"这个产品是为我做的"。目标是提升转化，不是通用产品介绍。

---

## 一、调研阶段：搜索意图分析

### 用户画像
- **主力群体**：14–25岁，在 Roblox Studio 做游戏的业余/半职业开发者
- **专业群体**：独立工作室、monetize 的 Experience 开发者
- **技能分布**：大多数会写 Lua，但 3D 建模能力弱（会用 Roblox 自带工具，不会 Blender/Maya）

### 核心搜索意图
| 搜索词 | 真实需求 |
|--------|----------|
| how to make 3D models for Roblox | 想跳过 Blender，找更简单路径 |
| Roblox asset creator AI | 想用 AI 自动生成，不想手动建模 |
| free Roblox models | 降低成本、快速填充游戏内容 |
| Roblox low poly model generator | 满足平台性能限制 |

### 核心顾虑（门槛）
1. **格式兼容性**：生成的模型能直接导入 Roblox Studio 吗？（.obj/.fbx 支持？）
2. **性能约束**：Polygon count、texture size 有没有超出 Roblox 限制？
3. **风格匹配**：模型的画风能不能贴合 Roblox 卡通/低多边形美学？
4. **学习成本**：AI 工具是否也要花很长时间学？

---

## 二、Meshy 设计语言分析

### 视觉系统
- **主色调**：深色背景（#0A0A0F 类深黑）+ 紫色/蓝紫渐变高亮（#7C3AED → #4F46E5）
- **字体**：无衬线现代体，标题 bold，副标题 medium，行间距宽松
- **间距**：大量留白，section padding 宽，呼吸感强
- **动效**：渐入动画、hover 发光效果、3D 模型展示旋转

### 结构模式
- Hero：大标题（痛点/结果导向）+ 副标题（机制说明）+ 单一 CTA 按钮
- Features：图标/截图 + 简短标题 + 1–2 句场景描述（不是功能列表）
- Social Proof：数字统计（生成数量）+ 用户案例图
- Footer CTA：复述核心价值 + 同款 CTA 按钮

---

## 三、Landing Page 结构设计

### 核心判断
Roblox 开发者的搜索意图是**"我想快速做出能用的 3D 资产，不想学建模"**，所以页面逻辑应该是：
> 消除顾虑（能用）→ 展示简单（好上手）→ 场景共鸣（为我做的）→ 驱动行动

### 页面 Section 规划

```
[Navbar] Meshy logo + 导航（可选，与主站一致）

[Hero]
  标题：Stop Struggling with Roblox Models — Just Describe It
  副标题：Meshy turns text into Roblox-ready 3D assets in seconds. 
          No Blender. No rigging. Just build.
  CTA：Generate Free →
  背景：3D 模型动态展示（Roblox 风格低多边形资产）

[Trust Bar]
  数字背书：X models generated · Used by X+ Roblox developers · Roblox Studio compatible

[Features × 3]
  1. "Describe your asset, get it in Studio"
     场景：输入"medieval stone castle wall"，30秒导出 .obj，拖进 Roblox Studio
  2. "Roblox-optimized by default"  
     场景：自动控制 poly count、贴图尺寸，不用手动优化担心性能
  3. "Build a whole game world, not just one asset"
     场景：批量生成同系列资产，保持风格统一（地图、道具、NPC）

[Gallery / Before-After]
  展示：Roblox 游戏截图中使用 Meshy 生成资产的实际效果
  或：text prompt → 生成结果 → Roblox Studio 导入 的流程图

[Roblox Developer Testimonials]
  来自 Roblox 开发者的引用（真实或基于调研构建的代表性声音）
  例："I used to spend 2 hours per prop in Blender. Now it's 2 minutes."

[FAQ（消除顾虑）]
  - Does it export to Roblox-compatible formats? → Yes, .obj and .fbx
  - Will it exceed Roblox's polygon limits? → Auto-optimized to Roblox specs
  - Does the style match Roblox's aesthetic? → Low-poly mode available

[Final CTA]
  标题：Your next Roblox game starts here.
  CTA：Start for Free →

[Footer]
  与 meshy.ai 一致
```

---

## 四、技术实现方案

### 技术选型
- 单 HTML 文件，内嵌 CSS + JS（无依赖，浏览器直接打开）
- CSS：自定义变量 + Flexbox/Grid，不引入框架
- 动效：CSS animation / Intersection Observer（scroll reveal）
- 图标：SVG inline 或 Lucide CDN
- 字体：Google Fonts CDN（Inter 或 Outfit）

### 关键实现细节
| 组件 | 实现方式 |
|------|----------|
| 渐变背景 | CSS radial-gradient，模拟 Meshy 深色星云效果 |
| 3D 模型展示 | CSS 3D transform 旋转的几何图形（低多边形风格）或 SVG |
| Glow 效果 | box-shadow + text-shadow 紫色发光 |
| Scroll 动画 | Intersection Observer API，class 切换 opacity/transform |
| CTA 按钮 | 渐变背景 + hover scale + glow transition |

### 文件结构
```
meshy-roblox-landing.html   # 唯一交付文件
```

---

## 五、说明文档提纲（300字内）

1. **搜索意图核心判断**：Roblox 开发者不是在找"3D建模工具"，是在找"跳过建模直接出资产"的捷径 → 页面不讲功能，讲结果和时间节省
2. **调研来源**：Reddit r/roblox、r/robloxgamedev、YouTube 教程评论区、Roblox DevForum、Google 自动补全
3. **超出预期的发现**：开发者对"poly count 限制"的焦虑远高于预期，格式兼容性是第一道拦截
4. **取舍**：去掉通用 AI 建模功能介绍，聚焦 Roblox 场景；FAQ 替代评测视频减少实现复杂度
5. **上线还缺什么**：真实 Roblox 项目截图、开发者真实证言、A/B 测试不同标题文案

---

## 六、验证方式

- 浏览器直接打开 HTML，检查各 section 渲染
- 调整窗口宽度，验证响应式布局（移动端 ≥ 375px）
- 检查动效：滚动时 scroll reveal 是否触发
- 对比 meshy.ai 首页，确认视觉风格一致性（配色、字体、间距）
