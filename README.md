# DIVIN'IN 潛靜 — Fun Dive 行程頁面

東北角 Fun Dive 活動行程表，Config 驅動、每週改幾行就能更新。

## 🚀 部署到 GitHub Pages

用 Claude Code 在終端執行以下指令：

```bash
# 1. 進入專案資料夾
cd ~/divinin-fundive

# 2. 初始化 Git
git init
git add .
git commit -m "Initial commit: DIVIN'IN fundive itinerary"

# 3. 建立 GitHub Repo 並推送（需要先登入 gh）
gh repo create divinin-fundive --public --source=. --push

# 4. 啟用 GitHub Pages
gh api repos/{OWNER}/divinin-fundive/pages \
  -X POST \
  -f "source[branch]=main" \
  -f "source[path]=/"
```

> 把 `{OWNER}` 換成你的 GitHub 帳號名稱。
> 部署完成後，頁面網址為：`https://{OWNER}.github.io/divinin-fundive/`

---

## 📝 每週更新流程

1. 打開 `index.html`
2. 修改最上方的 `CONFIG` 區塊（約第 15–55 行）
3. 存檔後推送：

```bash
cd ~/divinin-fundive
git add .
git commit -m "更新本週行程：5/31 龍洞3號"
git push
```

4. 等 1–2 分鐘，同一個連結自動更新！

### CONFIG 欄位說明

| 欄位 | 說明 | 範例 |
|------|------|------|
| `date` | 活動日期 | `"2025-05-31"` |
| `weekday` | 星期幾 | `"週六"` |
| `diveSite` | 潛點名稱（自動連動集合地點 & 行程） | `"蝙蝠洞"` / `"龍洞3號"` / `"蚊子坑"` |
| `diveCount` | 潛水支數 | `2` |
| `weather` | 天氣描述 | `"晴天"` |
| `airTemp` | 地面氣溫 | `"28 – 33°C"` |
| `waterTemp` | 水溫 | `"約 27°C"` |
| `waterTempNote` | 水溫補充說明 | `"水溫舒適，無需額外保暖"` |
| `tide.high1` | 第一次滿潮時間 | `"05:30"` |
| `tide.low` | 乾潮時間 | `"11:20"` |
| `tide.high2` | 第二次滿潮時間 | `"17:00"` |
| `tide.waveHeight` | 浪高 | `"0 – 30 CM"` |
| `leader.name` | 活動負責人姓名 | `"Cho 教練"` |
| `leader.phone` | 負責人電話 | `"0912-345-678"` |
| `photoAlbum` | 活動照片 Google Drive 連結 | `"https://drive.google.com/..."` |

### 潮汐自動化（選用）

1. 前往 [中央氣象署 Open Data](https://opendata.cwa.gov.tw/) 註冊帳號
2. 取得免費 API Key
3. 填入 `cwaApiKey: "CWA-XXXXXXXX"`
4. 頁面載入時會自動抓取當天潮汐資料
5. 如果 API 失敗，會自動 fallback 到手動填寫的 `tide` 資料

---

## 📍 新增潛點

在 `DIVE_SITES` 物件中新增一組（複製現有潛點格式）：

```js
"新潛點名稱": {
  shuttle:   { time: "06:50", location: "圓山捷運站 2 號出口", mapUrl: "https://maps.app.goo.gl/xxx" },
  selfDrive: { time: "07:50", location: "集合店家名稱", address: "完整地址（選填）", mapUrl: "https://maps.app.goo.gl/xxx", tag: "標籤文字" },
  direct:    { time: "08:00", location: "潛點名稱", mapUrl: "https://maps.app.goo.gl/xxx" },
  warning:   "",  // 入口注意事項，沒有就留空
  schedule: [
    // 複製其他潛點的 schedule，修改時間和地名
  ]
}
```

然後在 `CONFIG.diveSite` 填入新名稱即可使用。

---

## 📱 RWD 支援

- 📱 手機（< 480px）
- 📱 小手機（< 360px）
- 📋 平板（481px – 1024px）
- 🖥️ 桌機（> 1024px）
- 🖥️ 大螢幕（> 1280px）
- ♿ 支援 `prefers-reduced-motion`
