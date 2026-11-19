# NhomXX — Bài thực hành dữ liệu đặt phòng khách sạn



## 1. Thành viên và phân công

| Họ tên | MSSV | Phụ trách chính | Có thể giải thích thêm |
|---|---|---|---|
|Phạm Ngọc Hoàng Anh |11250869| Khảo sát dữ liệu và kiểm tra chất lượng | Quy tắc phát hiện missing, biến thể nhãn, bản ghi trùng |
|Nguyễn Minh Vũ |11258998 | Làm sạch và hợp nhất dữ liệu | Chuẩn hóa kiểu dữ liệu, xử lý xung đột `booking_id`, truy vết |
|Vũ Huy Phát |11256744| Phân tích, trực quan hóa và báo cáo | 10 câu hỏi phân tích, insight và diễn giải kết quả |



## 2. Cách chạy lại

### Cấu trúc thư mục

Đặt notebook và dữ liệu theo cấu trúc sau (giữ nguyên tên thư mục/tệp):

```text
NhomXX_KhachSan/
├── hotel_analysis.ipynb
├── data/
│   └── hotel_bookings_dirty.csv
├── tools/
│   └── kiem_tra_nop_bai.py        # nếu đề/gói bài tập có cung cấp
└── outputs/
    ├── bookings_clean.csv
    ├── monthly_summary.csv
    ├── cleaning_log.csv
    ├── row_lineage.csv
    ├── quality_report.csv
    ├── tables/
    │   └── 14 tệp CSV bảng phân tích
    └── figures/
        └── 8 tệp PNG biểu đồ
```

Notebook cũng tìm `hotel_bookings_dirty.csv` ở thư mục gốc nếu không tìm thấy trong `data/`.

### Các bước thực hiện

1. Giải nén gói bài nộp và giữ nguyên cấu trúc thư mục.
2. Mở notebook bằng Jupyter Notebook, JupyterLab, Google Colab hoặc VS Code có hỗ trợ Jupyter.
3. Đảm bảo tệp `hotel_bookings_dirty.csv` nằm trong `data/` hoặc cùng thư mục với notebook.
4. Nếu dùng bản notebook hiện tại, mở `hotel_analysis_completed.ipynb`. Trước khi nộp, có thể đổi tên thành `hotel_analysis.ipynb` theo yêu cầu của notebook/mẫu bài tập.
5. Chọn **Restart Kernel and Run All** (hoặc **Runtime → Run all** trên Colab) để chạy từ đầu đến cuối.
6. Notebook tự tạo thư mục `outputs/`, `outputs/tables/` và `outputs/figures/`, sau đó ghi các kết quả vào những thư mục này.
7. Kiểm tra các ô xác nhận `✅ / ❌`. Chỉ nộp sau khi toàn bộ kiểm tra cần thiết đạt yêu cầu.

**Thời gian chạy toàn bộ:** Notebook không ghi nhận thời gian chạy tổng thể; cần đo lại trên máy dùng để nộp.

## 3. Môi trường và thư viện

| Thành phần | Phiên bản / thông tin |
|---|---|
| Python | 3.13.5 (theo metadata của notebook; môi trường chạy thực tế có thể khác) |
| pandas | Có sử dụng; notebook không ghi cố định phiên bản |
| matplotlib | Có sử dụng; notebook không ghi cố định phiên bản |
| seaborn | Không được import/sử dụng trong notebook |
| Môi trường | Jupyter Notebook / JupyterLab / Google Colab / VS Code |

Notebook sử dụng các thư viện chính:

- `pandas`: đọc, kiểm tra, làm sạch, biến đổi, tổng hợp và xuất dữ liệu dạng bảng.
- `matplotlib.pyplot`: xây dựng và lưu biểu đồ.

Nếu môi trường chưa có thư viện, cài đặt bằng:

```bash
python -m pip install pandas matplotlib
```

Để tái lập kết quả tốt hơn, nhóm nên ghi lại phiên bản thực tế trên máy chạy bằng:

```bash
python --version
python -m pip show pandas matplotlib
```

## 4. Nguồn dữ liệu

Antonio, N., de Almeida, A., & Nunes, L. (2019). Hotel booking demand datasets. *Data in Brief*, 22, 41–49. https://doi.org/10.1016/j.dib.2018.11.126 (CC BY 4.0).

Dữ liệu đầu vào dùng trong bài thực hành là bản biên soạn cho học tập:

- Tệp: `hotel_bookings_dirty.csv`
- Kích thước đầu vào được notebook kiểm tra: **10.325 dòng × 24 cột**.
- Dữ liệu được đọc ở dạng chuỗi (`dtype=str`) để giữ nguyên cách ghi ban đầu trước khi khảo sát và chuẩn hóa.
- Đơn vị phân tích cuối cùng: **một đặt phòng (`booking_id`) là một dòng**.

Sau bước hợp nhất, dữ liệu phân tích có **10.000 booking duy nhất**. Không thay dữ liệu đầu vào bằng bộ dữ liệu sạch khác và không chỉnh sửa thủ công tệp CSV nguồn.

## 5. Quy tắc riêng của nhóm (khác hoặc bổ sung so với đề)

| # | Tình huống | Quy tắc nhóm chọn | Lý do | Ảnh hưởng đến kết quả |
|---|---|---|---|---|
| 1 | Trùng nội dung trên 23 cột nghiệp vụ | Nhận diện các dòng thuộc nhóm trùng tuyệt đối nhưng chưa xóa ngay ở B1; xử lý hợp nhất thống nhất theo `booking_id` ở B8. | Tránh mất `row_id` và phân biệt bản sao của cùng booking với hai booking khác nhau nhưng có thuộc tính giống nhau. | Sau hợp nhất, không còn nhóm trùng tuyệt đối trên 23 cột nghiệp vụ; mọi dòng nguồn vẫn được truy vết. |
| 2 | Xung đột giá trị khi gộp cùng `booking_id` | Sắp theo `row_id` tăng dần và lấy giá trị không thiếu đầu tiên cho từng trường (`groupby().first()`); lưu các cặp `booking_id`–`field` có xung đột trong `conflict_df`. | Có quy tắc xác định, nhất quán và có thể kiểm toán thay vì lựa chọn tùy ý. | Mỗi `booking_id` còn đúng một dòng; khi có xung đột, giá trị ở dòng có `row_id` nhỏ hơn được ưu tiên. |
| 3 | Ô trống và ký hiệu biểu diễn thiếu | Quy `NULL`, `N/A`, `NA`, `?`, `unknown`, `-` và ô rỗng sau khi bỏ khoảng trắng về `pd.NA`. Riêng `Undefined` ở `market_segment` và `distribution_channel` được coi là thiếu; `Undefined` ở `meal` được ánh xạ thành `SC`. | Thống nhất cách biểu diễn thiếu nhưng vẫn tôn trọng ý nghĩa riêng của từng cột. | Không tự điền trung bình/mode và không xóa toàn bộ dòng thiếu; các booking vẫn có thể được dùng ở những phân tích có đủ biến cần thiết. |
| 4 | Nhãn phân loại và trạng thái hủy không nhất quán | Chuẩn hóa alias theo từ điển từng cột. Khi `reservation_status` hợp lệ, tính lại `is_canceled`: `Check-Out = 0`, `Canceled/No-Show = 1`; nếu trạng thái thiếu thì giữ cờ nhị phân đã chuẩn hóa. | Đảm bảo các biến phân loại có tập nhãn thống nhất và cờ hủy nhất quán với trạng thái. | Tỷ lệ hủy được tính từ `is_canceled` sau chuẩn hóa, tránh bỏ sót các cách ghi `yes/no`, `True/False`, `1.0/0.0` hoặc mâu thuẫn trạng thái. |
| 5 | Ngày, số và ADR sai định dạng/ngoài miền | Đọc ngày theo các định dạng chỉ định; ngày không đọc được hoặc ngoài miền chuyển thành `NaT`. Biến đếm sai/ngoài miền chuyển thành thiếu. ADR bỏ ký hiệu `€`/`EUR`, đổi dấu phẩy thập phân thành dấu chấm, kiểm tra miền 0–1000 EUR; giữ `adr = 0`. | Chỉ chuẩn hóa khi có căn cứ và tránh tự sửa giá trị không hợp lệ thành một giá trị phỏng đoán. | Một số ô thiếu có thể tăng sau làm sạch do giá trị sai/ngoài miền được chuyển thành thiếu; ADR bằng 0 vẫn được báo cáo riêng. |
| 6 | Chuẩn hóa mã quốc gia | Ánh xạ `Portugal → PRT`, `United Kingdom/UK → GBR`, `Spain → ESP`, `France → FRA`, `Germany → DEU`; giữ mã 2–3 chữ cái hợp lệ, bao gồm `CN`. Không tự gộp `CN` với `CHN` và không suy đoán quốc gia. | Không áp đặt giả định khi dữ liệu không cung cấp bằng chứng về sự tương đương. | Giá trị không hợp lệ trở thành thiếu; booking thiếu quốc gia vẫn được giữ trong các phân tích khác. |
| 7 | Tạo biến dẫn xuất và ước tính tiền phòng | Tạo `arrival_year`, `arrival_month`, `total_nights`, `total_guests`, `lead_time_group`, `room_changed_flag`, `revenue_est`. `revenue_est = adr × total_nights` chỉ cho booking không hủy và đủ dữ liệu hợp lệ. | Phục vụ phân tích theo thời gian, lưu trú và ước tính tiền phòng với điều kiện rõ ràng. | `revenue_est` chỉ là **ước tính tiền phòng**, không phải doanh thu thực tế, lợi nhuận hay tổng giá trị giao dịch. |

## 6. Danh sách tệp nộp

### Tệp chính

-  `hotel_analysis.ipynb` — notebook hoàn chỉnh (có thể đổi tên từ `hotel_analysis_completed.ipynb`).
-  `Bao_cao_Khach_san.pdf` hoặc `Bao_cao_Khach_san.docx` — báo cáo cuối cùng.
-  `README.md` — hướng dẫn cấu trúc, chạy lại và quy tắc xử lý.
-  `data/hotel_bookings_dirty.csv` — dữ liệu đầu vào theo gói bài tập.

### Kết quả trong `outputs/` — 5 tệp dữ liệu

-  `bookings_clean.csv`
-  `monthly_summary.csv`
-  `cleaning_log.csv`
-  `row_lineage.csv`
-  `quality_report.csv`

### Kết quả trong `outputs/tables/` — 14 bảng

-  `a_missing_survey.csv`
-  `a_issue_catalog.csv`
-  `q01_before_after.csv`
-  `q02_hotel_cancel.csv`
-  `q03_monthly_arrivals_2016.csv`
-  `q04_leadtime_stats.csv`
-  `q04_leadtime_cancel.csv`
-  `q05_top10_country.csv`
-  `q06_segment_cancel.csv`
-  `q07_deposit_cancel.csv`
-  `q08_adr_stats_by_hotel.csv`
-  `q09_stay_nights.csv`
-  `q10_room_change_by_hotel.csv`


### Kết quả trong `outputs/figures/` — 8 hình

-  `fig01_hotel_cancel.png`
-  `fig02_monthly_arrivals_2016.png`
-  `fig03_leadtime_cancel.png`
-  `fig04_top10_country.png`
-  `fig05_segment_cancel.png`
-  `fig06_deposit_cancel.png`
-  `fig07_adr_hist.png`
-  `fig08_stay_nights.png`

