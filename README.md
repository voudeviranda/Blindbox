# Blind Box Pastel - Phiên bản chuẩn
Hướng dẫn triển khai web Blind Box public + lưu kết quả Google Sheet.

## 1. Chuẩn bị Google Sheet
- Tạo Sheet mới với 3 cột: Timestamp | Facebook Name | Result
- Copy ID Sheet từ URL: https://docs.google.com/spreadsheets/d/<YOUR_SHEET_ID>/edit#gid=0

## 2. Tạo Google Apps Script
- Trong Sheet → Extensions → Apps Script → New Project
- Dán code dưới đây:
```javascript
function doPost(e) {
  try {
    var ss = SpreadsheetApp.openById('YOUR_SHEET_ID');
    var sheet = ss.getSheetByName('Sheet1');
    var data = JSON.parse(e.postData.contents);
    sheet.appendRow([new Date(), data.fbName, data.result]);
    return ContentService.createTextOutput(JSON.stringify({status:'success'})).setMimeType(ContentService.MimeType.JSON);
  } catch(err) {
    return ContentService.createTextOutput(JSON.stringify({status:'error', message: err})).setMimeType(ContentService.MimeType.JSON);
  }
}
```

## 3. Triển khai Web App
- Deploy → New Deployment → Web App
- Execute as: Me
- Who has access: Anyone
- Copy URL Web App

## 4. Chỉnh file HTML
- Mở `index.html`
- Thay `YOUR_WEB_APP_URL` bằng Web App URL vừa copy

## 5. Upload GitHub Pages
- Tạo repo → upload `index.html` + `README.md`
- Settings → Pages → Source: main branch / root → Save
- Link web: https://<username>.github.io/<repo-name>/
