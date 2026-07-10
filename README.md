# 量化策略分析平台 — Quant Strategy Analyzer

基于双均线策略的交互式量化交易系统，支持回测、仓位管理和多模型扩展。

## 🚀 快速使用

直接双击打开 `strategy_analyzer_v4.html`，上传复权后的日线数据 Excel 即可使用。

## 📁 文件说明

| 文件 | 说明 |
|------|------|
| `strategy_analyzer_v4.html` | **主程序** — v4.3 量化交易系统（复选框条件选择版） |
| `strategy_analyzer.html` | v3.0 双均线策略图表（金叉/死叉标注） |
| `spec_v4_trading_system.md` | v4.3 交易系统设计规格 |
| `spec_interactive_ma_app.md` | v3.0 交互式网页规格 |
| `boe_specification.md` | 京东方A 双均线分析规格 |
| `boe_diagnostics_report.md` | 京东方A 数据诊断报告 |
| `boe_trading_system_v4.ipynb` | Python 交易系统回测 Notebook |
| `boe_dual_ma_analysis.ipynb` | Python 双均线分析 Notebook |
| `boe_dual_ma_chart.png` | 双均线策略图表（含金叉/死叉标注） |
| `京东方A_后复权日线数据.xlsx` | 京东方A 后复权日线样本数据 |

## 🎛️ 功能特性

- **多模型架构**：MODEL_REGISTRY 可扩展，当前支持双均线策略
- **买入管理**：金叉信号 + 趋势过滤（复选框独立开关）
- **卖出管理**：ATR止损 + 死叉止盈（复选框独立开关，支持全部平仓/减仓FIFO）
- **仓位管理**：风险比例规则，叠加建仓，独立止损
- **回测引擎**：逐日模拟，支持当日收盘价 / 次日开盘价两种成交模式
- **16项数据诊断**：概览、质量、收益率、量价关系四大类
- **绩效指标**：累计回报、最大回撤、夏普比率

## 🔧 技术栈

- 纯前端 HTML + ECharts + SheetJS
- 零依赖本地运行，无需安装任何环境

## 📊 样本回测结果 (京东方A 000725)

| 指标 | 数值 |
|------|------|
| 累计回报 | +88.85% |
| 最大回撤 | -16.70% |
| 夏普比率 | 1.72 |
| 金叉/死叉 | 各12次 |
