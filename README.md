# Dashboard ยอดส่งออกทุเรียนแช่แข็ง

Dashboard นี้ติดตามยอดส่งออกไทยของสินค้า:

- สินค้า: ทุเรียนแช่แข็ง
- HS Code: `08119000002`
- ชื่อจาก MOC lookup: `08119000002 : ทุเรียน แช่เย็นจนแข็ง`
- HS version: `2022`
- Source: Thailand Trade Report, Ministry of Commerce
- Report page: https://tradereport.moc.go.th/th/stat/reporthscodeexport01
- Endpoint: `https://tradereport.moc.go.th/stat/reporthscodeexport01/result`

## Coverage

- ช่วงข้อมูล: `2021-01` ถึง `2026-05`
- เดือนล่าสุดตาม source: พ.ค. 2569
- สกุลเงิน: บาท
- Grain หลัก: รายเดือน x ประเทศ

## Validation

ตรวจ reconciliation จาก MOC world summary row เทียบกับผลรวมรายประเทศทุกเดือน:

- จำนวนเดือนที่ดึง: `65`
- จำนวนรายประเทศ: `1,190` rows
- Max absolute value diff: `0.0`
- Max absolute quantity diff: `0.0`
- ประเทศที่ map ทวีปไม่ได้: ไม่มี

ไฟล์ validation อยู่ที่ `data/validation_reconciliation.csv`

## Dashboard Features

- KPI เดือนล่าสุด, MoM, YoY, YTD
- Filter รายเดือน / รายไตรมาส / รายปี
- มุมมองรวมทุกประเทศ / รายประเทศ / รายทวีป
- Metric มูลค่า / ปริมาณ
- Growth MoM / YoY / QoQ ตาม period
- Interactive line chart พร้อมจุดที่คลิก/กด keyboard ได้
- Detail panel ใต้กราฟ
- ตาราง sortable และ export CSV ตาม filter ปัจจุบัน
- Responsive desktop/mobile

## Files

- `index.html` - dashboard page
- `styles.css` - dashboard styles
- `app.js` - interaction, chart, table, export logic
- `data.js` - embedded dataset for static hosting
- `data/dataset.json` - full dataset
- `data/monthly_country_hs08119000002.csv` - monthly country rows
- `data/monthly_continent_hs08119000002.csv` - monthly continent rows
- `data/monthly_total_hs08119000002.csv` - monthly world total rows
- `data/validation_reconciliation.csv` - reconciliation check
- `scripts/fetch_moc_hs08119000002.py` - reproducible data fetcher
- `dashboard-desktop-smoke.png` - desktop QA screenshot
- `dashboard-mobile-smoke.png` - mobile QA screenshot

## Local Run

```powershell
python -m http.server 8781 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:8781/
```

## QA Run

Checks performed before publish:

- `node --check app.js`
- `curl http://127.0.0.1:8781/`
- `curl http://127.0.0.1:8781/data.js`
- Headless Edge screenshots for desktop and mobile
- Verified chart point accessibility markers in `app.js`
