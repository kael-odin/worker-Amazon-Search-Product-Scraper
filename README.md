# Amazon Search & Product Scraper

CafeScraper worker that searches Amazon by keywords and returns product list data (ASIN, title, price, rating, etc.) for analysis or export.

## Required files (project root)

| File | Purpose |
|------|--------|
| `main.py` | Entry point |
| `scraper.py` | Scraping logic |
| `requirements.txt` | Python dependencies |
| `input_schema.json` | Input form config |
| `README.md` | This file |
| `sdk.py`, `sdk_pb2.py`, `sdk_pb2_grpc.py` | CafeScraper SDK |

## Input

- **keywords** (required): list of search terms, e.g. `["iphone case", "usb c hub"]`
- **max_items_per_keyword** (default 50): max products per keyword
- **max_pages** (default 3): max result pages per keyword (1–20)
- **country** (default US): marketplace — US, UK, DE, FR, JP
- **min_rating** / **min_reviews**: optional filters; 0 = no filter
- **exclude_sponsored** (default false): drop sponsored results
- **fetch_details** (default false): open detail pages for first N items to get category path and feature bullets
- **max_detail_items** (default 5): N when fetch_details is true

## Output

Each row includes: keyword, country, pageIndex, asin, title, productUrl, priceText, price, originalPriceText, rating, reviewsCount, isPrime, brand, badges, isSponsored, imageUrl, currency; optionally categoryPath and featureBullets when fetch_details is enabled.

## Run

The platform runs `python main.py` and supplies input via the SDK. Proxy is optional via `PROXY_AUTH` (e.g. `socks5://{PROXY_AUTH}@proxy-inner.cafescraper.com:6000`).

**Playwright / Chromium:** The script first tries to use a system Chromium or Chrome if present (`chromium`, `chromium-browser`, `google-chrome` in PATH). If none is found, it tries to run `playwright install chromium` into `/tmp/playwright_browsers`. If you still see "Executable doesn't exist", the run environment has no browser and no network to download one — **contact CafeScraper support** and ask them to either run `playwright install chromium` before tasks (e.g. in a build step) or use a Docker image that has Chromium/Chrome preinstalled.

**Input / input_schema:** CafeScraper may not use our `input_schema.json` format (their UI often shows only Execution Node, Version, Timeout, Memory). We use defaults when the platform sends minimal input (see `DEFAULT_INPUT` in `main.py`). To pass keywords or country, use whatever input form CafeScraper provides, or ask them for the correct schema format.

## Anti-bot

Amazon uses strong anti-bot measures. This worker uses a realistic browser profile and basic CAPTCHA detection. For production, use the platform’s proxy and keep concurrency low.

---

## Troubleshooting: "Executable doesn't exist" (Chromium not found)

**Cause:** The script needs a Chromium or Chrome binary. In the run environment: (1) No system Chromium/Chrome in PATH. (2) `playwright install chromium` cannot complete (often no outbound network), so the browser is never downloaded.

**What to ask CafeScraper:** The run environment must provide Chromium or Chrome — e.g. run `playwright install chromium` in a build step before tasks, or use a Docker image with Chromium/Chrome preinstalled.

### 反馈模板（发给 CafeScraper 支持）

运行 Script 任务时报错：`BrowserType.launch: Executable doesn't exist at .../chrome-headless-shell`。

**原因：** 脚本依赖 Playwright 的 Chromium 才能跑。当前执行环境里 (1) 没有预装 Chromium/Chrome；(2) 运行时无法访问外网，导致脚本内执行 `playwright install chromium` 无法下载浏览器，所以启动失败。

**请支持在「构建/准备」阶段（在真正跑脚本之前）执行：**  
`playwright install chromium`  
或改用已预装 Chromium/Chrome 的 Docker 镜像，让任务运行时能直接使用浏览器。谢谢。
