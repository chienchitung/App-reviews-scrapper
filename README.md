# Overview

本專案旨在透過爬取 App Store 和 Google Play Store 上的用戶評論，深入分析用戶對應用程式的使用反饋，從而達成產品優化的目標。除了收集用戶評論之外，專案還將同步記錄應用程式的各個更新版本及中英文識別，以便精確識別每個版本的優化成果。

- 安裝爬蟲程式相關套件
```python
!pip install app-store-scraper -qqq
!pip install google-play-scraper -qqq
!pip install fasttext -qqq
!pip install emoji -qqq
```

- 使用FasText model進行語言檢測
```python
if not os.path.exists('lid.176.bin'):
    os.system('wget https://dl.fbaipublicfiles.com/fasttext/supervised-models/lid.176.bin')

model = fasttext.load_model('lid.176.bin')
```

- 到Google cloud console申請憑證 ([操作步驟](https://www.learncodewithmike.com/2020/08/python-write-to-google-sheet.html))
```python
# 設定憑證
scope = ['https://spreadsheets.google.com/feeds',
         'https://www.googleapis.com/auth/drive']

# 替換為你的服務帳號金鑰檔案路徑
creds = Credentials.from_service_account_file('{json key from Google cloud console}', scopes=scope)

gc = gspread.authorize(creds)

# 打開現有的 Google Sheet
spreadsheet_key = '{spreadsheet_key}'  # 替換為你的 spreadsheet key
spreadsheet = gc.open_by_key(spreadsheet_key)
```

- 可自行更換App id爬取評論
```python

# 下面網址 id 後面為，ios app id "959841107"
https://apps.apple.com/tw/app/蝦皮購物-花得更少買得更好/id959841107

# 下面網址 id 跟 & 之間的網址，為andriod app id "com.shopee.tw"
https://play.google.com/store/apps/details?id=com.shopee.tw&hl=en
```

- 參考來源
    - [Scrapping Data from AppStore](https://medium.com/@amaliaazizah160199/scrapping-data-from-appstore-1946773f0b9f)
    - [Apple App Store Reviews Scraper](https://github.com/glennfang/apple-app-reviews-scraper/tree/main)
