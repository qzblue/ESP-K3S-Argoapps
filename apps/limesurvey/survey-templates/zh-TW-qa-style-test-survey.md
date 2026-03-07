# LimeSurvey 繁體中文測試問卷（含圖片、附件、樣式）

## 問卷基本設定

- 問卷標題：`ESP 平台功能與體驗測試問卷（繁體）`
- 問卷語言：`繁體中文（zh-Hant-TW）`
- 問卷簡介：

```html
<div style="padding:16px;border:1px solid #d8e4f0;border-radius:10px;background:#f7fbff;">
  <h2 style="margin-top:0;color:#0F4C81;">歡迎參與 ESP 測試問卷</h2>
  <p>此問卷用於驗證 LimeSurvey 在繁體中文環境下的題型、圖片、檔案上傳、矩陣量表與樣式顯示。</p>
  <img src="https://images.unsplash.com/photo-1461749280684-dccba630e2f6?w=1200" alt="測試主圖" style="max-width:100%;border-radius:8px;" />
</div>
```

## 題組 A：受測者基本資料

1. 題型：短文字（必填）  
   題目：`請輸入您的暱稱`

2. 題型：單選  
   題目：`您的身份最接近下列哪一項？`  
   選項：
   - 學生
   - 教師
   - 行政人員
   - 其他

3. 題型：日期  
   題目：`您首次使用 ESP 問卷系統的日期為？`

## 題組 B：介面與樣式測試

4. 題型：顯示文字（Description）  
   內容：

```html
<div style="padding:12px 14px;background:linear-gradient(120deg,#e6f3ff,#f8fbff);border-radius:10px;border:1px solid #d6e8f8;">
  <strong style="color:#0F4C81;">樣式區塊測試：</strong>
  <ul>
    <li>字體渲染</li>
    <li>色彩顯示</li>
    <li>圖片縮放與響應式排版</li>
  </ul>
  <img src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=1000" alt="樣式測試圖片" style="max-width:100%;margin-top:8px;border-radius:8px;" />
</div>
```

5. 題型：5 分量表（Array / Likert）  
   題目：`請評估以下項目`  
   子題：
   - 首頁美觀程度
   - 文字可讀性
   - 操作直覺性
   - 手機瀏覽體驗
   列標：
   - 非常不滿意
   - 不滿意
   - 普通
   - 滿意
   - 非常滿意

6. 題型：長文字  
   題目：`請描述您最喜歡目前介面的哪個部分？`

## 題組 C：功能測試

7. 題型：多選  
   題目：`您已測試過哪些功能？`  
   選項：
   - 建立問卷
   - 匯入題目
   - 匯出回覆
   - 權限管理
   - 主題設定

8. 題型：排序（Ranking）  
   題目：`請依您認為的重要程度排序以下功能`  
   選項：
   - 穩定性
   - 視覺設計
   - 匯出報表
   - 題型豐富度
   - 多語言支援

9. 題型：數值輸入  
   題目：`若滿分 100 分，您會給目前系統幾分？`  
   驗證：最小 `0`，最大 `100`

## 題組 D：圖片與附件

10. 題型：檔案上傳（File upload）  
    題目：`請上傳一張截圖或文件，作為測試附件`  
    限制建議：
    - 允許格式：`jpg,png,pdf`
    - 單檔上限：`5MB`
    - 最多檔案數：`3`

11. 題型：是/否  
    題目：`您是否成功上傳附件？`

12. 題型：長文字（條件題）  
    題目：`若上傳失敗，請描述錯誤訊息`  
    顯示條件：第 11 題 = 否

## 題組 E：結尾

13. 題型：單選（Net Promoter Score 可替代）  
    題目：`您是否願意向同事推薦此系統？`  
    選項：
    - 非常願意
    - 願意
    - 普通
    - 不願意
    - 非常不願意

14. 題型：長文字  
    題目：`其他建議或問題回報`

## 佈景主題附加 CSS（可貼到 Theme Options > Custom CSS）

```css
:root {
  --esp-primary: #0F4C81;
  --esp-accent: #39A0ED;
}

.survey-name, .group-title {
  color: var(--esp-primary);
  font-weight: 700;
}

.btn-primary {
  background-color: var(--esp-primary);
  border-color: var(--esp-primary);
}

.btn-primary:hover {
  background-color: #0B3A61;
  border-color: #0B3A61;
}

.question-container {
  border-radius: 10px;
  border: 1px solid #e3edf7;
  padding: 14px;
  margin-bottom: 14px;
  background: #fff;
}
```

## 快速建立建議

1. 先建立新問卷，語言選繁體中文。
2. 依上方題組建立 5 個 Question Group（A~E）。
3. 先建立第 4 題與第 10 題，測試圖片渲染與附件上傳路徑是否正常。
4. 最後加上第 12 題的條件邏輯（第 11 題 = 否）。
