# Mezzanine Blog｜Django CMS 設定與部署練習

本 Repository 保存以 Mezzanine（建構於 Django 之上的 CMS）建立的網站專案設定，並包含 Heroku 部署所需的 Gunicorn、資料庫 URL 與靜態檔案設定。

## 專案內容

- Django／Mezzanine 專案設定。
- Mezzanine 預設管理後台與頁面／部落格路由整合。
- 以 TemplateView 設定首頁，並掛載 `mezzanine.urls`。
- 使用 `production_settings.py` 讀取部署環境的資料庫 URL。
- 使用 Gunicorn 作為 WSGI server，並設定 WhiteNoise／靜態檔案相關套件。

## 技術

- Python
- Django 3.2
- Mezzanine 5.1.3
- Gunicorn
- dj-database-url
- WhiteNoise
- PostgreSQL driver（requirements 中列出）

## 重要說明

- Repository 目前主要是 Mezzanine 專案骨架與部署設定，沒有足夠證據顯示自行開發了額外的 CMS 功能或自訂資料模型。
- 主設定檔的資料庫 ENGINE 與 NAME 仍為空白；部署設定則預期透過資料庫 URL 設定資料庫。
- `runtime.txt` 指定舊版 Python 3.6；依賴版本與部署環境均屬歷史設定，未重新驗證。
- 原本硬編碼的 Django `SECRET_KEY` 已在目前主分支替換為佔位值；Git 歷史未重寫，舊 commit 仍可能保留原始 secret。
- 本次未重新安裝依賴、啟動伺服器或確認舊部署服務狀態。

詳細技術範圍請參閱 [PROJECT_RETROSPECTIVE.md](PROJECT_RETROSPECTIVE.md)。
