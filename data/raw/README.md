# ข้อมูลดิบก่อนสร้างแบบจำลอง

ข้อมูลจากเอกสารสองไฟล์เท่านั้น

| source | เอกสาร |
|---|---|
| `pole.pdf` | Tuntawisut, Kurapa & Keeratipitayanusarn (2024) การพัฒนาเสาอินเทอร์เน็ตของสรรพสิ่งสำหรับการตรวจวัดและวิเคราะห์ข้อมูลในสวนผลไม้ (`KMUTNB-Program/P2 (Pole).pdf`, 161 หน้า) |
| `sw.pdf` | สไลด์สอบป้องกันของโครงงาน Design and development of a GUI for an automated farm (Nunthasrithananon, Suyawa & Bubpha, 2024) (`KMUTNB-Program/R1/sw.pdf`, 153 สไลด์) |

## ไฟล์

| ไฟล์ | หนึ่งแถวคือ | คอลัมน์ |
|---|---|---|
| `readings.csv` | ค่าอ่านหนึ่งค่าจากการทดสอบซ้ำ | `source, page, test, run, time, device, quantity, value, unit` |
| `facts.csv` | ค่าเดี่ยวที่เอกสารระบุ เช่น ค่าวัด สเปก ค่าในโค้ด ผลสรุป ปัญหา | `id, source, page, subject, quantity, value, unit, kind` |
| `purchases.csv` | รายการจัดซื้อหนึ่งบรรทัด ของโครงงานเสา (`pole`) และโครงงาน GUI (`gui`) | `source, page, project, line, item, unit_price_thb, quantity, line_total_thb` |
| `sites.csv` | สวนที่ติดตั้งเสาหนึ่งแห่ง | `source, page, site, subdistrict, district, province, pole_to_gateway_m_approx` |

การทดสอบใน `readings.csv` (คอลัมน์ `test`)

| test | ที่มา | run |
|---|---|---|
| `battery_discharge` | pole.pdf หน้า 101-105 | แถวที่ 1-101; `time` คือเวลาที่พิมพ์ไว้ |
| `sensor_test_soil`, `_air`, `_wind`, `_light`, `_pressure`, `_float_switch` | pole.pdf หน้า 105-110 | ครั้งที่ 1-10 |
| `lora_400m`, `lora_60m` | sw.pdf สไลด์ 16-20 และ 24-28 | ครั้งที่ 1-50 |
| `calibration_*` | sw.pdf สไลด์ 99-131 | ครั้งที่ 1-5 (การทดสอบด้วยชุดตรวจดินมีครั้งเดียว) |
| `server_daily_status` | sw.pdf สไลด์ 34 | วันที่ 1-105 ตามลำดับในกราฟ |

## ข้อตกลง

- `page` คือเลขหน้าของไฟล์ PDF ใน sw.pdf เลขหน้าคือเลขสไลด์ pole.pdf ไม่มีเลขหน้าพิมพ์บนหน้า
- `unit` ว่างเมื่อเอกสารไม่ได้พิมพ์หน่วยไว้ ตารางทดสอบเซ็นเซอร์ใน pole.pdf และตารางสอบเทียบอุณหภูมิและความชื้นใน sw.pdf ไม่พิมพ์หน่วย
- `value` ส่วนใหญ่เป็นตัวเลข บางแถวเป็นข้อความตามที่พิมพ์ เช่น ระดับความชื้นในดิน `DRY+` ถึง `WET+` ช่วงค่า `920-925` และปัญหาที่รายงาน
- การทดลอง LoRa: `sent` และ `received` เป็น 1 หรือ 0 เฟรมที่หาย (400 เมตร ครั้งที่ 11 และ 38) ไม่มีแถว `rssi` และ `snr`
- `server_daily_status`: อ่านจากจุดในกราฟ ค่า 1 คือทำงาน ค่า 0 คือล่ม กราฟมีจุดค่า 0 ห้าจุด ตรงกับสไลด์ 35 ที่ระบุว่าล่ม 5 วันจาก 105 วัน `time` มีเฉพาะจุดที่แกนวันที่พิมพ์ป้ายไว้ (ทุกจุดที่สอง เริ่ม 30-Nov-67 จบ 13-Mar-68) แกนนับสองจุดจาก 28-Feb-68 ถึง 1-Mar-68 จึงมี 105 จุด ขณะที่ปฏิทินจริงช่วง 2024-11-30 ถึง 2025-03-13 มี 104 วัน
- ข้อความในไฟล์ไม่แก้ตัวสะกดของต้นฉบับ เช่น `Anternna` และ `แคล้มปป์นก`
- ไม่ใส่ชื่อสวน ชื่อเจ้าของสวน รหัสผ่าน หรือที่อยู่เซิร์ฟเวอร์
