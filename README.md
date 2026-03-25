# 🛒 Amazon Search Product Scraper

[English](#english) | [中文](#中文)

---

<a name="english"></a>

## English

### 🚀 Amazon Product Search & Data Extraction

A powerful CafeScraper worker that searches Amazon by keywords and returns comprehensive product data including ASIN, title, price, rating, reviews, Prime status, and more. Supports multiple Amazon marketplaces (US, UK, DE, FR, JP).

### ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🔍 **Multi-Keyword Search** | Search multiple keywords in one run |
| 🌍 **Multi-Marketplace** | US, UK, Germany, France, Japan |
| 📊 **Rich Product Data** | ASIN, title, price, rating, reviews, Prime, badges |
| 🏷️ **Sponsored Filter** | Option to exclude sponsored products |
| 📈 **Rating/Reviews Filter** | Filter by minimum rating or review count |
| 📄 **Detail Page Fetch** | Optional category path and feature bullets |
| 🛡️ **Anti-Bot Bypass** | Playwright stealth mode for reliable scraping |

### 📋 Input Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `keywords` | array | - | **Required.** Search terms |
| `country` | string | `US` | Marketplace: US, UK, DE, FR, JP |
| `max_items_per_keyword` | integer | 50 | Max products per keyword (1-500) |
| `max_pages` | integer | 3 | Max pages per keyword (1-20) |
| `min_rating` | integer | 0 | Filter by minimum rating (0=no filter) |
| `min_reviews` | integer | 0 | Filter by minimum reviews (0=no filter) |
| `exclude_sponsored` | boolean | false | Exclude sponsored products |
| `fetch_details` | boolean | false | Fetch detail pages for extra data |
| `max_detail_items` | integer | 5 | Products to fetch details for |

### 📤 Output Fields

| Field | Description |
|-------|-------------|
| `asin` | Amazon Standard Identification Number |
| `title` | Product title |
| `price` | Current price (numeric) |
| `priceText` | Price display text |
| `rating` | Star rating (0-5) |
| `reviewsCount` | Number of reviews |
| `isPrime` | Prime eligible |
| `brand` | Brand name |
| `badges` | Best Seller, Amazon's Choice, etc. |
| `isSponsored` | Sponsored product flag |
| `imageUrl` | Main product image |
| `productUrl` | Product page URL |
| `categoryPath` | Category breadcrumb (if fetch_details) |
| `featureBullets` | Product features (if fetch_details) |

### 🚀 Quick Start

```bash
# Install dependencies
pip install -r requirements.txt
python -m playwright install chromium

# Run locally
python main.py
```

### ⚙️ Configuration Example

```json
{
  "keywords": [{"string": "iphone 17 case"}, {"string": "usb c hub"}],
  "country": "US",
  "max_items_per_keyword": 50,
  "max_pages": 3,
  "min_rating": 4,
  "exclude_sponsored": true,
  "fetch_details": true,
  "max_detail_items": 5
}
```

---

<a name="中文"></a>

## 中文

### 🚀 亚马逊产品搜索与数据提取

一款强大的 CafeScraper Worker，通过关键词搜索亚马逊并返回全面的产品数据，包括 ASIN、标题、价格、评分、评论数、Prime 状态等。支持多个亚马逊市场（美国、英国、德国、法国、日本）。

### ✨ 核心功能

| 功能 | 说明 |
|------|------|
| 🔍 **多关键词搜索** | 一次运行搜索多个关键词 |
| 🌍 **多市场支持** | 美国、英国、德国、法国、日本 |
| 📊 **丰富产品数据** | ASIN、标题、价格、评分、评论、Prime、徽章 |
| 🏷️ **赞助过滤** | 可选择排除赞助商品 |
| 📈 **评分/评论过滤** | 按最低评分或评论数过滤 |
| 📄 **详情页获取** | 可选获取分类路径和产品特性 |
| 🛡️ **反爬虫绕过** | Playwright 隐身模式确保稳定抓取 |

### 📋 输入参数

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `keywords` | array | - | **必填。** 搜索关键词 |
| `country` | string | `US` | 市场：US, UK, DE, FR, JP |
| `max_items_per_keyword` | integer | 50 | 每个关键词最大商品数（1-500） |
| `max_pages` | integer | 3 | 每个关键词最大页数（1-20） |
| `min_rating` | integer | 0 | 按最低评分过滤（0=不过滤） |
| `min_reviews` | integer | 0 | 按最低评论数过滤（0=不过滤） |
| `exclude_sponsored` | boolean | false | 排除赞助商品 |
| `fetch_details` | boolean | false | 获取详情页额外数据 |
| `max_detail_items` | integer | 5 | 获取详情的商品数量 |

### 📤 输出字段

| 字段 | 说明 |
|------|------|
| `asin` | 亚马逊标准识别号 |
| `title` | 产品标题 |
| `price` | 当前价格（数值） |
| `priceText` | 价格显示文本 |
| `rating` | 星级评分（0-5） |
| `reviewsCount` | 评论数量 |
| `isPrime` | 是否支持 Prime |
| `brand` | 品牌名称 |
| `badges` | 畅销榜、亚马逊推荐等徽章 |
| `isSponsored` | 是否为赞助商品 |
| `imageUrl` | 主产品图片 |
| `productUrl` | 产品页面 URL |
| `categoryPath` | 分类面包屑（需启用 fetch_details） |
| `featureBullets` | 产品特性列表（需启用 fetch_details） |

### 🚀 快速开始

```bash
# 安装依赖
pip install -r requirements.txt
python -m playwright install chromium

# 本地运行
python main.py
```

### ⚙️ 配置示例

```json
{
  "keywords": [{"string": "iphone 17 手机壳"}, {"string": "type c 扩展坞"}],
  "country": "US",
  "max_items_per_keyword": 50,
  "max_pages": 3,
  "min_rating": 4,
  "exclude_sponsored": true,
  "fetch_details": true,
  "max_detail_items": 5
}
```

---

## 🔧 Technical Details | 技术细节

| Item | Value |
|------|-------|
| Platform | CafeScraper |
| Runtime | Python 3.11+ |
| Browser | Playwright (Stealth Mode) |
| Anti-Bot | playwright-stealth |
| Proxy Support | Platform PROXY_AUTH |

---

## ⚠️ Notes | 注意事项

- Amazon uses strong anti-bot measures. This worker uses stealth mode for reliable scraping. | 亚马逊使用强反爬虫措施，此 Worker 使用隐身模式确保稳定抓取。
- For production use, keep concurrency low and use platform proxy. | 生产环境建议降低并发并使用平台代理。
- CDP browser connection requires `PROXY_AUTH` environment variable. | CDP 浏览器连接需要 `PROXY_AUTH` 环境变量。

---

## 📜 License

MIT License © 2024 kael-odin

## 🔗 Links

- [GitHub Repository](https://github.com/kael-odin/worker-Amazon-Search-Product-Scraper)
- [Report Issues](https://github.com/kael-odin/worker-Amazon-Search-Product-Scraper/issues)
