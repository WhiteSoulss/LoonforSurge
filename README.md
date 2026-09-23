# LoonforSurge

將 [可莉插件中心](https://hub.kelee.one/) 的 Loon 插件整理為 Surge 可讀取的靜態檔案。這是非官方轉換，並非原作者或 Surge 官方發布；請遵守原作者授權及使用條款。原站明確說明插件為 Loon 專用、不建議轉換至其他工具，因此檔案格式轉換成功不等於功能已在 Surge 驗證。

## 目前進度（2026-09-23）

以插件中心的 [`list.json`](https://hub.kelee.one/list.json) 共 275 項為基準：

| 類別 | 數量 | 說明 |
| --- | ---: | --- |
| `modules/*.sgmodule` | 270 | 以 Script-Hub 自動轉換，僅完成靜態格式檢查 |
| `modules/*.sgmodule` | 2 | Loon 手動執行腳本改寫為 Surge `generic` 語法，**實驗性** |
| `rulesets/*.list` | 1 | DNS 防泄露插件，須在主設定檔指定自己的代理策略 |
| 尚未收錄 | 2 | 公開鏡像缺少原始 `.lpx`，未虛構內容 |

完整清單及每項原始連結、鏡像版本、轉換狀態見 [`manifest.json`](manifest.json)。

尚未收錄：`ShoujiDesk_remove_ads.lpx`（口袋壁紙去廣告）、`ShandongSchool_remove_ads.lpx`（閃動校園去廣告）。這兩項在本次檢查時無法從原站直接取得，所用公開鏡像亦未收錄。

## 使用

在 Surge 的模組介面加入所需檔案的 Raw URL，例如：

```text
https://raw.githubusercontent.com/WhiteSoulss/LoonforSurge/main/modules/BaiduWenku_remove_ads.sgmodule
```

DNS 防泄露不是模組。請在自己的 Surge **主設定檔** `[Rule]` 中指定實際存在的代理或策略組名稱，例如：

```ini
RULE-SET,https://raw.githubusercontent.com/WhiteSoulss/LoonforSurge/main/rulesets/Prevent_DNS_Leaks.list,MyProxy
```

將 `MyProxy` 換成你設定檔中的策略名稱。Surge 模組的規則只能使用內建策略，不能直接承接原插件的 `PROXY` 指派，因此沒有產生空的 `.sgmodule` 冒充完整轉換。

`NodeLinkCheck.sgmodule` 與 `Node_detection_tool.sgmodule` 為實驗性檔案：Surge 支援 `generic` 腳本語法，但原始 JavaScript 可能依賴 Loon 專用 API；未驗證前請勿預期其功能正常。

請逐一啟用、測試。需要 HTTPS 解密的插件還須在 Surge 正確設定 MITM；轉換後的模組仍可能引用原作者或 Script-Hub 的遠端 JavaScript，而非把腳本本體打包到本倉庫。若原始腳本無法下載、API 不相容或目標 App 改版，模組也可能無法工作。

## 來源與轉換方法

- 插件目錄：[可莉插件中心](https://hub.kelee.one/list.json)
- `.lpx` 快照：[Qmxn/Tools](https://github.com/Qmxn/Tools/tree/f849c3730ed760b36d4b79d1d793c5e8176d8a87/Plugin)，固定提交 `f849c3730ed760b36d4b79d1d793c5e8176d8a87`
- 自動轉換器：[Script-Hub](https://github.com/Script-Hub-Org/Script-Hub/tree/6b4fb62240629d2fc66b08bc271f8c1f83a5dcd1)，固定提交 `6b4fb62240629d2fc66b08bc271f8c1f83a5dcd1`

每個輸出檔案的開頭均保留原始 `.lpx` 連結、鏡像位置及轉換來源；原插件的作者等中繼資料也予以保留。本倉庫不代表原作者背書。
