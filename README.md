# 电商商品经营分析（Power BI）

> 数据截至：2024-09-04（来自公开数据集的最大日期）  
> 口径：GMV=已完成订单金额；时间=下单日期；单位=千（K）
<img width="2077" height="1183" alt="image" src="https://github.com/user-attachments/assets/7c5f7da3-3a55-4ddf-a3ea-8fdd5155085f" />
## 交互说明
筛选器：
* 年份（Year）
* 商品线（男装/女装）
联动逻辑：
* 筛选器会同时影响 KPI、Top 商品、品类结构、气泡图与明细表
* 在任一图表点击品类/商品，可联动高亮与过滤明细表

---

## 项目目标
围绕电商商品经营核心问题搭建可交互看板，用于回答：
- 今年/某条商品线（男装/女装）GMV 与订单规模如何？
- GMV Top 商品与贡献占比是多少？是否头部集中？
- 品类结构（GMV占比）如何？哪些品类是高规模/高毛利的“优质品类”？
- 通过明细表联动下钻到商品与品牌，快速定位贡献来源

---

## 数据来源
公开数据集（Kaggle）：
```text
https://www.kaggle.com/datasets/chiraggivan82/ecommerce-bigquery?resource=download
```
---

# 指标口径说明（v0.1）

## 核心口径
- 时间口径：下单日期（order_date / created_at 的日期部分）
- GMV：已完成订单销售额（status = "Complete"）
- 单位：千（K）

## 指标
1. Completed GMV
- 定义：订单状态为 Complete 的销售额
- 说明：用于排除取消/处理中订单对收入的干扰

2. Completed Orders
- 定义：状态为 Complete 的订单数（去重 order_id）

3. AOV（客单价）
- 定义：Completed GMV / Completed Orders

4. Cancel Rate（取消率）
- 定义：Cancelled Orders / Orders
- 注：Orders 为所有订单数（去重 order_id）

5. Gross Profit（毛利额）
- 定义：Completed GMV - Completed COGS


6. Gross Margin（毛利率）
- 定义：Gross Profit / Completed GMV

## TopN Share
- Top10 GMV Share：Top10 商品 Completed GMV / 全部商品 Completed GMV
- Top50 GMV Share：同理，用于衡量头部集中度
