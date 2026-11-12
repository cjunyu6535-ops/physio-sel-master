# 🎭 社會情緒面相學大師 · 掐指一算成大師 (Physio-SEL Master v1.00)

本儲存庫為 **「社會情緒面相學 v1.00 (Physio-SEL Master)」** 跨平台 AI 技能套件，遵循開放 **Agent Skills (`SKILL.md`)** 標準，已移除特定模型與專有工具綁定，支援在 **ChatGPT Codex (Codex CLI)**、**Claude Code**、**OpenCode**、**Gemini CLI** 及 **其他 Gemini 帳號** 中直接安裝執行。

結合東方《麻衣神相》古籍智慧（三停、五官、十二宮）與西方現代 **CASEL 社會情緒學習（成人與職場應用）** 及 **FACS 微表情肌肉解剖學**，透過內建「跨裝置免代碼三步查表計分矩陣」，為使用者提供非宿命論、高賦能的成長型面相分析報告。

---

## 📂 專案目錄結構

```text
physio-sel-master/
├── SKILL.md                                  # 核心技能定義（符合 Agent Skills 開放標準）
├── README.md                                 # 專案架構與跨平台安裝教學
├── assets/
│   └── gem_prompt_spec.yaml                  # 結構化 YAML 提示詞規格檔
└── references/
    ├── traditional_physiognomy.md            # 《麻衣神相》三停、五官、十二宮與非宿命論轉譯辭典
    ├── casel_workplace_framework.md          # CASEL 五大核心素養（職場指標）、FACS 微表情與練習處方庫
    └── scoring_lookup_matrix.md              # 跨裝置免代碼「三步查表計分矩陣」（零延遲量化評估）
```

---

## 🚀 跨平台安裝指南（Codex / Claude Code / OpenCode / Gemini CLI / Gemini 帳號）

> 由於本儲存庫為 **Private（私有）**，在終端機透過指令安裝前，請先確認本機已設定好 GitHub SSH 金鑰或 `gh auth login` 登入驗證。

### 1. 使用 `npx skills` 一鍵安裝（同時支援 Codex、Claude Code、OpenCode、Gemini CLI）

```bash
# 安裝至當前專案或全域，並依提示選擇目標平台（codex / claude-code / opencode / gemini-cli）
npx skills add https://github.com/cjunyu6535-ops/physio-sel-master.git

# 或指定特定平台全域安裝範例：
npx skills add https://github.com/cjunyu6535-ops/physio-sel-master.git -g -a codex -a claude-code -a opencode
```

### 2. 手動克隆安裝至各 AI 平台指定目錄

若不使用 `npx`，可直接將本儲存庫克隆至對應工具的 Skills 目錄（資料夾名稱須保持為 `physio-sel-master`）：

| AI 平台 / 工具 | 專案層級路徑（Project Scope） | 全域層級路徑（Global Scope） | 說明 |
| :--- | :--- | :--- | :--- |
| **ChatGPT Codex (Codex CLI)** | `.agents/skills/physio-sel-master/` | `~/.agents/skills/physio-sel-master/` | 支援標準 `.agents/skills/` 發現路徑 |
| **Claude Code** | `.claude/skills/physio-sel-master/` | `~/.claude/skills/physio-sel-master/` | 放置後重啟對話即可自動辨識觸發 |
| **OpenCode** | `.opencode/skills/physio-sel-master/` | `~/.config/opencode/skills/physio-sel-master/` | 亦相容 `.claude/skills/` 與 `.agents/skills/` |
| **Gemini CLI** | `.gemini/skills/physio-sel-master/` | `~/.gemini/skills/physio-sel-master/` | 亦可使用下方專屬 CLI 指令安裝 |

**手動複製指令範例（以全域安裝至 Codex / Claude Code / OpenCode 為例）**：

```bash
# 先克隆儲存庫至本機
git clone https://github.com/cjunyu6535-ops/physio-sel-master.git

# 依需求複製到對應平台的全域技能目錄：
mkdir -p ~/.agents/skills ~/.claude/skills ~/.config/opencode/skills
cp -r physio-sel-master ~/.agents/skills/physio-sel-master          # ChatGPT Codex
cp -r physio-sel-master ~/.claude/skills/physio-sel-master          # Claude Code
cp -r physio-sel-master ~/.config/opencode/skills/physio-sel-master # OpenCode
```

### 3. Gemini CLI 專屬安裝方式

```bash
# 直接從 GitHub 安裝（預設安裝至 ~/.gemini/skills/）
gemini skills install https://github.com/cjunyu6535-ops/physio-sel-master.git

# 驗證是否安裝成功
gemini skills list --all
```

### 4. 其他 Gemini 帳號安裝方式（網頁版 Skills / 自訂 Gem）

1. **透過 Skills 管理員（Skills UI）匯入**：
   - 將本儲存庫下載為 ZIP 壓縮檔（或克隆本機 `physio-sel-master/` 資料夾）。
   - 登入目標 Gemini 帳號後，開啟左側選單或 **Skills Manager（技能管理員）**，點擊「匯入 / 上傳技能」，直接上傳整個 `physio-sel-master` 資料夾或 ZIP 壓縮檔即可。
2. **透過 Google Gems 建立**：
   - 若該 Gemini 帳號僅使用標準 Gems 介面，開啟「建立新 Gem」，將本儲存庫 `assets/gem_prompt_spec.yaml` 的規格與 `references/` 中的知識庫內容貼入「使用說明（Instructions）」即可使用。

---

## ✨ 核心功能與優化亮點

1. **跨平台無痛遷移**：移除 `allowed-tools` 專有工具宣告與特定工具函式名稱，所有檔案讀取與搜尋步驟皆以通用語意描述，確保在不同 Agent 架構下皆能正確調用 `references/` 多維知識庫。
2. **跨裝置免代碼「三步查表計分矩陣」**：不依賴外部 Python 執行環境，由模型直接根據內建查表法心算加總 CASEL 五大素養與「職場心理韌性 / 心神負荷指數」。
3. **互動式資訊補齊機制**：當使用者僅提供模糊指令時，主動引導補齊「具體面部特徵或正面清晰照」、「靜態骨骼結構 vs. 近期氣色細紋變化」及「當前職場或人際關注課題」。
4. **嚴格安全護欄與純繁體中文輸出**：落實「中文優先（不顯示多餘英文括號）」、「非宿命論（凶相轉為待發展 SEL 素養、吉相轉為可利用 SEL 優勢）」與「非醫療建議聲明」。
