---
name: shopify-store-auditor
description: "用户要求Shopify店铺只读体检、上线准备审计、促销残留/追踪/移动体验检查时使用；实际修改转给 shopify-cro-optimizer 或 shopify-safe-deployment，审计本身不授予写入。"
---

# Shopify 店铺全面审计

## When to use

用户要求Shopify店铺只读体检、上线准备审计、促销残留/追踪/移动体验检查时使用。实际修改转给 shopify-cro-optimizer 或 shopify-safe-deployment，审计本身不授予写入。

## Preconditions

确认输入、当前版本、可用工具及本次授权范围。历史案例只作方法依据，不能替代当前验证。缺少关键输入时先做可独立完成的只读检查，再列阻塞。

## Procedure

1. 确认店铺、当前环境、审计日期、浏览器/只读API权限及可用源码版本。不要沿用历史主题ID作为当前LIVE/DEV角色证明。
2. 建立范围矩阵：首页、集合、商品、政策、导航、购物车、SEO、追踪、支付与配送。逐项记来源是本地快照、公开网页、预览主题还是Admin只读。
3. 先审本地Liquid/JS/配置，再在授权页面验证实际呈现；使用390、750、1440像素等实际可用视口，记录菜单、长文案、抽屉滚动/关闭与横向溢出。没有渲染不能宣称移动视觉PASS。
4. 购物车至少检查主商品、主商品+配件A、主商品+配件B、全部配件、无关商品五种状态，验证推荐去重与入口可达；会修改服务器购物车的操作须先有授权且用隔离会话。
5. 核对促销文字、图片烘焙文字、本地模板入口、远端折扣、商品价格和导航，分别给状态。本地移除促销不证明Admin自动折扣已关闭；历史URL可保留结束态。
6. 对追踪先定位theme/app/web pixel归属与请求证据，再判断重复事件；多个ID或端点不等于重复purchase。无事件级证据记UNKNOWN，不移除代码。
7. 支付/运费/市场只读检查权限范围内配置与说明一致性。结账入口200不代表支付成功；不输入客户数据、不下单、不付款。缺Admin权限的配置验收为BLOCKED。
8. 输出P0/P1/P2发现、复现路径、证据日期、影响、置信度、责任人/待分配与建议。区分全量静态错误基线和新增错误，不把零新增称为零错误。

## Tool permissions

允许本地快照读取、公开页面浏览和已授权的Admin只读查询。禁止编辑LIVE、支付、折扣、商品、库存和客户数据；本次无生产购物车写入授权时仅本地分析。

## Failure handling

遇登录/权限/预览失效停止该项；保留可继续的本地审计。缺少证据写UNKNOWN；确认缺陷NEED FIX；必须远端项不可访问BLOCKED，不能用旧报告补成当前PASS。

## Deliverables

审计矩阵、优先级发现、复现与证据、当前可验证边界及下一步；不得导出客户/订单明细。

## Acceptance criteria

每条结论标明检查范围、时间、版本及来源，缺陷可复现；本地、视觉、Admin、结账入口、付款分别验收。发布准备必需权限/预览缺失时不得给READY。

## Hard boundaries

不泄露密钥、客户隐私或非公开商业资料，不覆盖用户已有工作。读取权限不等于外发权限；生产变更按用户明确授权执行。

## Response contract

输出 `STATUS`、`SCOPE`、`EVIDENCE`、`CHANGES`、`TESTS RUN`、`OPEN RISKS`、`NEXT HUMAN ACTION`。逐项区分 PASS / NEED FIX / BLOCKED / NOT VERIFIED；历史记录、mock、本次本地与平台实测分列。

## Evidence and examples

阅读 [历史案例](references/cases.md) 时只加载与任务相关的案例；证据索引见其中链接。
