# 大鱼GEO AI品牌可见度检测系统 - UI/UX设计规范

> 文档版本：v2.0
> 创建日期：2026-05-30
> 更新日期：2026-05-31
> 设计标准：像素级复刻，不精简组件，使用21st-dev-magic强制获取

---

## 零、技术栈统一规范

### 0.1 统一技术栈（强制执行）

| 层级 | 技术选型 | 理由 |
|------|----------|------|
| **UI组件库** | shadcn/ui | 组件100%可控，易于定制 |
| **CSS框架** | Tailwind CSS | 原子化CSS，灵活定制 |
| **图表库** | Recharts + 自定义DonutChart | 专业的React图表库 |
| **动画库** | Framer Motion | 流畅的动画效果 |
| **图标库** | Lucide React | 统一图标风格 |
| **前端框架** | React 18 + TypeScript | 现代化前端架构 |
| **后端框架** | Python FastAPI | 异步支持好，AI集成方便 |
| **数据库** | SQLite（开发）/ PostgreSQL（生产） | 轻量/企业级 |
| **报告生成** | WeasyPrint | Python原生，支持CSS |

### 0.2 组件获取流程（强制执行）

```
┌─────────────────────────────────────────────────────────────────┐
│                    组件获取标准流程                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1️⃣ 确定组件需求 → 明确需要什么组件（如：环形图、进度条）         │
│           ↓                                                      │
│  2️⃣ 21st-dev-magic查询 → 使用工具搜索高质量组件代码              │
│           ↓                                                      │
│  3️⃣ 选择最佳组件 → 根据设计风格选择最匹配的组件                  │
│           ↓                                                      │
│  4️⃣ 获取完整代码 → 使用builder工具获取生产级代码                 │
│           ↓                                                      │
│  5️⃣ 集成到项目 → 放入 src/components/ui/ 对应目录               │
│                                                                 │
│  ⚠️ 禁止手动编写组件代码！必须使用21st-dev-magic获取！          │
│  ⚠️ 禁止因为实现困难就简化设计！必须100%像素级复刻！             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 一、设计理念

### 1.1 核心设计原则

| 原则 | 说明 | 实现方式 |
|------|------|----------|
| **专业感** | 让客户觉得大鱼GEO很专业 | 深色标题栏、数据可视化、图表动画 |
| **快速** | 几分钟出结果 | 进度条实时反馈、操作简洁 |
| **可视化** | 数据直观易懂 | 环形图、条形图、状态徽章 |
| **信任感** | 数据可信 | 来源标注、置信度展示 |
| **差异化** | 不同于同行 | 独特的数据故事线、专业排版 |

### 1.2 设计风格

- **风格定位**：专业数据仪表盘风格，参考现代BI工具（如Tableau、PowerBI）+ 商务咨询报告
- **色彩系统**：科技蓝为主色，搭配渐变色点缀
- **组件库**：shadcn/ui + Tailwind CSS
- **图表库**：Recharts + 自定义组件

---

## 二、色彩系统

### 2.1 主色板

```css
:root {
  /* Primary - 科技蓝 */
  --primary: hsl(210, 100%, 50%);
  --primary-foreground: hsl(0, 0%, 100%);
  --primary-hover: hsl(210, 100%, 45%);
  
  /* Secondary */
  --secondary: hsl(210, 40%, 96%);
  --secondary-foreground: hsl(210, 40%, 10%);
  
  /* Accent - 渐变紫 */
  --accent: hsl(262, 83%, 58%);
  --accent-foreground: hsl(0, 0%, 100%);
  
  /* Background */
  --background: hsl(0, 0%, 100%);
  --background-elevated: hsl(210, 40%, 98%);
  
  /* Foreground */
  --foreground: hsl(210, 40%, 10%);
  --muted-foreground: hsl(210, 10%, 45%);
  
  /* Border */
  --border: hsl(210, 20%, 90%);
  --ring: hsl(210, 100%, 50%);
}
```

### 2.2 语义色

```css
/* 成功 - 绿色 */
--success: hsl(142, 76%, 36%);
--success-light: hsl(142, 76%, 95%);

/* 警告 - 橙色 */
--warning: hsl(38, 92%, 50%);
--warning-light: hsl(38, 92%, 95%);

/* 错误 - 红色 */
--destructive: hsl(0, 84%, 60%);
--destructive-light: hsl(0, 84%, 95%);

/* 平台颜色 */
--deepseek: hsl(210, 100%, 50%);      /* DeepSeek */
--doubao: hsl(15, 95%, 55%);           /* 豆包 */
--baidu: hsl(204, 86%, 49%);          /* 百度 */
--qwen: hsl(30, 100%, 50%);           /* 通义千问 */
--kimi: hsl(220, 90%, 56%);           /* Kimi */
--zhipu: hsl(168, 76%, 42%);          /* 智谱 */
--hunyuan: hsl(210, 100%, 50%);       /* 混元 */
```

### 2.3 情绪色

```css
/* 正面情绪 - 绿色 */
--sentiment-positive: hsl(142, 76%, 36%);
--sentiment-positive-bg: hsl(142, 76%, 95%);

/* 中性情绪 - 黄色 */
--sentiment-neutral: hsl(45, 93%, 47%);
--sentiment-neutral-bg: hsl(45, 93%, 95%);

/* 负面情绪 - 红色 */
--sentiment-negative: hsl(0, 84%, 60%);
--sentiment-negative-bg: hsl(0, 84%, 95%);
```

---

## 三、核心业务组件规范

### 3.1 行业选择卡片网格 (IndustryCardGrid)

**组件来源**：21st-dev-magic `grid card selection`

**组件名称**：`Sortable` → 改造为 `IndustryCardGrid`

**设计要求**：
```
┌─────────────────────────────────────────────────────────────────────┐
│  行业选择网格                                                       │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐               │
│  │   🏢    │  │   🛒    │  │   💊    │  │   🚗    │               │
│  │         │  │         │  │         │  │         │               │
│  │  制造业  │  │  零售业  │  │  医疗健康 │  │  汽车   │               │
│  │         │  │         │  │         │  │         │               │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘               │
│                                                                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐               │
│  │   🏗️    │  │   💰    │  │   🎓    │  │   🍽️    │               │
│  │         │  │         │  │         │  │         │               │
│  │  房地产  │  │  金融   │  │  教育   │  │  餐饮   │               │
│  │         │  │         │  │         │  │         │               │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘               │
│                                                                     │
│  📋 更多行业可通过搜索框筛选...                                     │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**样式规范**：
- 布局：2-4列响应式网格（桌面4列，平板2列，手机1列）
- 卡片尺寸：宽度自适应，高度120px
- 选中态：蓝色边框 + 浅蓝色背景 + 选中图标
- 悬停态：微微上浮（transform: translateY(-2px)）+ 阴影加深
- 动画：悬停和选中切换时平滑过渡（200ms ease-out）

**交互规范**：
- 单选模式，选中后自动取消上一个选择
- 点击卡片后有按压反馈（scale: 0.98）
- 移动端支持触摸选择

**组件代码获取命令**：
```bash
# 使用21st_magic_component_inspiration查询
搜索关键词：grid card selection selectable cards
```

---

### 3.2 AI检测进度条 (DetectionProgressSteps)

**组件来源**：21st-dev-magic `step progress wizard steps`

**组件名称**：`Steps` 或 `ProgressIndicator`

**设计要求**：
```
┌─────────────────────────────────────────────────────────────────────┐
│  四步闭环检测进度                                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ①───────────②───────────③───────────④                             │
│  场景覆盖    竞品发现    机会分析    行动排序                       │
│    ✓           ◐           ○           ○                           │
│   完成      进行中      等待中      等待中                           │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │  ⏳ 正在分析[品牌]在[行业]的AI可见度...                     │    │
│  │  [████████████░░░░░░░░░░░░░░░░] 60%                      │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**样式规范**：
- 布局：四步横向排列，步骤之间用连接线
- 圆形指示器：40px直径
- 状态颜色：
  - 待处理：灰色边框 + 灰色数字
  - 进行中：蓝色填充 + 脉冲动画
  - 已完成：绿色填充 + 白色勾选图标
- 连接线：2px粗细，完成部分为蓝色，未完成为灰色
- 当前步骤文字高亮加粗

**动画规范**：
- 步骤切换：圆圈缩放动画（scale 1 → 1.1 → 1）
- 完成时：打勾图标从透明到显示
- 连接线：从左向右填充动画（500ms ease-out）

**组件代码获取命令**：
```bash
# 使用21st_magic_component_inspiration查询
搜索关键词：step progress wizard steps indicator
```

---

### 3.3 品牌可见度环形图 (VisibilityDonutChart)

**组件来源**：21st-dev-magic `pie chart donut chart analytics percentage`

**组件名称**：`DonutChart` + 自定义动画

**设计要求**：
```
┌─────────────────────────────────────────────────────────────────────┐
│  品牌可见度                                                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│                        ┌───────────┐                               │
│                        │           │                               │
│                    ╭───────────╮   │                               │
│                   ╱    78%     ╲  │                               │
│                  │               │ │                               │
│                  │   品牌名称    │ │                               │
│                   ╲             ╱  │                               │
│                    ╰───────────╯   │                               │
│                        │           │                               │
│                        └───────────┘                               │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ 🟦 DeepSeek   32%   ████████████████░░░░░░░░░░  15次     │   │
│  │ 🟧 豆包       25%   ██████████████░░░░░░░░░░░░░  12次     │   │
│  │ 🟩 通义千问   22%   █████████████░░░░░░░░░░░░░░  11次     │   │
│  │ 🟪 Kimi       21%   ████████████░░░░░░░░░░░░░░░  10次     │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**样式规范**：
- 外环直径：280px（桌面）/ 200px（移动端）
- 环宽度：30px
- 中心区域：显示百分比数字 + 品牌名称
- 分段颜色：使用平台对应颜色
- 图例：水平排列，每个图例项带颜色块 + 平台名 + 百分比 + 次数

**动画规范**：
- 首次加载：从0%增长到目标值的动画（1200ms ease-out）
- 分段延迟：每个分段延迟50ms依次出现
- 悬停交互：悬停某段时高亮该段 + 显示详细数值

**组件代码获取命令**：
```bash
# 使用21st_magic_component_inspiration查询
搜索关键词：pie chart donut chart analytics percentage
```

---

### 3.4 竞品对比条形图 (CompetitorRankingChart)

**组件来源**：21st-dev-magic `horizontal bar chart comparison ranking`

**组件名称**：`HorizontalBarReportCard` + Recharts BarChart

**设计要求**：
```
┌─────────────────────────────────────────────────────────────────────┐
│  竞争格局                                                           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  客户品牌 [███████████████░░░░░░░░░░░░] 52%  第1名  ⭐            │
│                                                                     │
│  竞品A    [████████████░░░░░░░░░░░░░░░░] 38%  第2名               │
│                                                                     │
│  竞品B    [████████░░░░░░░░░░░░░░░░░░░░] 25%  第3名               │
│                                                                     │
│  竞品C    [█████░░░░░░░░░░░░░░░░░░░░░░░] 15%  第4名               │
│                                                                     │
│  竞品D    [███░░░░░░░░░░░░░░░░░░░░░░░░░] 8%   第5名               │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**样式规范**：
- 条形高度：36px
- 条形圆角：8px
- 客户品牌条形：渐变色（蓝色到紫色）
- 竞品条形：灰色渐变（从深到浅表示排名）
- 数值标签：条形右侧显示百分比
- 排名标签：最右侧显示名次
- 客户品牌：特殊标记（星标/边框高亮）

**动画规范**：
- 条形从短到长逐个增长（每个延迟100ms）
- 数字从0增长到目标值
- 加载完成时有轻微弹跳效果

**组件代码获取命令**：
```bash
# 使用21st_magic_component_inspiration查询
搜索关键词：horizontal bar chart comparison ranking
```

---

### 3.5 报告封面 (ReportCover)

**组件来源**：21st-dev-magic `report cover page professional business`

**组件名称**：`HeroSection04` → 改造为报告封面

**设计要求**：
```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│                                                                     │
│                                                                     │
│                     AI 品牌机会发现报告                              │
│                                                                     │
│              ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                    │
│                                                                     │
│                      [ 品牌名称 ]                                   │
│                                                                     │
│                       [ 所属行业 ]                                  │
│                                                                     │
│                                                                     │
│              ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                    │
│                                                                     │
│                                                                     │
│                                                                     │
│                                        大鱼GEO                      │
│                                        AI品牌机会发现引擎             │
│                                    报告日期：2026.05.31             │
│                                                                     │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              水印（30%透明度）      │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**样式规范**：
- 主标题：居中，大字号（48px），科技蓝渐变色
- 副标题：居中，中等字号（24px），灰色
- 品牌名称：突出显示（32px），加粗
- 分隔线：渐变色细线
- 底部信息：右对齐，日期格式为 YYYY.MM.DD
- 水印：右下角，包含Logo + "AI品牌机会发现引擎"文字，30%透明度

**动画规范**：
- 标题文字逐行淡入（stagger 200ms）
- 底部信息从下方滑入
- 水印轻微浮动动画

**组件代码获取命令**：
```bash
# 使用21st_magic_component_inspiration查询
搜索关键词：report cover page professional business
```

---

## 四、基础UI组件规范

### 4.1 按钮组件 (Button)

**组件来源**：shadcn/ui Button

```tsx
// 变体
<Button variant="default">默认按钮</Button>
<Button variant="primary" className="bg-gradient-to-r from-blue-600 to-purple-600">主要CTA</Button>
<Button variant="secondary">次要按钮</Button>
<Button variant="outline">边框按钮</Button>
<Button variant="ghost">文字按钮</Button>
<Button variant="destructive">危险操作</Button>

// 尺寸
<Button size="sm">小按钮</Button>
<Button size="default">默认</Button>
<Button size="lg">大按钮</Button>
<Button size="icon">图标</Button>
```

### 4.2 卡片组件 (Card)

**组件来源**：shadcn/ui Card

```tsx
<Card>
  <CardHeader>
    <CardTitle>卡片标题</CardTitle>
    <CardDescription>卡片描述</CardDescription>
  </CardHeader>
  <CardContent>
    {/* 内容 */}
  </CardContent>
  <CardFooter>
    {/* 底部操作 */}
  </CardFooter>
</Card>
```

### 4.3 输入框组件 (Input)

**组件来源**：shadcn/ui Input

```tsx
<Input placeholder="请输入品牌名称" />
<Input className="border-2 border-primary" /> {/* 聚焦态 */}
```

### 4.4 徽章组件 (Badge)

**组件来源**：shadcn/ui Badge

```tsx
<Badge variant="default">默认</Badge>
<Badge variant="secondary">次要</Badge>
<Badge variant="outline">边框</Badge>
<Badge variant="destructive">危险</Badge>
```

---

## 五、动画与交互规范

### 5.1 过渡动画

| 场景 | 动画 | 时长 | 缓动函数 |
|------|------|------|----------|
| 页面切换 | 淡入淡出 | 200ms | ease-out |
| 卡片出现 | 向上滑入 + 淡入 | 300ms | ease-out |
| 按钮点击 | 缩放 0.95 | 100ms | ease-in-out |
| 数据加载 | 骨架屏闪烁 | 1.5s | ease-in-out |
| 进度更新 | 平滑过渡 | 500ms | ease-out |
| 条形图动画 | 从左向右增长 | 800ms | ease-out |
| 环形图动画 | 从0到目标值 | 1200ms | ease-out |

### 5.2 加载状态

```tsx
// 骨架屏
const DetectionSkeleton = () => (
  <div className="space-y-4 animate-pulse">
    <div className="h-12 bg-muted rounded-lg" />
    <div className="h-64 bg-muted rounded-lg" />
    <div className="grid grid-cols-3 gap-4">
      <div className="h-24 bg-muted rounded-lg" />
      <div className="h-24 bg-muted rounded-lg" />
      <div className="h-24 bg-muted rounded-lg" />
    </div>
  </div>
)

// 进度加载
const LoadingSpinner = ({ size = "md" }) => {
  const sizeClasses = {
    sm: "h-4 w-4",
    md: "h-8 w-8",
    lg: "h-12 w-12"
  }
  
  return (
    <Loader2 className={cn(sizeClasses[size], "animate-spin text-primary")} />
  )
}
```

---

## 六、技术实现要求

### 6.1 组件库依赖

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "typescript": "^5.0.0",
    "@radix-ui/react-dialog": "^1.0.0",
    "@radix-ui/react-dropdown-menu": "^2.0.0",
    "@radix-ui/react-progress": "^1.0.0",
    "@radix-ui/react-select": "^2.0.0",
    "@radix-ui/react-slot": "^1.0.0",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.0.0",
    "tailwind-merge": "^2.0.0",
    "lucide-react": "^0.300.0",
    "recharts": "^2.10.0",
    "tailwindcss": "^3.4.0",
    "framer-motion": "^10.0.0"
  }
}
```

### 6.2 项目结构

```
src/
├── components/
│   ├── ui/                    # 基础UI组件（shadcn/ui风格）
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── badge.tsx
│   │   ├── progress.tsx
│   │   ├── table.tsx
│   │   ├── input.tsx
│   │   ├── select.tsx
│   │   ├── dialog.tsx
│   │   ├── skeleton.tsx
│   │   ├── donut-chart.tsx      # 自定义环形图
│   │   ├── steps.tsx            # 自定义步骤条
│   │   └── ...
│   ├── layout/
│   │   ├── main-layout.tsx    # 主布局
│   │   └── page-header.tsx    # 页面头部
│   ├── detection/
│   │   ├── industry-card-grid.tsx  # 行业选择网格 ⭐
│   │   ├── brand-input.tsx         # 品牌输入框
│   │   ├── platform-status.tsx      # 平台状态
│   │   ├── detection-progress.tsx  # 检测进度条 ⭐
│   │   └── detection-form.tsx
│   ├── results/
│   │   ├── visibility-donut.tsx    # 可见度环形图 ⭐
│   │   ├── competitor-ranking.tsx   # 竞品排名条形图 ⭐
│   │   ├── opportunity-cards.tsx   # 机会卡片
│   │   └── optimization-suggestions.tsx
│   └── report/
│       ├── report-cover.tsx         # 报告封面 ⭐
│       ├── report-preview.tsx
│       └── report-template.tsx
├── lib/
│   ├── utils.ts                   # cn() 工具函数
│   ├── api.ts                     # API 调用
│   └── constants.ts                # 常量定义
├── pages/
│   ├── dashboard.tsx
│   ├── brands.tsx
│   ├── detection.tsx
│   ├── results.tsx
│   └── reports.tsx
└── App.tsx
```

---

## 七、质量标准

### 7.1 设计检查清单（21st-dev-magic强制使用）

- [ ] 所有组件使用21st-dev-magic获取（不是手动编写）
- [ ] 所有组件像素级对齐设计稿
- [ ] 深色/浅色主题支持
- [ ] 响应式布局（桌面/平板/手机）
- [ ] 加载状态完整（骨架屏、loading）
- [ ] 错误状态友好提示
- [ ] 空状态设计
- [ ] 动画流畅无卡顿（≥60fps）
- [ ] 无障碍访问（ARIA标签）

### 7.2 性能要求

| 指标 | 要求 |
|------|------|
| 首屏加载时间 | < 2秒 |
| 组件渲染时间 | < 100ms |
| 动画帧率 | ≥ 60fps |
| Lighthouse 评分 | ≥ 90 |

---

## 八、品牌视觉规范

### 8.1 水印规范（报告）

```
位置：每页右下角
内容：大鱼GEO Logo + "AI品牌机会发现引擎"
透明度：30%
大小：Logo高度 40px，文字 12px
```

### 8.2 颜色层级

```
一级标题：主色（科技蓝）
二级标题：深灰色
正文：中性灰
辅助信息：浅灰色
```

### 8.3 字体规范

```
主标题：32-48px，加粗
副标题：24px，中等
正文：16px，常规
辅助文字：14px，常规
水印文字：12px，常规
```

---

*文档版本历史*
- v1.0 (2026-05-30): 初始版本
- v2.0 (2026-05-31): **统一技术栈为shadcn/ui + Tailwind CSS**，增加21st-dev-magic组件获取流程，增加核心业务组件详细规范（IndustryCardGrid、DetectionProgressSteps、VisibilityDonutChart、CompetitorRankingChart、ReportCover）

