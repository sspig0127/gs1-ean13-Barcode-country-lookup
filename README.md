# GS1 食品條碼國別查詢工具 (GS1 Food Barcode Scanner)

這是一個專為手機瀏覽器設計的純前端單頁應用程式 (SPA)。使用者可透過手機相機掃描食品包裝上的 **EAN-13 條碼**，程式會自動解析開頭三碼 (GS1 Prefix)，並快速查詢、顯示該條碼是由哪一個國家/地區的 GS1 會員組織所核發。

👉 **[Live Demo 線上預覽](https://sspig0127.github.io/gs1-ean13-Barcode-country-lookup/)** 

> ⚠️ **重要觀念宣導**：
> 食品條碼開頭的三碼代表「**發行該條碼的 GS1 組織所在國家**」，這**不等於**該產品的實際製造國或原產地。例如：台灣公司 (471) 可能在中國設廠製造商品，但條碼依然會是 471 開頭。本程式已在介面中加入相關防呆提醒。

---

## ✨ 功能特色

- **🎯 專精 EAN-13 解析**：底層採用優化過的 `Quagga2` 引擎，專注解析 EAN-13 等商品條碼，拔除不必要的二維碼解析，大幅提升掃描速度。
- **🛡️ 智慧防抖機制**：內建連續幀比對演算法，必須連續多幀掃出相同結果才判定成功，徹底解決 1D 條碼常見的誤讀問題。
- **🔦 硬體手電筒 (Torch) 支援**：自動偵測手機鏡頭是否支援手電筒，支援在光線不足時手動開啟補光（具備錯誤捕捉與 UI 震動提示）。
- **🌍 內建完整 GS1 國別資料庫**：免連網 API，程式內部已建置涵蓋全球的 GS1 Prefix 對照表，掃描後瞬間顯示結果。
- **🌐 多國語系 (i18n)**：內建繁體中文 (zh-TW) 與英文 (en) 介面，支援一鍵即時切換。
- **📱 離線優先與隱私安全**：完全以純 HTML/CSS/JS 實作，條碼資料僅在本地端瀏覽器處理，無任何後端伺服器資料傳輸。

---

## 🚀 快速開始

這是一個完全靜態的專案，不需要安裝任何 Node.js 模組或建置工具。

1. 將本專案 Clone 到本地端：
   ```shell
   git clone https://github.com/sspig0127/gs1-ean13-Barcode-country-lookup.git
   ```

1. 直接用瀏覽器開啟 `index.html`。

2. 或者，若要測試手機相機功能，請使用 Live Server 或其他本地伺服器工具（相機權限需在 `localhost` 或 `https://` 環境下才能運作）：

   ```shell
   npx serve .
   ```



## 🛠️ 開發與客製化

## 調整防抖強度

若發現條碼很難掃描，或是掃描太快導致誤讀，可以調整原始碼中的防抖常數：

```
javascript// 預設需要連續 2 次掃出同樣字串才算成功。數字越大越嚴謹，但也需要對準越久。
const REQUIRED_MATCHES = 2; 
```

## 擴充 GS1 對照表

若未來 GS1 總部有新增前置碼，您可以直接修改 `getGS1Country(barcode)` 函式中的 `if-else` 邏輯，例如：

```
javascriptif (prefix === 471) return "台灣 (Taiwan)";
// 在此處加入新的 Prefix 判斷
```

------

## 📦 使用套件

- [Quagga2 (@ericblade/quagga2)](https://github.com/ericblade/quagga2) - 負責高效的 1D 條碼即時影像解析與綠框定位追蹤。

## 📄 授權條款

本專案採用 [MIT License](https://www.perplexity.ai/search/LICENSE) 授權。您可以自由修改、散佈與使用於商業用途。
