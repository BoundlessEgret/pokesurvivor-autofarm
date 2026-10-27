# PokéSurvivor 自動掛機（PSBot）

替 [PokéSurvivor](https://pokesurvivor.com/) 自動走位躲招、選卡、綁羈絆、進神祕裂縫、處理各種事件，結束後自動再開一局。

> **非官方工具**，跟遊戲作者沒有關係。遊戲改版可能讓它失效，請自行斟酌使用。
> 掛機打的局**預設不會送上排行榜**（可以在設定裡關掉）。

[English below](#english)

## 安裝

### 方法一：油猴腳本（推薦，會自動更新）

油猴會定期檢查新版本並自動更新，從 Greasy Fork 或 GitHub 安裝都一樣。

1. 先安裝 [Tampermonkey](https://www.tampermonkey.net/) 或 [Violentmonkey](https://violentmonkey.github.io/)
2. 安裝腳本：
   - [Greasy Fork 頁面](https://greasyfork.org/scripts/602469)，按「安裝腳本」
   - 或直接開 [`dist/pokesurvivor-autofarm.user.js`](https://github.com/BoundlessEgret/pokesurvivor-autofarm/raw/main/dist/pokesurvivor-autofarm.user.js)，油猴會跳出安裝畫面
3. 重新整理 pokesurvivor.com，左上角會出現「PSBot 自動掛機」面板

> Chrome 新版的 Tampermonkey 需要在擴充功能的詳細資料裡打開「允許使用者指令碼」才會執行。

### 方法二：Chrome 擴充（不會自動更新）

1. 到 [Releases](https://github.com/BoundlessEgret/pokesurvivor-autofarm/releases) 下載最新的 `pokesurvivor-autofarm-v*.zip` 並解壓縮
2. Chrome 開 `chrome://extensions`，打開右上角「開發人員模式」
3. 「載入未封裝項目」→ 選剛剛解壓縮的資料夾
4. 重新整理 pokesurvivor.com

**兩種方法擇一就好**，同時裝會跑兩份。

擴充版沒辦法自動更新，但有新版本時面板上會出現「有新版本」的連結（每 6 小時最多檢查一次）。更新方法：下載新的 zip 覆蓋原本的資料夾，在 `chrome://extensions` 按重新載入，再重新整理遊戲頁。面板標題會顯示目前的版本號。

## 使用

- 在遊戲主選單先選好要出戰的寶可夢，再按面板上的 **OFF → ON**（或按 **F8**）
- 開著時會自動：開始遊戲 → 走位打怪撿經驗 → 選卡 → 結算 → 回主選單 → 再開
- 自己按方向鍵時以你的操作為準，放開就交還給 bot
- 面板可以拖曳；拖不見了按 **Shift+F8** 或標題列的 **⌂** 叫回左上角
- **遊戲分頁要保持可見**：最小化或切到背景分頁時，瀏覽器會暫停遊戲。建議把遊戲放在一個獨立的視窗

### 畢業配置

面板下方的「畢業配置」以**目前出戰的寶可夢**為準：

- 從下拉選單依序「加入」最多 4 招，順序就是**學招順序**和**羈絆順序**
- 點已加入的招式可以移除；「道具」選想要的攜帶道具
- 超夢內建一組：念力 → 變硬 → 詭計 → 精神強念，道具貝殼之鈴
- 沒設配置的寶可夢走**自動模式**：先拿 1 招適合物攻 / 特攻的輸出招，再拿對應的增益招（劍舞或詭計）、變硬，最後補第 2 招輸出

### 設定

| 選項 | 預設 | 說明 |
|---|---|---|
| 自動走位 | 開 | 關掉就只幫你選卡、選道具 |
| 自動選卡 | 開 | 見下方「選卡優先序」 |
| 自動羈絆 | 開 | 照畢業配置的順序綁 |
| 自動選攜帶道具 | 開 | 配置指定的道具 > 貝殼之鈴 > 吃剩的東西 > 先制之爪 > … |
| 主動進神祕裂縫 | 開 | 羈絆券只能靠打贏裂縫拿 |
| 自動用寶珠 | 開 | 快沒血或被包圍時用控場寶珠，首領戰用增益寶珠 |
| 結束後自動再開一局 | 開 | |
| 掛機局不上排行榜 | 開 | 想上榜就關掉 |
| 回主選單時自動買強化 | **關** | 會花金幣，見下方「養成」 |
| 回主選單時自動抽獎 | **關** | 用抽獎券，見下方「養成」 |
| 自動換最強的寶可夢出戰 | **關** | 見下方「養成」 |

## 功能

**選卡優先序**（招式進化 = 招式升到滿級 + 拿過一次指定的被動，例：念力要反應、精神強念要磁鐵）

1. 招式進化
2. 拿了就能立刻進化的強化
3. 配置裡的新招式；配置外的新招式不拿，免得佔掉欄位
4. 進化需要、但還沒拿過的被動
5. 還能進化的招式的升級
6. 其他被動（護甲沒滿 70% 前最優先；之後威力 > 反應 > 活力 > 光合作用 > 學習 > 磁鐵 > 奔跑）
7. 其他招式升級

HP 低於 35% 時文柚果最優先；三張都是爛卡而且還有重抽次數時會先重抽。

**走位**

- 躲技能：彈幕、首領招式、地面預警都用「預警落下那一刻我在哪」來預測；緊急閃避選定方向會維持一下，不會原地抽搐
- 避開障礙物和陷阱；用 A\* 尋路繞過狹縫和牆；子彈被擋住時會換射擊角度
- 前 5 分鐘專心追經驗光球；之後怪多時繞大圈遛怪，讓怪排在身後
- 卡住時自動脫困

**事件**（越前面越優先，趕不到的會直接放棄，選定後不會被半路拉走）

1. Gholdengo（十連抽券）
2. 神祕裂縫（羈絆券的唯一來源）
3. 寶可夢求救（帶到綠色標記）、喵喵（金幣）
4. 祭壇 buff、泉水回血（HP < 60%）、大寶箱
5. 撿光球

**養成（自動買強化，預設關）**：每局結束回到主選單時，替目前的夥伴花金幣買「強化」：

1. 畢業配置的第一招跟預設開局招式不同時，先買「初始招式」並把開局招式設好（例：妙蛙種子預設藤鞭，換成能量球）
2. 金幣夠 1500 時買「招式庫」，再買「第二初始招式」，設成配置裡的下一招
3. 其他強化每次挑「價值 ÷ 價格」最高的買，一直買到錢不夠（護甲、力量、反應、財運、重抽比較優先；財運、磁鐵、智慧、重抽只升到中段）

**自動抽獎（預設關）**：回主選單時把抽獎券用完（×10 券優先，普通券每 10 張抽一次）。先抽保底進度最高的地區（70 抽保底傳說），都沒進度時抽「還沒抽到的傳說最強」的地區。走遊戲自己的抽獎流程，只是跳過動畫。

**自動換最強的寶可夢出戰（預設關）**：強度看「最好的那招不用瞄準的招打多痛」，照遊戲的傷害公式算：攻擊倍率 × 物攻 / 特攻合不合 × 單屬性用同屬性招式 1.2 × 自帶天氣（例：蓋歐卡的降雨讓水系 ×1.5），再乘耐久、速度和已投資的強化。所以能力總和最高的阿爾宙斯不一定最強，蓋歐卡（2.74）和超夢（1.86）才是。強化是每隻分開的，新的要比現在的強 15% 以上才換。沒有畢業配置的寶可夢，自動強化會幫牠挑最適合掛機的開局招式。

**想養的寶可夢**：設定裡的 `favorites`（預設蓋歐卡、超夢）會讓自動抽獎優先抽牠們所在的地區（豐緣、關都），抽到後也優先出戰。蓋歐卡內建畢業配置：泡沫 → 詭計 → 水流環 → 水炮。

**神祕裂縫裡打神獸**：不遛怪，沿場地邊緣內側繞，讓神獸一直在場地對面，被貼近時先拉開距離。

**阿爾宙斯的審判（第 30 分鐘）**：阿爾宙斯打不死、會越追越快，所有傷害都按最大 HP 百分比算而且無視防禦。bot 繞場地中間的圈，讓牠留在對面，專心閃招。

## 疑難排解

- **確認版本**：面板標題會顯示版本號（例如 v1.1.0），回報問題時請附上
- **沒有出現面板**：確認只裝了一種（油猴或擴充）；油猴版請確認已允許使用者指令碼
- **其他問題**：按 F12 打開 Console，搜尋 `[PSBot]`，把訊息貼到 [Issues](https://github.com/BoundlessEgret/pokesurvivor-autofarm/issues)

設定存在瀏覽器的 `localStorage`（`psbot.v1`），只在這台電腦、這個瀏覽器裡。

## 運作方式

遊戲所有模組都掛在一個沒有暴露到 `window` 的內部物件上（`ns.Game`、`ns.Input`、`ns.RunUI`…）。
腳本在頁面載入前於 `Object.prototype` 放一個暫時的 `Game` setter，遊戲執行 `ns.Game = …` 時抓到 `ns`，然後立刻移除。之後：

- 覆寫 `ns.Input.axis()` 當虛擬搖桿：每幀取樣 16 個方向，預測位置後計算危險度，減去往目標靠近的收益，選成本最低的方向
- 包住 `ns.RunUI.showLevelUp / showBond / showItemChoice / showOver`，用遊戲自己的 `pick` / `pickBond` 選

不依賴混淆後的變數名，遊戲小改版通常不會壞。

## 開發

改 `inject.js` 時，`VERSION` 要跟 `manifest.json` 的 `version` 一起改，然後：

```sh
node build.js   # 產生 dist/pokesurvivor-autofarm.user.js 和 Release 用的 zip
```

---

## English

An unofficial auto-farm bot for [PokéSurvivor](https://pokesurvivor.com/). It handles movement and dodging, card picks, move bonds and held items. It also enters rifts, takes care of events (Gholdengo, rescues, altars, chests) and restarts runs automatically. It is not affiliated with the game's author and may break when the game updates. **Runs played by the bot are not submitted to the leaderboard by default**; you can change this in the settings.

**Install** (pick one):

- **Userscript** (updates automatically): install [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/), then install from [Greasy Fork](https://greasyfork.org/scripts/602469) or open [`dist/pokesurvivor-autofarm.user.js`](https://github.com/BoundlessEgret/pokesurvivor-autofarm/raw/main/dist/pokesurvivor-autofarm.user.js). In recent versions of Chrome, Tampermonkey needs "Allow User Scripts" turned on in the extension's details page.
- **Chrome extension** (no auto-update; the panel shows a link when a new version is out): download the zip from [Releases](https://github.com/BoundlessEgret/pokesurvivor-autofarm/releases) and unzip it. Then go to `chrome://extensions`, turn on Developer mode and choose "Load unpacked".

**Use**: choose your Pokémon in the main menu, then toggle the panel (top-left) to ON or press **F8**. **Shift+F8** brings the panel back if you drag it off-screen. Keep the game tab visible, because browsers pause background tabs.

The panel UI is in Traditional Chinese. The settings table above lists every option in order.

## License

[MIT](LICENSE)
