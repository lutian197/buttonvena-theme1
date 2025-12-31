# 订单追踪页面开发指南

## 概述

`templates/page.track-your-order.json` 是一个自动生成的 Shopify 主题模板文件。该文件包含一个 `custom-liquid` 块，用于显示订单追踪功能。

## 开发方式

由于模板文件是自动生成的，**不建议直接修改** `page.track-your-order.json` 文件。推荐使用以下两种方式：

### 方式一：使用 Snippet（推荐）

1. **已创建的 snippet 文件**：`snippets/track-order.liquid`

   - 这是一个可重用的订单追踪组件
   - 包含表单、样式和 JavaScript 逻辑

2. **在 Shopify 后台使用**：
   - 登录 Shopify 后台
   - 进入 **在线商店 > 主题 > 自定义**
   - 打开 "Track Your Order" 页面
   - 找到 `custom-liquid` 块
   - 在代码编辑器中输入以下代码：

```liquid
{% render 'track-order' %}
```

### 方式二：直接在 Custom Liquid 块中编写代码

如果不想使用 snippet，也可以直接在 custom-liquid 块中编写完整的 Liquid 代码。

## 功能说明

当前的 `track-order.liquid` snippet 包含：

1. **订单追踪表单**

   - 订单号输入框
   - 邮箱地址输入框
   - 提交按钮

2. **基础样式**

   - 响应式设计
   - 与主题风格一致的样式

3. **JavaScript 逻辑**
   - 表单提交处理
   - 结果展示（目前是占位符）

## 下一步开发

### 1. 集成订单追踪 API

当前代码中的 JavaScript 部分是占位符。你需要：

- **选项 A：使用 Shopify Order Status API**

  ```javascript
  // 使用 Shopify 的订单状态页面
  // 需要配置 Shopify 的订单状态页面设置
  ```

- **选项 B：集成第三方物流 API**

  ```javascript
  // 例如：UPS、FedEx、DHL 等
  const response = await fetch('/apps/order-tracking/api/track', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ order_number: orderNumber, email: email })
  });
  ```

- **选项 C：使用 Shopify App**
  ```javascript
  // 使用 Shopify App 提供的订单追踪功能
  // 例如：AfterShip、Tracktor 等应用
  ```

### 2. 添加翻译

如果需要多语言支持，可以在翻译文件中添加：

**locales/en.default.json**:

```json
{
  "pages": {
    "track_order": {
      "title": "Track Your Order",
      "description": "Enter your order number and email address to track your order status.",
      "order_number": "Order Number",
      "order_number_placeholder": "Enter order number",
      "email": "Email Address",
      "email_placeholder": "Enter your email",
      "submit": "Track Order"
    }
  }
}
```

**locales/zh-CN.json**:

```json
{
  "pages": {
    "track_order": {
      "title": "追踪您的订单",
      "description": "请输入订单号和邮箱地址以查询订单状态。",
      "order_number": "订单号",
      "order_number_placeholder": "请输入订单号",
      "email": "邮箱地址",
      "email_placeholder": "请输入您的邮箱",
      "submit": "查询订单"
    }
  }
}
```

### 3. 自定义样式

如果需要修改样式，可以：

1. 在 `snippets/track-order.liquid` 中修改 `<style>` 部分
2. 或者在主题的 CSS 文件中添加自定义样式类

### 4. 添加更多功能

可以考虑添加：

- 订单历史记录
- 物流跟踪地图
- 预计送达时间
- 订单详情展示
- 邮件通知功能

## 文件结构

```
shopify/
├── snippets/
│   └── track-order.liquid          # 订单追踪组件（已创建）
├── templates/
│   └── page.track-your-order.json  # 页面模板（自动生成，不要直接修改）
└── assets/
    └── (可选) track-order.js        # 如果需要更复杂的 JavaScript 逻辑
```

## 注意事项

1. ⚠️ **不要直接修改** `page.track-your-order.json` 文件，因为它会被自动覆盖
2. ✅ **使用 snippet** 方式开发，代码更易维护
3. ✅ 在 Shopify 后台的主题编辑器中编辑 custom-liquid 块的内容
4. ✅ 测试时确保订单号和邮箱验证逻辑正确
5. ✅ 考虑 GDPR 和隐私政策要求

## 测试步骤

1. 在 Shopify 后台创建测试订单
2. 访问订单追踪页面
3. 输入订单号和邮箱
4. 验证结果是否正确显示
5. 测试错误处理（无效订单号、错误邮箱等）

## 相关资源

- [Shopify Liquid 文档](https://shopify.dev/docs/api/liquid)
- [Shopify Order Status API](https://shopify.dev/docs/api/admin-rest/2023-10/resources/order)
- [Shopify Theme 开发文档](https://shopify.dev/docs/themes)
