
การค้นหาสถานที่ใช้ Google Places, การคำนวณเส้นทางจริงยังใช้ Google Directions Service แบบ `TravelMode.TRANSIT`, และหน้าแผนที่ภาพรวมยังใช้ข้อมูลจาก `src/transit-overview-data.js`

src/main.js                       จุดเริ่มต้นของแอป เรียก setup หลักทั้งหมด
src/core/app-state.js             state กลาง, ข้อความภาษาไทย/อังกฤษ, ค่าคงที่ของระบบ
src/core/dom.js                   helper สำหรับเลือก element
src/core/utils.js                 helper สำหรับ format, escape HTML, icon
src/maps/map-style.js             dark style ของ Google Map
src/maps/map-service.js           สร้าง map, mini map, directions renderer, reset route visualization
src/maps/places-service.js        Google Places Autocomplete และ normalize place
src/maps/overview-layer.js        เลเยอร์ภาพรวมขนส่งสาธารณะ รถไฟฟ้า รถเมล์ เรือ
src/routing/google-transit-service.js  เรียก Google Directions Transit
src/routing/route-summary.js      สรุปเวลา ระยะทาง เดินเท้า ค่าโดยสาร และ steps
src/routing/preferences.js        จัดอันดับผลลัพธ์ตาม shortest / cheapest / least walk
src/routing/route-renderer.js     สร้าง route cards, เลือก route, อัปเดตแผนที่
src/location/current-location.js  ใช้ตำแหน่งปัจจุบันและตรวจขอบเขตกรุงเทพฯ
src/storage/favorites.js          บันทึกและแสดงเส้นทางโปรดใน localStorage
src/ui/events.js                  รวม event listeners หลักของหน้า route และ settings
src/ui/language.js                เปลี่ยนภาษาและ placeholder
src/ui/navigation.js              เปลี่ยนแท็บล่างและ resize map
src/ui/profile.js                 โปรไฟล์, แก้ชื่อ, logout
src/ui/messages.js                แสดงข้อความผลลัพธ์และ API status

### หลักการดูแลโค้ดหลังแยกไฟล์

- ต้องการแก้การเรียก Google Transit: แก้ที่ `src/routing/google-transit-service.js`
- ต้องการแก้การจัดอันดับ shortest / cheapest / least walk: แก้ที่ `src/routing/preferences.js`
- ต้องการแก้การ์ดผลลัพธ์: แก้ที่ `src/routing/route-renderer.js`
- ต้องการแก้การสรุปค่าโดยสาร/เวลา/ระยะเดิน: แก้ที่ `src/routing/route-summary.js`
- ต้องการเพิ่มสถานีหรือเส้นทางภาพรวม: แก้ที่ `src/transit-overview-data.js`
- ต้องการแก้แผนที่ภาพรวม: แก้ที่ `src/maps/overview-layer.js`
- ต้องการแก้ปุ่มตำแหน่งปัจจุบัน: แก้ที่ `src/location/current-location.js`

`src/main.js` เป็นตัวประกอบระบบ ไม่นำ logic จำนวนมากกลับไปใส่ในไฟล์นี้เพื่อให้โปรเจกต์ดูแลต่อได้ง่ายขึ้น
