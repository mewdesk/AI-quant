# 量化策略分析工具 v3.0 — 交互式网页规格文件

## 目标

构建一个**纯前端单页交互式量化策略分析网页**，用户可以上传 Excel 数据，选择模型和参数，实时查看策略分析结果。

## 技术栈

| 组件 | 方案 |
|------|------|
| 文件解析 | SheetJS (xlsx) CDN |
| 图表渲染 | ECharts 5.x CDN |
| 架构 | 纯前端单 HTML 文件，无后端依赖 |
| 页面结构 | 卡片式布局，响应式设计 |

## 页面结构（6大区块）

### ① 上传区
- 拖拽/点击上传 Excel (.xlsx) / CSV 文件
- ⚠️ 醒目提示：**请上传复权后的数据**（前复权/后复权均可）
- 列名自动匹配（支持中英文列名：日期/trade_date、开盘价/open、收盘价/close等）
- 上传后展示"数据预览（前5行）"
- 自动解析日期并排序

### ② 模型选择 + 动态参数面板
- 下拉选择框列出所有注册模型
- 参数面板根据模型动态渲染（MA周期、标准差倍数等）
- 已实现：双均线交叉 (MA Crossover)
- 预留：MACD、布林带、RSI

### ③ 绩效指标面板
- 4个核心指标卡片：累计回报、最大回撤、夏普比率、总信号次数
- 上涨用红色、下跌用绿色（A股习惯）
- 日期范围筛选器（1-5年可选）

### ④ ECharts 策略图表
- 价格走势线 + MA线 + 金叉/死叉标注
- ▲红色三角 = 金叉（买入信号）
- ▼绿色三角 = 死叉（卖出信号）
- 支持缩放（dataZoom）
- 自适应窗口大小

### ⑤ 数据诊断
- 总交易日数、日期范围、缺失值、异常波动日

### ⑥ 信号统计
- 信号类型汇总表
- 信号明细列表（日期、信号类型、价格）

## 模型注册架构 (MODEL_REGISTRY)

每个模型需实现3个方法：

```javascript
{
  name: '模型名称',
  params: [{ key, label, type, min, max, default }],  // 参数定义
  analyze(data, params) → { maShort, maLong, signals, cumulativeReturn, ... },
  getChartSeries(result, dates, closes) → [ECharts series],
  getSignalStats(result) → [{ type, label, count }],
  getChartTitle(params) → '图表标题',
}
```

## 数据流

```
上传Excel → SheetJS解析 → 列名匹配 → 日期排序 → 日期范围裁剪
  → 模型分发 → analyze()计算 → 指标更新 + ECharts渲染 + 信号统计
```

---

*规格版本: v3.0 | 实现状态: 双均线已完成，MACD/布林带/RSI预留*
