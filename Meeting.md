## 1. Dịch vụ VPS, Cloud & chi phí

**1.1. Dịch vụ VPS**

* Bên CSC hiện đang cung cấp:

  * Những **loại VPS nào** (cấu hình/gói chuẩn)?
  * Sử dụng hạ tầng / nhà cung cấp nào (tự build, hay dùng hạ tầng của cloud provider nào khác)?
* Xin:

  * **Thông tin chi tiết từng gói VPS**: CPU, RAM, storage, băng thông, datacenter.
  * **Bảng giá** và chính sách chiết khấu theo tháng / 6 tháng / 12 tháng.

**1.2. Dịch vụ Cloud Database**

* Hiện CSC có dịch vụ **Managed DB / Cloud DB** nào?

  * Đặc biệt hỏi rõ:

    * Có sẵn dịch vụ cho **PostgreSQL** không?
    * Có hỗ trợ **TimescaleDB** (trên nền PostgreSQL) không?
* Cách họ vận hành:

  * Backup, monitoring, failover, scale cho DB như thế nào?
  * Giá theo dung lượng / theo instance / theo số kết nối?

**1.3. Dịch vụ S3 / Object Storage**

* Các dịch vụ **S3-compatible** mà CSC đang cung cấp là gì?

  * Nhà cung cấp / nền tảng (vd: S3 riêng, Ceph, Cloudian, CLF… – nhờ họ liệt kê).
* Hỏi:

  * Cách tính giá theo dung lượng + băng thông.
  * Độ bền (durability), versioning, lifecycle rule (tự động chuyển tier, xóa file cũ).

---

## 2. Dịch vụ lưu trữ file cho doanh nghiệp

* CSC có dịch vụ **lưu trữ file, chia sẻ dữ liệu doanh nghiệp** tương tự Google Drive/Workspace không?

  * Tính năng:

    * Quản trị người dùng, phân quyền thư mục/file.
    * Đồng bộ desktop/mobile, chia sẻ link nội bộ/ngoài.
    * Log truy cập, audit.
* Giao diện quản trị:

  * Có **portal / web admin** dễ dùng cho admin doanh nghiệp không?
* Giá:

  * Tính theo **số user**, dung lượng, hay theo gói?

---

## 3. Bảo mật, quản trị & SLA

**3.1. Bảo mật hạ tầng**

* Các giải pháp bảo mật sẵn có:

  * **Firewall** (L3/L4, WAF cho web không?).
  * **VPN** để truy cập vào server nội bộ (site-to-site, client VPN).
  * Anti-DDoS, giới hạn IP, 2FA cho panel quản trị.
* Hỏi thêm:

  * Có gói “**bảo vệ server**” trọn gói không (rule firewall, hardening, giám sát bất thường)?

**3.2. Trang quản trị**

* CSC có cung cấp **trang quản trị tập trung** không:

  * Quản lý VPS, DB, storage, S3, firewall, VPN… từ một portal?
  * Theo dõi resource (CPU/RAM/disk), log cơ bản.
* API/CLI:

  * Có API/SDK cho phép tự động hóa (tự tạo server, scale, backup) không?

**3.3. SLA & hỗ trợ**

* **SLA cam kết**:

  * Uptime bao nhiêu % cho: VPS, DB Cloud, Storage, S3?
  * Nếu vi phạm SLA thì **bồi thường** như thế nào (credit, giảm phí, hoàn tiền)?
* Hỗ trợ:

  * Kênh support (ticket, email, hotline, Zalo).
  * Thời gian phản hồi và xử lý sự cố (P1/P2/P3).

---

## 4. Backup & Restore

* **Cơ chế backup**:

  * Backup những gì: VPS (snapshot), DB (logical/physical), file/S3?
  * **Tần suất**: theo giờ, theo ngày, theo tuần?
  * **Thời gian lưu**: 7/30/90 ngày?
  * Backup lưu ở **cùng DC hay khác DC** (offsite)?

* **Restore**:

  * Khi cần restore:

    * Thời gian khôi phục (RTO).
    * Mất tối đa bao nhiêu dữ liệu (RPO).
  * Có **tính phí riêng cho việc restore** không?
  * Có hỗ trợ **test restore định kỳ** để đảm bảo backup dùng được?

---

## 5. Tech stack & yêu cầu kỹ thuật

**5.1. Tech stack chính**

* Hệ thống sử dụng:

  * **Backend**: Laravel
  * **Frontend**: VueJS
  * **Database**: PostgreSQL, TimescaleDB, MySQL
* Hỏi:

  * Hạ tầng đề xuất (VPS/Cloud/Managed DB) tối ưu cho **Laravel + VueJS + PG/Timescale + MySQL**.
  * Có nên tách **app server** và **DB server**? Nên tách theo dịch vụ (PG/Timescale riêng, MySQL riêng) không?

**5.2. Nhu cầu đặc biệt cho database**

* Yêu cầu:

  * **Dung lượng lớn**, tăng trưởng theo thời gian (log/time-series cho TimescaleDB).
  * **Uptime cao**, cần hạn chế downtime tối đa.
  * Có **backup định kỳ** + **cơ chế failover** (master–standby, cluster…).
* Cần làm rõ:

  * Các phương án **HA/failover** họ cung cấp cho Postgres/Timescale.
  * Tần suất backup cho DB, giữ bao lâu, restore tới thời điểm nào được (point-in-time recovery?).
  * Giám sát CPU, RAM, I/O, connection cho DB.

**5.3. Vấn đề DB hay bị treo / CPU cao**

* Mô tả: trước đây DB thường bị **treo** và phải **restart** khi CPU cao.
* Hỏi họ:

  * Hạ tầng + monitoring nào giúp tránh tình trạng này?

    * Alert khi CPU cao / connection quá nhiều.
    * Giải pháp scale (tăng tài nguyên, tách read/write, connection pool…).
  * Có dịch vụ **tư vấn tuning DB** / managed DB không?

---

## 6. Chi phí theo từng phương án

* Yêu cầu CSC:

  * Đưa **nhiều phương án**:

    1. Phương án tối thiểu (chi phí thấp).
    2. Phương án khuyến nghị (cân bằng chi phí/ổn định).
    3. Phương án cao cấp (HA/failover đầy đủ).
  * Mỗi phương án ghi rõ:

    * Cấu hình VPS/DB/S3/File service.
    * SLA, backup, bảo mật đi kèm.
    * **Tổng chi phí/tháng** và chiết khấu nếu trả 6–12 tháng.