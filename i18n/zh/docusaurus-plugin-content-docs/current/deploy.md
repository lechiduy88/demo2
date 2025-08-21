# 部署

AI Short 是一個開源專案。您可以自由修改網站的名稱與描述。

- 若要修改網站名稱，請編輯 `docusaurus.config.js` 檔案。
- 若要修改說明文件，請前往 `docs` 目錄。
- 若要修改提示詞，請在 `src/data/prompt.json` 中找到相關檔案。若只需修改單一語言，例如中文，可以直接編輯 `src/data/prompt_zh.json`。
- 目前使用者後台與共用後端系統相連，如有需要，您可以建立自己的後端。相關介面位於 `src/api.js`。

`CodeUpdateHandler.py` 是一個用於多語言部署的批次處理腳本。完成修改後執行 `python CodeUpdateHandler.py`，它會依照規則將 `prompt.json` 拆分成多語言版本，並同步更新各語言的主頁程式碼以及選定提示詞的獨立頁面程式碼。

## 部署說明

系統需求：

- [Node.js 18.0](https://nodejs.org/) 或更新版本  
- 支援 macOS、Windows（含 WSL）與 Linux

### 本地部署

請確保您已安裝 [Node.js](https://nodejs.org/)。

# 安裝
yarn

# 本地開發
yarn start

# 建置：此指令會在 `build` 目錄中產生靜態內容
yarn build

# 更新 `docusaurus.config.js` 檔案中的 `defaultLocale`，然後為所需語言執行建置
yarn build --locale zh
yarn build --locale en
yarn build --locale ja
yarn build --locale ko
yarn build --locale es
yarn build --locale fr
yarn build --locale de
yarn build --locale it
yarn build --locale ru
yarn build --locale pt
yarn build --locale hi
yarn build --locale ar
yarn build --locale bn

# 多語言部署
yarn build --locale zh && yarn build --locale en
```

### Vercel 部署

點擊下方按鈕，即可一鍵在 Vercel 平台部署 ChatGPT-Shortcut：

[![Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Frockbenben%2FChatGPT-Shortcut%2Ftree%2Fmain)

**注意**：Vercel 免費方案可能因記憶體不足而出現錯誤。在這種情況下，您可以選擇僅部署單一語言。具體步驟如下：

1. 前往剛剛建立的 Vercel 專案，打開 **Settings**。
2. 在 **Build & Deployment** 區段找到 **Build Command**，然後點擊右側的 **Override**。
3. 修改部署指令。例如：若要部署中文版，請使用 `yarn build --locale zh`；若要部署葡萄牙文版，請使用 `yarn build --locale pt`。

## Cloudflare Pages 部署

點擊下方按鈕或連結來 fork 此專案，然後依照說明在 Cloudflare Pages 上進行部署：

👉 [Fork 此專案](https://github.com/rockbenben/ChatGPT-Shortcut/fork)

部署步驟：

1. 登入 [Cloudflare Pages](https://pages.cloudflare.com/)，並選擇 **"Create a project"**。
2. 綁定剛剛 fork 的程式庫。
3. 設定建置指令：
   - **建置指令**：`yarn build --locale zh` （請根據要部署的語言選擇對應的 locale；例如葡萄牙文請使用 `yarn build --locale pt`）。
   - **輸出目錄**：`build`
4. 點擊 **Deploy**，並等待 Cloudflare Pages 完成建置與部署流程。

Cloudflare Pages 會在每次您 push 新程式碼時，自動觸發建置與部署。

### Docker 部署

如果您熟悉 Docker，可以使用以下指令快速部署：

```bash
# ghcr.io
docker run -d -p 3000:3000 --name chatgpt-shortcut ghcr.io/rockbenben/chatgpt-shortcut:latest

# docker hub
docker run -d -p 3000:3000 --name chatgpt-shortcut rockben/chatgpt-shortcut:latest
```

另外，您也可以使用 `docker-compose` 進行部署：

```yml
version: "3.8"

services:
  chatgpt-shortcut:
    container_name: chatgpt-shortcut
    image: ghcr.io/rockbenben/chatgpt-shortcut:latest
    ports:
      - "3000:3000"
    restart: unless-stopped

## 同步更新

如果您曾透過一鍵在 Vercel 部署專案，可能會遇到更新無法持續同步的情況。這是因為 Vercel 預設會為您建立一個新專案，而不是 fork 現有專案，導致更新檢測異常。建議按照以下步驟重新部署：

1. 移除先前的程式庫。
2. 使用頁面右上角的 **Fork** 按鈕 fork 當前專案。
3. 前往 [Vercel「New Project」頁面](https://vercel.com/new)，在「Import Git Repository」區段中選擇剛 fork 的專案並進行部署。

### 自動更新

> 如果在執行 Upstream Sync 時出現錯誤，請手動執行單次 Sync Fork。

專案 fork 完成後，因 GitHub 限制，您需要在 fork 專案的 **Actions** 頁面手動啟用工作流程，並啟用 Upstream Sync 動作。啟用後，系統會每天自動執行更新。

![自動更新](https://img.newzone.top/2023-05-19-11-57-59.png?imageMogr2/format/webp)

![啟用自動更新](https://img.newzone.top/2023-05-19-11-59-26.png?imageMogr2/format/webp)

### 手動更新

如果您希望立即進行手動更新，可以參考 [GitHub 文件](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork)，了解如何將 fork 的專案與上游程式碼同步。

💡 如果覺得這個專案對您有幫助，歡迎點個 ⭐star 支持，或追蹤作者以便及時獲取新功能更新通知。

