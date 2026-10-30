# แบบจำลอง Durian DSL เป็น CSV

ไฟล์ในโฟลเดอร์นี้คัดลอกจาก `DSL/DurianOrchardMonitoring/DurianOrchardMonitoring.norasi` และฝาแฝดภาษาไทย `DurianOrchardMonitoringTH.norasi` ตามที่เขียนในไฟล์ ไม่มีค่าใดคำนวณหรือแก้ไข ชื่อทุกชื่อตรงกับ DSL ทุกตัวอักษร คอลัมน์ `_th` มาจากฝาแฝดภาษาไทยตามลำดับเดียวกัน

| ไฟล์ | หนึ่งแถวคือ | จำนวน |
|---|---|---|
| `UserRequirements.csv` | chain `UR-xx` ในชั้น OA พร้อม MoE | 4 |
| `SystemRequirements.csv` | chain `SR-xx` ในชั้น SA พร้อม MoP | 10 |
| `DesignPoints.csv` | chain `DP-xx` สองแถวต่อหนึ่ง DP: ชั้น LA และ chain `_Implementation` ในชั้น PA | 42 |
| `Parameters.csv` | บรรทัด `key = value` หนึ่งบรรทัด เรียงตามชั้น OA, SA, LA, PA | 287 |
| `Statements.csv` | คู่ระหว่างองค์ประกอบหนึ่งตัว (activity, function, MoE, MoP ทุกชั้น) กับข้อความหนึ่งข้อความจาก `pole.pdf` หรือ `sw.pdf` | 311 แถว, 180 องค์ประกอบ, 120 ข้อความ |

- ใน `UserRequirements.csv`, `SystemRequirements.csv` และ `DesignPoints.csv` ค่าที่เป็นรายการ (`realizes`, `steps`, `flows`, `realized_by`) คั่นด้วย `; ` และ `steps` เรียงตามลำดับใน DSL
- ชั้น OA ไม่มีพารามิเตอร์ใน DSL จึงไม่มีแถว OA ใน `Parameters.csv`
- ข้อความใน `Statements.csv` ยกมาตรงตามตัวอักษรจากข้อความของหน้า PDF ที่ระบุ (`page` คือเลขหน้าของไฟล์ PDF ใน sw.pdf คือเลขสไลด์) ข้อความหนึ่งรายการอาจรองรับหลายองค์ประกอบ และใช้ `statement_id` เดียวกัน
- องค์ประกอบ 22 ตัวไม่มีข้อความใดในสองไฟล์ PDF รองรับ แถวขององค์ประกอบเหล่านี้มีคอลัมน์ข้อความว่าง ได้แก่ ค่าใช้จ่ายรายเดือน การซ่อมและเวลาซ่อม เวลาเริ่มใช้งานสถานี การเข้ารหัสระหว่างทาง จำนวนข้อความต่อเดือนและโควตา จำนวนชุดซอฟต์แวร์ เวลาออกอากาศ รายงานตามกำหนด และการแฟลชผ่าน USB
