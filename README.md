# LEGO Model Production — Timesheet & Workforce Analytics

[English](#english) | [Tiếng Việt](#tiếng-việt)

---

## English

### 1. Project Overview
An end-to-end workforce, project costing, and timesheet governance analytics solution built for **LEGO Model Production**. The project evaluates operational efficiency across three manufacturing locations (**PRC, Mexico, and Germany**) from **January 2024 to September 2025**, alongside a **Q4 2025 capacity forecast** modeled on LEGO's **5-4-4 accounting calendar**.

* **Author:** Nguyễn Đông Trường — Data Analyst
* **Contact:** truong10042004.work@gmail.com
* **Deliverables:** Interactive Power BI Dashboard (`.pbix`), Executive Presentation (`.pdf`), ETL Pipeline Scripts (`.py`), and Data Dictionary.

---

### 2. Business Context & Dataset Scale
To support resource allocation and cost control, this analysis processes raw timesheet logs combined with employee rate cards and country contract standards:

| Metric | Value | Details |
| :--- | :--- | :--- |
| **Timesheet Records** | `103,961` | Cleaned and standardized entries (`01/01/2024 – 27/09/2025`) |
| **Active Workforce** | `202` | Distributed across 6 Resource Groups (`Build`, `Design`, `PM`, `Tech`, `Overheads`, `Concept`) |
| **Projects Tracked** | `127` | Production and internal overhead projects across `PRC`, `Mexico`, and `Germany` |
| **Accounting Calendar** | `5-4-4` | 5-week periods in Jan, Apr, Jul, Oct; Sunday–Saturday workweek; Monday approval SLA |
| **Total Logged Hours** | `429,854.4 hrs` | `298,336.0 hrs` Billable (`69.4%`) vs. `131,518.4 hrs` Non-billable (`30.6%`) |
| **Total Labor Cost** | `$12.41M` | Calculated via resource group hourly rates (`$25/hr` to `$40/hr`) |

---

### 3. Tech Stack & Architecture
1. **Data Cleaning & ETL (`Python - Pandas`):**
   * Handled missing values, standardized `Duration` strings into decimal hours, enforced strict schema types, and loaded cleaned fact/dimension tables into **Google BigQuery**.
2. **Data Warehousing (`SQL / Google BigQuery`):**
   * Structured a Star Schema linking `fact_timesheets` with `dim_resource_rate`, `dim_country_contract`, and a custom calendar dimension.
3. **Data Modeling & Analytics (`Power BI & DAX`):**
   * Built a custom **5-4-4 Fiscal Calendar (`DimDate`)** in DAX to align weekly cutoffs and period-over-period comparisons.
   * Created dynamic DAX measures for *Productive Utilisation (Logged vs. Contractual Capacity)*, *Weekly Overtime Allocation*, *SLA Late Approvals*, *Proxy Approvals*, and *Seasonal Q4 2025 Forecasting*.

---

### 4. Dashboard Structure
The Power BI report is organized into a modular brick-style **Table of Contents**, **3 Core Analytical Modules**, an **Executive Insights** summary page, and **4 Contextual Tooltips**:

* **Page 1 — Table of Contents:** Interactive navigation hub outlining the 4 core business questions answered by the report.
* **Page 2 — Utilisation & Forecast:** Tracks Productive Utilisation by Resource Group, Country, and Period; analyzes individual employee outliers; breaks down overtime peaks; and forecasts Q4 2025 hours.
* **Page 3 — Costing & Financials:** Evaluates Billable vs. Non-billable cost shares, project-level cost drivers (`LMP00001503` vs. `LMP00001501`), and activity-level non-billable spending.
* **Page 4 — Timesheet Governance:** Monitors weekly approval rates, unapproved billable hours, post-Monday late approvals, timesheet amendments, proxy approvals, and YoY sick leave trends.
* **Page 5 — Executive Insights:** Synthesizes findings into a structured **Data $\rightarrow$ Problem $\rightarrow$ Action Plan** framework.
* **Pages 6–9 — Hover Tooltips:** Hidden drill-down views for KPI Glossary, Employee Details, Activity Breakdown, and Group Approval Rates.

---

### 5. Key Findings & Actionable Recommendations

#### A. Workforce Utilisation & Q4 Forecast
* **Finding:** Overall Productive Utilisation stands at **69.4%**, led by **Build (73.3%)** and **Mexico (74.1%)**. However, utilisation dropped from **73.8% (FY2024)** to **61.5% (FY2025)**—bottoming out at **45.1% in August 2025**—as active headcount contracted to ~80–90 employees while non-billable hours rose by **+9.4%**. Q4 2025 utilisation is projected to peak in **November (58.9%)** before dipping to **40.6% in December** due to year-end holidays.
* **Action:** Reallocate bench capacity from Q2–Q3 2025 into active billable projects, and separate full-time `Leadership` personnel from technical production groups to ensure accurate utilisation tracking.

#### B. Project Cost Concentration & Overtime Pressure
* **Finding:** Flagship project **`LMP00001503`** accounts for **55.5% of total billable hours** and **$4.72M (38.0% of total cost)** with a **99.8% utilisation rate**. However, it also drives **50.2% of company-wide overtime** (`7,625 hrs` out of `15,200 hrs` total), placing heavy workload pressure on the **Build** team (`58.4%` of all overtime, peaking in March 2025).
* **Action:** Pre-allocate cross-trained Build capacity ahead of peak production milestones on `LMP00001503` to curb overtime costs (`$448.8K` total) and close dormant 1-hour project codes.

#### C. Non-Billable Cost Optimization
* **Finding:** Non-billable activities cost **$3.88M (31.3% of total labor spend)**, with **99.8%** logged under internal code **`LMP00001501`** (`4.3%` PU). **Meetings** represent the single largest non-billable expense at **$1.28M** (exceeding Annual Leave at `$1.25M`), driven by high-rate groups (`PM` at `$40/hr`, `Tech` at `$37/hr`) and isolated production staff logging up to `70%` of their hours in meetings.
* **Action:** Audit and restructure `LMP00001501` deliverables, cap weekly recurring meetings for high-rate groups, and introduce dedicated "No-Meeting Blocks" for Build teams.

#### D. Timesheet Governance & Compliance
* **Finding:** While overall approval compliance is **98.1%**, **19.4% of approved records (`19,786` entries)** missed the Monday deadline—with the **PM group** acting as the primary bottleneck (**56.5% late**). Furthermore, **proxy approvals** (`Approved_By` $\neq$ `Time_Approver`) surged to **40.3% in June 2025**, most frequently occurring in **Tech (28.5%)** and **Overheads (25.8%)**.
* **Action:** Deploy automated approval reminders every Monday morning (prioritizing PMs) and update designated approver mappings in the system for Tech and Overheads.

---

### 6. Repository Structure
```text
├── data_pipeline/          # Python scripts for data cleaning and BigQuery ingestion
├── powerbi/                # Power BI dashboard file (.pbix) and DAX measure documentation
├── presentation/           # Executive slide deck (LEGO Analysis Presentation.pdf)
└── README.md               # Project documentation (English & Vietnamese)
```

---
---

## Tiếng Việt

### 1. Tổng Quan Dự Án
Giải pháp phân tích dữ liệu toàn diện về hiệu suất nguồn lực, chi phí dự án và quản trị quy trình chấm công dành cho **LEGO Model Production**. Dự án đánh giá hiệu quả vận hành tại 3 nhà máy (**PRC, Mexico và Germany**) từ **tháng 01/2024 đến tháng 09/2025**, kết hợp **mô hình dự báo công suất Quý 4/2025** theo **lịch kế toán 5-4-4** đặc thù của LEGO.

* **Người thực hiện:** Nguyễn Đông Trường — Data Analyst
* **Liên hệ:** truong10042004.work@gmail.com
* **Sản phẩm bàn giao:** Dashboard tương tác Power BI (`.pbix`), Tài liệu thuyết trình (`.pdf`), Mã nguồn xử lý dữ liệu (`.py`) và Từ điển chỉ số (Data Dictionary).

---

### 2. Bối Cảnh Nghiệp Vụ & Quy Mô Dữ Liệu
Dự án kết hợp dữ liệu nhật ký chấm công (Timesheets) với bảng đơn giá nhân sự và định mức giờ hợp đồng theo từng quốc gia:

| Chỉ số | Giá trị | Chi tiết |
| :--- | :--- | :--- |
| **Bản ghi Timesheet** | `103,961` | Dữ liệu đã làm sạch và chuẩn hóa (`01/01/2024 – 27/09/2025`) |
| **Quy mô nhân sự** | `202` | Phân bổ tại 6 nhóm chuyên môn (`Build`, `Design`, `PM`, `Tech`, `Overheads`, `Concept`) |
| **Số lượng dự án** | `127` | Các dự án sản xuất mô hình và mã vận hành nội bộ tại `PRC`, `Mexico`, `Germany` |
| **Lịch kế toán** | `5-4-4` | Các tháng 1, 4, 7, 10 dài 5 tuần; tuần làm việc từ Chủ nhật – Thứ Bảy; hạn duyệt vào Thứ Hai |
| **Tổng giờ ghi nhận** | `429,854.4 giờ` | `298,336.0 giờ` Billable (`69.4%`) và `131,518.4 giờ` Non-billable (`30.6%`) |
| **Tổng chi phí nhân công** | `$12.41M` | Tính theo đơn giá giờ chuẩn của từng nhóm nguồn lực (`$25/giờ` – `$40/giờ`) |

---

### 3. Công Nghệ & Kiến Trúc Xử Lý
1. **Làm sạch & Nạp dữ liệu (`Python - Pandas`):**
   * Xử lý giá trị khuyết thiếu, chuyển đổi định dạng giờ làm việc (`Duration`) sang số thập phân, chuẩn hóa kiểu dữ liệu và đẩy lên **Google BigQuery**.
2. **Lưu trữ dữ liệu (`SQL / Google BigQuery`):**
   * Tổ chức mô hình lược đồ hình sao (Star Schema) kết nối bảng dữ liệu chính `fact_timesheets` với các bảng danh mục `dim_resource_rate`, `dim_country_contract` và bảng lịch.
3. **Mô hình hóa & Trực quan hóa (`Power BI & DAX`):**
   * Xây dựng bảng **Lịch kế toán 5-4-4 (`DimDate`)** bằng DAX để đồng bộ chu kỳ tuần và so sánh cùng kỳ.
   * Viết hệ thống hàm DAX tính toán *Productive Utilisation (theo giờ thực tế & giờ hợp đồng)*, *Phân bổ Overtime theo tuần*, *Tỷ lệ phê duyệt trễ hạn*, *Phê duyệt thay thế (Proxy Approval)* và *Dự báo Q4/2025*.

---

### 4. Cấu Trúc Dashboard Power BI
Báo cáo được thiết kế theo bố cục mô-đun nhận diện của LEGO, gồm **Trang Mục Lục**, **3 Phân Hệ Phân Tích Chính**, **Trang Tổng Hợp Giải Pháp** và **4 Trang Tooltip Bổ Trợ**:

* **Trang 1 — Table of Contents:** Trang điều hướng trực quan tóm tắt 4 câu hỏi nghiệp vụ trọng tâm của báo cáo.
* **Trang 2 — Utilisation & Forecast:** Theo dõi hiệu suất sử dụng thời gian theo nhóm nguồn lực, quốc gia và giai đoạn; phân tích biến động cấp nhân viên; chi tiết giờ làm thêm (Overtime) và dự báo Q4/2025.
* **Trang 3 — Costing & Financials:** Phân tích cơ cấu chi phí Billable và Non-billable, các yếu tố cấu thành chi phí dự án trọng điểm (`LMP00001503` so với `LMP00001501`) và chi phí theo từng loại hoạt động.
* **Trang 4 — Timesheet Governance:** Giám sát tỷ lệ phê duyệt hàng tuần, giờ Billable chưa duyệt, tỷ lệ duyệt trễ sau Thứ Hai, chỉnh sửa phiếu chấm công, duyệt thay thế và xu hướng nghỉ ốm qua các năm.
* **Trang 5 — Executive Insights:** Tổng hợp toàn bộ phát hiện theo cấu trúc **Số liệu $\rightarrow$ Vấn đề $\rightarrow$ Action**.
* **Trang 6–9 — Hover Tooltips:** Các bảng tra cứu chi tiết (Bảng giải thích thuật ngữ KPI, Chi tiết nhân sự, Chi tiết loại công việc và Tỷ lệ phê duyệt theo nhóm).

---

### 5. Phát Hiện Chính & Đề Xuất Hành Động

#### A. Hiệu Suất Nguồn Lực & Dự Báo Q4/2025
* **Phát hiện:** Hiệu suất chung đạt **69.4%**, dẫn đầu là nhóm **Build (73.3%)** và chi nhánh **Mexico (74.1%)**. Tuy nhiên, hiệu suất giảm từ **73.8% (FY2024)** xuống **61.5% (FY2025)**—chạm mức thấp nhất **45.1% vào tháng 08/2025**—khi nhân sự hoạt động thu hẹp còn ~80–90 người trong khi giờ Non-billable tăng **+9.4%**. Dự báo Q4/2025 hiệu suất sẽ phục hồi vào **tháng 11 (58.9%)** trước khi giảm về **40.6% trong tháng 12** do kỳ nghỉ lễ cuối năm.
* **Hành động:** Rà soát và điều chuyển quỹ giờ nhàn rỗi từ Q2–Q3/2025 sang các đầu việc tính phí; tách riêng nhân sự làm công tác điều hành (`Leadership`) khỏi nhóm sản xuất kỹ thuật để đo lường đúng hiệu suất.

#### B. Tập Trung Chi Phí Dự Án & Áp Lực Làm Thêm Giờ
* **Phát hiện:** Dự án **`LMP00001503`** chiếm **55.5% tổng giờ Billable** và **$4.72M (38.0% tổng chi phí)** với tỷ lệ chuyển đổi đạt **99.8%**. Tuy nhiên, dự án này cũng tạo ra **50.2% tổng giờ làm thêm** toàn công ty (`7,625` / `15,200` giờ), gây quá tải cục bộ cho nhóm **Build** (chiếm `58.4%` tổng Overtime, cao điểm vào tháng 03/2025).
* **Hành động:** Lập kế hoạch điều phối và bổ sung nhân sự hỗ trợ cho nhóm Build trước các mốc cao điểm của `LMP00001503` nhằm giảm chi phí làm thêm giờ (`$448.8K`), đồng thời đóng các mã dự án chỉ phát sinh 1 giờ làm việc.

#### C. Tối Ưu Chi Phí Công Việc Không Tính Phí (Non-Billable)
* **Phát hiện:** Chi phí Non-billable lên tới **$3.88M (31.3% tổng chi phí nhân công)**, tập trung **99.8%** tại mã dự án nội bộ **`LMP00001501`** (`4.3%` PU). Riêng chi phí **Meetings (Họp hành)** chiếm **$1.28M** (cao hơn cả nghỉ phép năm `$1.25M`) do các nhóm có đơn giá cao (`PM` `$40/giờ`, `Tech` `$37/giờ`) họp nhiều và một số nhân sự sản xuất dành tới `70%` quỹ giờ cho việc họp.
* **Hành động:** Rà soát mục tiêu đầu ra của mã dự án `LMP00001501`, giới hạn thời lượng họp định kỳ của các nhóm đơn giá cao và áp dụng khung giờ tập trung sản xuất (không họp) cho khối Build.

#### D. Tuân Thủ Quy Trình Chấm Công
* **Phát hiện:** Dù tỷ lệ phê duyệt chung đạt **98.1%**, có **19.4% bản ghi (`19,786` phiếu)** bị duyệt trễ sau hạn chót Thứ Hai—với điểm nghẽn lớn nhất nằm ở nhóm **PM (56.5% duyệt trễ)**. Bên cạnh đó, tỷ lệ **phê duyệt thay thế** (`Approved_By` $\neq$ `Time_Approver`) tăng lên **40.3% vào tháng 06/2025**, tập trung cao nhất ở nhóm **Tech (28.5%)** và **Overheads (25.8%)**.
* **Hành động:** Thiết lập hệ thống nhắc duyệt tự động vào sáng Thứ Hai hàng tuần (ưu tiên nhóm PM) và cập nhật lại danh sách người phê duyệt chính thức trên hệ thống cho nhóm Tech và Overheads.

---

### 6. Cấu Trúc Thư Mục
```text
├── data_pipeline/          # Mã nguồn Python làm sạch dữ liệu và nạp lên BigQuery
├── powerbi/                # File báo cáo Power BI (.pbix) và tài liệu công thức DAX
├── presentation/           # Slide thuyết trình tổng hợp (LEGO Analysis Presentation.pdf)
└── README.md               # Tài liệu mô tả dự án (Song ngữ Anh - Việt)
```