# Insight đã hoàn thành

**Phạm vi:** mẫu 10.000 đặt phòng, hai khách sạn (City Hotel và Resort Hotel), giai đoạn 2015–2017.
**Đáp ứng yêu cầu:** 6 insight, 5 chủ đề khác nhau (giá phòng/ADR, mùa vụ, lead time, quốc gia, phân khúc thị trường); mỗi đoạn 80–120 từ.

---

## Bảng tổng hợp

| # | Chủ đề | Bằng chứng (Câu / Bảng / Hình) | Phát hiện chính (1 câu) |
|---|---|---|---|
| 1 | Giá phòng (ADR) · khách sạn | Hình 1 (`fig07_adr_hist.png`) | ADR trung bình của City Hotel cao hơn Resort Hotel 14,58 EUR (≈15,58%). |
| 2 | Mùa vụ | Bảng `q03_monthly.csv` | Năm 2016, City Hotel đỉnh tháng 10 (360), Resort Hotel đỉnh tháng 5 (162). |
| 3 | Lead time · hủy phòng | Hình 3 (`fig03_leadtime_cancel.png`) | Nhóm đặt ≥181 ngày có tỷ lệ hủy 58,06%, cao hơn nhóm 0–7 ngày (10,06%) khoảng 48 điểm phần trăm. |
| 4 | Quốc gia | Hình 4 (`fig04_top10_country.png`) | Bồ Đào Nha chiếm 40,05% đặt phòng nhưng có tỷ lệ hủy 57,68%. |
| 5 | Phân khúc thị trường | Hình 5 (`fig05_segment_cancel.png`) | Tỷ lệ hủy của Groups (61,89%) cao hơn Direct (15,03%) 46,86 điểm phần trăm. |
| 6 | Khách quay lại · lead time | Hình 6 (`repeat_lead_boxplot.png`) | Trung vị lead time của khách quay lại chỉ 4 ngày, so với 74 ngày của khách mới. |

---

## Insight 1 — City Hotel có ADR trung bình cao hơn Resort Hotel

- **Câu hỏi / chủ đề:** Giá phòng (ADR) giữa hai khách sạn có khác nhau không?
- **Phát hiện chính:** ADR trung bình của City Hotel cao hơn Resort Hotel 14,58 EUR mỗi đêm.
- **Số liệu, đơn vị và mẫu số:** 108,18 EUR/đêm trên 3.915 đặt phòng (City) và 93,60 EUR/đêm trên 2.320 đặt phòng (Resort); điều kiện lọc: không hủy, adr > 0; mẫu phân tích 6.235 đặt phòng (loại 3.765 đặt phòng so với mẫu 10.000 vì bị hủy hoặc adr ≤ 0).
- **So sánh làm rõ phát hiện:** Chênh 14,58 EUR (≈15,58% so với Resort); trung vị 100,65 so với 75,00 EUR; Welch t = 10,7528, p = 7,51 × 10⁻²⁷, khoảng tin cậy 95% của chênh lệch: 12,34–16,80 EUR.
- **Ý nghĩa trong phạm vi dữ liệu:** Trong hai khách sạn của mẫu, City Hotel có mức giá phòng ghi nhận cao hơn.
- **Giới hạn hoặc thông tin cần kiểm chứng:** Hai phân phối chồng lấn đáng kể (khoảng Q1–Q3); ADR không phải doanh thu thực; chưa kiểm soát loại phòng, mùa, kênh bán.
- **Bằng chứng:** Hình `outputs/figures/fig07_adr_hist.png`

**Đoạn hoàn chỉnh (~116 từ):**

> Trong 6.235 đặt phòng không bị hủy và có adr lớn hơn 0, ADR trung bình của City Hotel là 108,18 EUR mỗi đêm (3.915 đặt phòng), cao hơn Resort Hotel là 93,60 EUR (2.320 đặt phòng) 14,58 EUR, tương đương khoảng 15,58%. Trung vị cũng cao hơn (100,65 so với 75,00 EUR), nên chênh lệch không chỉ nằm ở giá trị trung bình. Kiểm định Welch cho thấy chênh lệch có ý nghĩa thống kê (p = 7,51 × 10⁻²⁷; khoảng tin cậy 95%: 12,34–16,80 EUR). Kết quả chỉ áp dụng cho hai khách sạn của mẫu; hai phân phối còn chồng lấn đáng kể, và ADR không phải doanh thu thực. *(Nguồn: Hình 1)*

---

## Insight 2 — Hai khách sạn có mùa cao điểm đặt phòng khác nhau

- **Câu hỏi / chủ đề:** Mùa vụ — tháng nào có nhiều đặt phòng nhất ở mỗi khách sạn?
- **Phát hiện chính:** Năm 2016, City Hotel đạt đỉnh vào tháng 10, Resort Hotel đạt đỉnh vào tháng 5.
- **Số liệu, đơn vị và mẫu số:** 360 đặt phòng (City, tháng 10) và 162 đặt phòng (Resort, tháng 5) trong 4.759 đặt phòng năm 2016; điều kiện lọc: chỉ năm 2016.
- **So sánh làm rõ phát hiện:** So với tháng 1 (thấp nhất), đỉnh City Hotel cao gấp ≈3,08 lần; đỉnh Resort Hotel cao gấp ≈2,61 lần.
- **Ý nghĩa trong phạm vi dữ liệu:** Cách phân bổ nhân sự theo tháng có thể cần khác nhau giữa hai khách sạn.
- **Giới hạn hoặc thông tin cần kiểm chứng:** Chỉ có một năm 2016 trọn vẹn, chưa đủ để kết luận quy luật mùa vụ lặp lại hằng năm.
- **Bằng chứng:** Bảng `outputs/tables/q03_monthly.csv`

**Đoạn hoàn chỉnh (~117 từ):**

> Trong 4.759 đặt phòng năm 2016, City Hotel đạt đỉnh vào tháng 10 với 360 đặt phòng, còn Resort Hotel đạt đỉnh vào tháng 5 với 162 đặt phòng. So với tháng 1, tháng thấp nhất, đỉnh của City Hotel cao gấp khoảng 3,08 lần và đỉnh của Resort Hotel cao gấp khoảng 2,61 lần. Như vậy hai khách sạn có mùa cao điểm lệch nhau, và cách phân bổ nhân sự theo tháng có thể cần khác nhau trong phạm vi hai khách sạn này. Tuy nhiên, dữ liệu mới có một năm 2016 trọn vẹn nên chưa đủ để kết luận đây là quy luật mùa vụ lặp lại hằng năm. *(Nguồn: Bảng q03_monthly)*

---

## Insight 3 — Đặt càng sớm, tỷ lệ hủy quan sát được càng cao

- **Câu hỏi / chủ đề:** Lead time có liên quan đến tỷ lệ hủy phòng không?
- **Phát hiện chính:** Nhóm đặt trước ≥181 ngày có tỷ lệ hủy cao hơn nhiều so với nhóm đặt 0–7 ngày.
- **Số liệu, đơn vị và mẫu số:** 1.199/2.065 (58,06%) với nhóm ≥181 ngày; 159/1.581 (10,06%) với nhóm 0–7 ngày; mẫu 9.969 đặt phòng có nhóm lead time (31 đặt phòng không đưa vào phân tích).
- **So sánh làm rõ phát hiện:** Chênh ≈48 điểm phần trăm; gấp ≈5,77 lần.
- **Ý nghĩa trong phạm vi dữ liệu:** Với hai khách sạn của mẫu, đặt phòng đặt sớm có thể cần quy trình xác nhận và theo dõi riêng.
- **Giới hạn hoặc thông tin cần kiểm chứng:** Chỉ là mối liên hệ quan sát được, không chứng minh quan hệ nhân quả; cần kiểm tra thêm theo khách sạn, phân khúc, chính sách đặt cọc.
- **Bằng chứng:** Hình `outputs/figures/fig03_leadtime_cancel.png`

**Đoạn hoàn chỉnh (~106 từ):**

> Trong 9.969 đặt phòng có nhóm lead time, nhóm đặt trước từ 181 ngày trở lên có 1.199 trên 2.065 đặt phòng bị hủy (58,06%), còn nhóm đặt 0–7 ngày trước ngày đến có 159 trên 1.581 bị hủy (10,06%). Chênh lệch khoảng 48 điểm phần trăm, tức tỷ lệ hủy của nhóm đặt sớm cao gấp khoảng 5,77 lần. Trong phạm vi hai khách sạn của mẫu, các đặt phòng đặt sớm có thể cần quy trình xác nhận và theo dõi riêng. Tuy nhiên, đây chỉ là mối liên hệ quan sát được, không chứng minh quan hệ nhân quả. *(Nguồn: Hình 3)*

---

## Insight 4 — Bồ Đào Nha chiếm thị phần lớn nhất nhưng tỷ lệ hủy cao

- **Câu hỏi / chủ đề:** Quốc gia — thị trường lớn nhất có chất lượng đặt phòng tốt không?
- **Phát hiện chính:** Bồ Đào Nha chiếm 40,05% đặt phòng nhưng có tỷ lệ hủy 57,68%.
- **Số liệu, đơn vị và mẫu số:** 4.005/10.000 đặt phòng (40,05%); 2.310/4.005 bị hủy (57,68%); Vương quốc Anh có 999 đặt phòng.
- **So sánh làm rõ phát hiện:** Gấp ≈4 lần Vương quốc Anh về số đặt phòng; tỷ lệ hủy cao hơn Vương quốc Anh 37,96 điểm phần trăm (suy ra Vương quốc Anh ≈19,72%).
- **Ý nghĩa trong phạm vi dữ liệu:** Thị phần lớn không đi cùng tỷ lệ hủy thấp; nên xem xét kỹ đặc điểm đặt phòng của thị trường này.
- **Giới hạn hoặc thông tin cần kiểm chứng:** Không có lý do hủy; không suy rộng cho mọi khách Bồ Đào Nha.
- **Bằng chứng:** Hình `outputs/figures/fig04_top10_country.png`

**Đoạn hoàn chỉnh (~105 từ):**

> Trong 10.000 đặt phòng, Bồ Đào Nha chiếm 4.005 (40,05%), gấp khoảng bốn lần Vương quốc Anh, thị trường lớn thứ hai với 999 đặt phòng. Tuy nhiên, 2.310 trên 4.005 đặt phòng của Bồ Đào Nha bị hủy (57,68%), cao hơn Vương quốc Anh 37,96 điểm phần trăm (suy ra khoảng 19,72%). Điều này cho thấy trong mẫu hai khách sạn, thị phần lớn không đi cùng tỷ lệ hủy thấp, nên nhóm khách này đáng được xem xét kỹ hơn. Dữ liệu không nêu lý do hủy, cũng không cho phép suy rộng cho mọi khách Bồ Đào Nha. *(Nguồn: Hình 4)*

---

## Insight 5 — Tỷ lệ hủy khác biệt lớn giữa các phân khúc thị trường

- **Câu hỏi / chủ đề:** Phân khúc thị trường — phân khúc nào có tỷ lệ hủy cao/thấp?
- **Phát hiện chính:** Groups hủy nhiều nhất (61,89%), Direct hủy ít nhất trong các nhóm được nêu (15,03%).
- **Số liệu, đơn vị và mẫu số:** Groups 1.054/1.703; Direct 153/1.018; Online TA 36,98% trên 4.741 đặt phòng; mẫu 9.997 đặt phòng đưa vào phân tích.
- **So sánh làm rõ phát hiện:** Groups cao hơn Direct 46,86 điểm phần trăm; cao hơn Online TA ≈24,91 điểm phần trăm.
- **Ý nghĩa trong phạm vi dữ liệu:** Chất lượng đặt phòng nên đánh giá theo từng phân khúc, không chỉ theo khối lượng.
- **Giới hạn hoặc thông tin cần kiểm chứng:** Thiếu điều khoản hợp đồng, chính sách đặt cọc, quy mô từng đoàn.
- **Bằng chứng:** Hình `outputs/figures/fig05_segment_cancel.png`

**Đoạn hoàn chỉnh (~114 từ):**

> Trong 9.997 đặt phòng đưa vào phân tích, Groups có 1.054 trên 1.703 đặt phòng bị hủy (61,89%), trong khi Direct chỉ có 153 trên 1.018 (15,03%), chênh 46,86 điểm phần trăm. Online TA có lượng đặt phòng lớn nhất với 4.741, nhưng tỷ lệ hủy là 36,98%, thấp hơn Groups khoảng 24,91 điểm phần trăm. Vì vậy, trong phạm vi hai khách sạn này, chất lượng đặt phòng nên được đánh giá theo từng phân khúc chứ không chỉ theo khối lượng. Tuy nhiên, dữ liệu không có điều khoản hợp đồng, chính sách đặt cọc hay quy mô từng đoàn, nên chưa thể giải thích chênh lệch. *(Nguồn: Hình 5)*

---

## Insight 6 — Khách quay lại đặt sát ngày đến hơn khách mới

- **Câu hỏi / chủ đề:** Khách quay lại và khách mới có hành vi đặt trước khác nhau không?
- **Phát hiện chính:** Trung vị lead time của khách quay lại là 4 ngày, so với 74 ngày của khách mới.
- **Số liệu, đơn vị và mẫu số:** Khách mới: 9.706 đặt phòng, trung bình 106,94 ngày, trung vị 74 ngày; khách quay lại: 294 đặt phòng (≈2,9% của 10.000), trung bình 38,11 ngày, trung vị 4 ngày.
- **So sánh làm rõ phát hiện:** Trung vị của khách mới cao hơn 70 ngày; trung bình cao hơn ≈68,83 ngày.
- **Ý nghĩa trong phạm vi dữ liệu:** Nhóm khách quay lại có thể cần cách tiếp cận đặt phòng khác nhóm khách mới.
- **Giới hạn hoặc thông tin cần kiểm chứng:** Nhóm quay lại chỉ 294 đặt phòng nên cần thận trọng khi khái quát; dữ liệu không giải thích lý do.
- **Bằng chứng:** Hình `outputs/figures/repeat_lead_boxplot.png`

**Đoạn hoàn chỉnh (~115 từ):**

> Trong 10.000 đặt phòng, 9.706 thuộc khách mới có lead time trung bình 106,94 ngày và trung vị 74 ngày, còn 294 đặt phòng của khách quay lại (khoảng 2,9%) có trung bình chỉ 38,11 ngày và trung vị 4 ngày. Trung vị của khách mới cao hơn khách quay lại 70 ngày, tức khách quay lại thường đặt sát ngày đến hơn nhiều. Trong phạm vi hai khách sạn này, nhóm khách quay lại có thể cần cách tiếp cận đặt phòng khác nhóm khách mới. Tuy nhiên, cỡ mẫu nhóm quay lại nhỏ (294), nên cần thận trọng khi khái quát; dữ liệu cũng không giải thích lý do. *(Nguồn: Hình 6)*

---

## Ghi chú cần kiểm tra trước khi nộp

- Insight 2: văn bản gốc ghi nguồn là `outputs/figures/q03_monthly.csv`; tệp `.csv` là bảng nên tôi ghi `outputs/tables/`. Hãy đối chiếu đường dẫn thật.
- Insight 6: văn bản gốc ghi "n = 9706" ở chú thích hình, nhưng 9.706 chỉ là khách mới; tổng hai nhóm là 10.000. Nên sửa chú thích hình.
- Insight 1: 3.765 đặt phòng bị loại được suy ra từ 10.000 − 6.235; chưa tách số bị hủy và số adr ≤ 0.
- Insight 2: văn bản gốc chưa nói 4.759 đặt phòng năm 2016 có gồm đặt phòng bị hủy hay không; hãy nêu rõ.
- Insight 3 và 5: số đặt phòng bị loại (31 và 3) chưa có lý do trong văn bản gốc.
- Tỷ lệ hủy của Vương quốc Anh (≈19,72%) và chênh lệch 24,91 điểm phần trăm ở Insight 5 là số tính từ các số có sẵn.
