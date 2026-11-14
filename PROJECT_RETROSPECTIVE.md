# Mezzanine Blog：技術經歷回顧

> 本文件依據 Repository 中的 Django／Mezzanine 設定、URL、部署檔案及相依套件整理。此 Repository 主要呈現 CMS 專案設定與部署環境配置；不把框架本身的內建功能誤寫為自行開發的功能。

## 1. 專案定位

此專案使用 Mezzanine 作為 Django CMS。程式碼主要包含：

- Django settings 與 Mezzanine dynamic settings。
- Mezzanine 管理後台及預設 URL patterns。
- 首頁 TemplateView。
- production settings、資料庫 URL 及靜態檔案設定。
- Heroku Procfile、Python runtime 與 requirements。

目前沒有看到額外自訂 Django app、獨立資料模型或自訂 CMS 功能，因此合理定位是 Django／Mezzanine CMS 設定與部署練習。

## 2. Django／Mezzanine 設定

主要檔案：`myblog/settings.py`

- 設定繁體中文語系及 Asia/Taipei 時區。
- 使用 Mezzanine authentication backend。
- 設定 Django／Mezzanine app 與中介層。
- 設定預設首頁及網站相關參數。
- 設定 `ALLOWED_HOSTS`、`DEBUG` 及靜態檔案位置。

主要檔案：`myblog/urls.py`

- 使用 `i18n_patterns` 包裝管理後台路由。
- 使用 TemplateView 指向首頁模板。
- include `mezzanine.urls`，交由 Mezzanine 處理 CMS 頁面及其他預設路由。

這些功能主要來自 Mezzanine 框架設定，不能視為自行從零實作 CMS 或部落格系統。

## 3. 部署設定

### Production settings

`myblog/production_settings.py`：

- 匯入主要 settings。
- 使用 `dj_database_url.config()` 讀取環境提供的資料庫連線設定。
- 設定 `STATIC_ROOT`。
- 設定反向代理 HTTPS header。
- 關閉 DEBUG。

### Heroku 執行設定

- `Procfile` 使用 Gunicorn 啟動 WSGI application。
- `runtime.txt` 指定 Python 3.6。
- `requirements.txt` 固定 Django、Mezzanine、Gunicorn、dj-database-url、WhiteNoise 及資料庫 driver 等套件版本。

這些檔案可佐證曾接觸 Django production settings、WSGI server、環境變數式資料庫配置及 PaaS 部署設定；但不代表歷史部署目前仍在線。

## 4. 技術能力摘要

| 技術 | 程式證據 | 合理定位 |
|---|---|---|
| Python／Django | settings、URL、WSGI | 有 Django 專案設定經驗 |
| Mezzanine | app settings、預設 URL 整合 | 有使用 Django CMS framework 經驗 |
| Gunicorn | Procfile | 有 WSGI server 部署設定經驗 |
| dj-database-url | production settings | 有環境資料庫 URL 配置經驗 |
| WhiteNoise | requirements／靜態檔案設定 | 有靜態資源部署設定接觸 |
| Heroku | Procfile、runtime、production settings | 有 PaaS 部署設定接觸 |

## 5. 已知限制

- 主設定檔的資料庫 ENGINE 與 NAME 是空字串，不能單靠該檔案啟動資料庫連線。
- Production settings 依賴部署環境提供資料庫 URL；沒有看到可確認的現行環境設定。
- `runtime.txt` 使用 Python 3.6，屬歷史環境設定。
- 沒有看到自訂 Django app 或額外功能程式碼，因此履歷不應誇大成獨立開發完整 CMS。
- 沒有測試或重新部署紀錄。

## 6. 履歷描述建議

使用 Django 與 Mezzanine 建立 CMS 專案環境，設定網站語系、時區、管理後台及頁面路由，並配置 Gunicorn、資料庫 URL 與靜態檔案等 production deployment settings，接觸 Django CMS 與 PaaS 部署流程。

## 7. 安全整理紀錄

- 主設定檔原本包含硬編碼 Django `SECRET_KEY`，目前主分支已替換為 `SECRET_KEY` 佔位值。
- Git commit history 未重寫，舊 commit 仍可能保留原始 secret。若該金鑰曾用於部署，應視為已曝光並重新產生。

## 8. 驗證界線

- 未重新安裝 requirements。
- 未啟動 Django server 或執行部署。
- 未確認 Heroku app 或資料庫目前狀態。
- 本文件只描述 Repository 中可見的框架設定與部署配置。
