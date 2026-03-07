# 🌐 Free Proxy Scraper

Automatically scrapes, checks, and saves free proxies to a formatted Excel file every hour — powered by GitHub Actions (completely free).

## 📦 What's included

| File | Purpose |
|------|---------|
| `proxy_scraper.py` | Main scraper script |
| `requirements.txt` | Python dependencies |
| `.github/workflows/scrape.yml` | Hourly GitHub Actions scheduler |
| `proxies.xlsx` | Auto-generated Excel output (updated hourly) |
| `summary.json` | Machine-readable stats (updated hourly) |

## 🚀 Setup (5 minutes)

### 1. Create a new GitHub repository

Go to [github.com/new](https://github.com/new) and create a **public** or **private** repo.

### 2. Upload all files

Upload these files keeping the folder structure:
```
your-repo/
├── proxy_scraper.py
├── requirements.txt
└── .github/
    └── workflows/
        └── scrape.yml
```

> ⚠️ The `.github/workflows/` folder must be created exactly as shown.

### 3. Enable Actions write permissions

Go to your repo → **Settings** → **Actions** → **General**  
Under *Workflow permissions*, select **Read and write permissions** → Save.

### 4. Run it manually first

Go to **Actions** tab → click **🌐 Proxy Scraper** → click **Run workflow**.  
Watch the logs — it should complete in ~5–10 minutes.

### 5. Sit back — it runs every hour automatically ✅

GitHub Actions will trigger the workflow at the top of every hour via cron.

---

## 📊 Output: proxies.xlsx

The Excel file has 3 sheets:

| Sheet | Contents |
|-------|---------|
| **All Proxies** | Every scraped proxy with status, latency, country, protocol |
| **✅ Live Proxies** | Working proxies only, sorted fastest → slowest |
| **📊 Summary** | Live/dead counts, live rate %, breakdown by source & protocol |

---

## 🔧 Configuration

Edit the top of `proxy_scraper.py` to tweak:

```python
CHECK_TIMEOUT = 8    # seconds before a proxy is marked dead
MAX_WORKERS   = 60   # concurrent threads for checking
```

To change the schedule, edit `.github/workflows/scrape.yml`:
```yaml
- cron: "0 * * * *"   # every hour  (default)
- cron: "0 */2 * * *" # every 2 hours
- cron: "0 */6 * * *" # every 6 hours
```

---

## 📥 Downloading proxies.xlsx

After each run:
- **From the repo**: The file is committed directly — just download `proxies.xlsx`
- **From Actions artifacts**: Go to the Actions run → scroll down → download the artifact (kept for 7 days)

---

## 🕷️ Sources scraped

| Source | Update Frequency |
|--------|----------------|
| free-proxy-list.net | Every 30 min |
| proxyscrape.com (HTTP/SOCKS4/SOCKS5) | Every 5 min |
| proxynova.com | Every 15 min |
| geonode.com | Continuous |
| github/proxifly | Every 5 min |
| github/TheSpeedX | Daily (~8,000 proxies) |

---

## ⚠️ Disclaimer

Free proxies are public IPs scraped from the internet. Never use them for sensitive tasks, login sessions, or anything requiring privacy. For personal/research use only.
