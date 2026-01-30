# 智鐵機械財務管理系統 - CSV 匯入範本

## 檔案格式說明

所有 CSV 檔案使用 UTF-8 編碼，欄位以逗號分隔。

---

## 1. customers.csv - 客戶資料

| 欄位 | 必填 | 說明 | 範例 |
|------|------|------|------|
| code | ✓ | 客戶代碼 (唯一) | C001 |
| name | ✓ | 公司全名 | 台灣積體電路製造股份有限公司 |
| shortName |  | 簡稱 | 台積電 |

---

## 2. suppliers.csv - 供應商資料

| 欄位 | 必填 | 說明 | 範例 |
|------|------|------|------|
| code | ✓ | 供應商代碼 (唯一) | V001 |
| name | ✓ | 供應商名稱 | 永豐鋼鐵有限公司 |

---

## 3. projects.csv - 工程專案

| 欄位 | 必填 | 說明 | 範例 |
|------|------|------|------|
| code | ✓ | 專案代號 (唯一) | ZT-2024-001 |
| name | ✓ | 專案名稱 | 台積電廠房空調系統安裝工程 |
| customerCode | ✓ | 客戶代碼 | C001 |
| orderAmount | ✓ | 訂單金額 | 2850000 |
| materialCost |  | 材料費 | 680000 |
| laborCost |  | 人工費 | 520000 |
| status |  | 狀態 (ongoing/completed/closed) | ongoing |

---

## 4. ar.csv - 應收帳款

| 欄位 | 必填 | 說明 | 範例 |
|------|------|------|------|
| projectCode | ✓ | 專案代號 | ZT-2024-001 |
| customerCode | ✓ | 客戶代碼 | C001 |
| type | ✓ | 類型 (deposit/delivery/acceptance/final) | deposit |
| amount | ✓ | 應收金額 | 855000 |
| paidAmount |  | 已收金額 | 855000 |
| dueDate | ✓ | 到期日 (YYYY-MM-DD) | 2024-03-15 |

### 類型說明
- `deposit` - 訂金
- `delivery` - 進場款
- `acceptance` - 驗收款
- `final` - 尾款

---

## 5. ap.csv - 應付帳款

| 欄位 | 必填 | 說明 | 範例 |
|------|------|------|------|
| projectCode |  | 專案代號 | ZT-2024-001 |
| vendorCode | ✓ | 供應商代碼 | V001 |
| paymentType | ✓ | 付款方式 (CHECK/TRANSFER/CASH) | CHECK |
| amount | ✓ | 金額 | 350000 |
| dueDate | ✓ | 到期日 (YYYY-MM-DD) | 2024-04-30 |
| status |  | 狀態 (pending/paid) | pending |

### 付款方式說明
- `CHECK` - 支票
- `TRANSFER` - 匯款
- `CASH` - 現金

---

## 6. commissions.csv - 佣金記錄

| 欄位 | 必填 | 說明 | 範例 |
|------|------|------|------|
| projectCode | ✓ | 專案代號 | ZT-2024-001 |
| type | ✓ | 類型 (agent/referral/rebate) | agent |
| amount | ✓ | 金額 | 142500 |
| description |  | 說明 | 業務代理佣金 5% |
| date |  | 日期 (YYYY-MM-DD) | 2024-03-20 |

### 佣金類型說明
- `agent` - 代理佣金
- `referral` - 轉介佣金
- `rebate` - 回扣

---

## 匯入順序建議

1. customers.csv (客戶)
2. suppliers.csv (供應商)
3. projects.csv (專案) - 需要先有客戶資料
4. ar.csv (應收帳款) - 需要先有專案和客戶資料
5. ap.csv (應付帳款) - 需要先有專案和供應商資料
6. commissions.csv (佣金) - 需要先有專案資料

---

## 注意事項

1. **編碼**：請確保 CSV 檔案使用 UTF-8 編碼
2. **重複資料**：系統會跳過已存在的代碼（客戶、供應商、專案）
3. **關聯資料**：如果找不到對應的專案/客戶/供應商代碼，該筆資料將被跳過
4. **日期格式**：請使用 `YYYY-MM-DD` 格式
5. **金額**：請輸入數字，不要包含貨幣符號或千分位
