# 1.建環境（conda / Python 3.10）

把畫布裡的 environment.yml 存到專案資料夾的根目錄（例如 miniworld/）
開啟終端機：
conda --version
conda env create -f environment.yml
conda activate miniworld666


# 2.建專案結構與檔案
在 VS Code 建一個空資料夾（例如 miniworld/），將畫布中每個「==== 文件：... ====" 區塊另存成對應檔案與路徑（含 routes/、templates/ 子資料夾）。把 .env.example 另存一份成 .env。

# 3.設定資料庫連線（.env）
.env 內容已放入你的連線（140.117.68.66 / project_4 / czb2g4）。確保伺服器端允許你的 IP 存取 5432。
若你用 pgAdmin4 測過可連線，Flask 這邊就沒問題。

# 4.啟動 Flask
在 VS Code 右下角選擇 miniworld666 解譯器

終端機執行：
set FLASK_APP=app.py   
### Windows PowerShell 請改：$env:FLASK_APP=\"app.py\"
flask run

A.正常模式:
瀏覽器打開 http://127.0.0.1:5000/
 ，應能看到儀表；上方導覽可進「客人 / 訂單 / 機器人 / 送餐紀錄」
B. 網頁APP檢查模式（不連 DB）:
在同一個 flask run 執行中，瀏覽 http://127.0.0.1:5000/healthz
若看到 {"app":"ok"} 代表 Flask 跑得好，問題在 DB 連線。DB檢查模式(
C. 網頁DB檢查模式:
瀏覽 http://127.0.0.1:5000/dbz
若是 {"db":"ok"}，表示 DB 可達；首頁應該會正常顯示統計。
若是 {"db":"down"}，代表你的機器 目前到 140.117.68.66:5432 不可達 或帳密/DB 名不符。此時首頁會顯示警示訊息，而不會無限轉圈。

# 5.快速驗收
先到「客人」→ 新增一位客人
到「訂單」→ 新增訂單（選剛剛那個客人，填 1~2 個品項，金額會自動加總）
進入訂單明細 → 「切換狀態」看 TODO↔DONE 是否生效
在明細底下「送餐」→ 選一個機器人（若沒有先到「機器人」新增），送出後到「送餐紀錄」看是否出現

# 6.Git 初始化（可選）
git init
git add .
git commit -m "init: flask miniworld (conda py310)"
git branch -M main
git remote add origin <你的 GitHub repo URL>
git push -u origin main
