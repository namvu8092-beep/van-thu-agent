# HƯỚNG DẪN CHI TIẾT CÁCH LẬP TỪNG LOẠI BÁO CÁO DOANH NGHIỆP
*(Cẩm nang thực hành toàn diện: Nguồn dữ liệu - Công thức - Quy trình đối chiếu - Mẹo kiểm tra)*

> **Mục tiêu:** Hướng dẫn từng bước cách thu thập số liệu, xử lý tính toán và lập hoàn chỉnh từng loại báo cáo — từ Báo cáo Thuế, Báo cáo Tài chính chuẩn VAS, Báo cáo Quản trị dòng tiền cho đến Hồ sơ Thẩm định Tín dụng Ngân hàng.

---

## NGUYÊN TẮC CỐT LÕI: DÒNG CHẢY DỮ LIỆU CỦA HỆ THỐNG BÁO CÁO

Mọi báo cáo trong doanh nghiệp đều tuân theo chu trình 4 bước khép kín:

```
  [BƯỚC 1: DỮ LIỆU ĐẦU VÀO]         [BƯỚC 2: XỬ LÝ & TÍNH TOÁN]       [BƯỚC 3: ĐỐI CHIẾU & KIỂM TRA]       [BƯỚC 4: XUẤT BÁO CÁO]
  - Hóa đơn điện tử (Đầu vào/ra)    - Sổ cái tài khoản (General Ledger)  - Bảng Cân đối tài khoản (Trial Balance) - Nộp thuế: File XML qua HTKK
  - Sao kê ngân hàng (Bank Stmt) ──> - Bảng phân bổ chi phí, tính khấu hao──>- Đối chiếu chéo (Cross-check) ────>- Báo cáo Quản trị: Excel / BI
  - Bảng chấm công & tính lương      - Phân loại Biến phí vs Định phí   - Kiểm kê tồn kho, quỹ tiền mặt      - Nộp Ngân hàng: Hồ sơ tín dụng
  - Hợp đồng kinh tế & Biên bản NG
```

---

## PHẦN 1: CÁCH LẬP CÁC BÁO CÁO THUẾ & HÓA ĐƠN

### 1. Cách lập Tờ khai Thuế GTGT (Mẫu 01/GTGT)
*Áp dụng: Phương pháp khấu trừ theo tháng (hạn ngày 20) hoặc theo quý (hạn ngày cuối tháng đầu quý sau).*

- **Nguồn số liệu:**
  1. Bảng kê hóa đơn hàng hóa, dịch vụ mua vào (thu thập từ cổng hóa đơn điện tử `hoadondientu.gdt.gov.vn`).
  2. Bảng kê hóa đơn hàng hóa, dịch vụ bán ra xuất trong kỳ.
- **Quy trình lập:**
  - **Bước 1:** Mở phần mềm **HTKK (Hỗ trợ kê khai)** của Tổng cục Thuế, chọn kỳ kê khai (tháng hoặc quý).
  - **Bước 2 (Chỉ tiêu [22]):** Nhập số thuế GTGT còn được khấu trừ kỳ trước chuyển sang (phải khớp chính xác với chỉ tiêu [43] của tờ khai kỳ trước liền kề).
  - **Bước 3 (Mua vào):** Nhập tổng giá trị mua vào chưa thuế tại chỉ tiêu **[23]** và thuế GTGT mua vào tại chỉ tiêu **[24]**. Điền số thuế đủ điều kiện khấu trừ vào chỉ tiêu **[25]** (lưu ý: Hóa đơn mua vào từ 20 triệu trở lên phải có chứng từ thanh toán không dùng tiền mặt/chuyển khoản ngân hàng thì mới được điền vào [25]).
  - **Bước 4 (Bán ra):** Nhập doanh thu bán ra theo từng nhóm thuế suất:
    - Không chịu thuế: Chỉ tiêu **[26]**.
    - Thuế suất 0% (Hàng xuất khẩu): Chỉ tiêu **[29]**.
    - Thuế suất 5%: Chỉ tiêu **[30]** và thuế GTGT **[31]**.
    - Thuế suất 10% (hoặc 8% nếu có chính sách giảm thuế): Chỉ tiêu **[32]** và thuế GTGT **[33]**.
  - **Bước 5 (Tính kết quả):**
    - Nếu Thuế bán ra [35] > Thuế mua vào được khấu trừ [25] + [22] $\to$ Phát sinh thuế phải nộp tại chỉ tiêu **[40]** $\to$ Mang tiền đi nộp vào kho bạc.
    - Nếu Thuế bán ra [35] < Thuế mua vào được khấu trừ [25] + [22] $\to$ Chưa khấu trừ hết tại chỉ tiêu **[43]** $\to$ Chuyển sang chỉ tiêu [22] của kỳ sau.
  - **Bước 6:** Bấm "Ghi", xuất file định dạng **XML**, đăng nhập trang `thuedientu.gdt.gov.vn` bằng Chữ ký số (Token) để ký điện tử và nộp.

---

### 2. Cách lập Tờ khai Quyết toán Thuế TNDN (Mẫu 03/TNDN)
*Áp dụng: Hàng năm, hạn chót ngày cuối tháng thứ 3 kể từ khi kết thúc năm tài chính (31/03).*

- **Nguồn số liệu:** Báo cáo kết quả hoạt động kinh doanh (P&L) năm và Sổ chi tiết các khoản chi phí.
- **Quy trình lập:**
  - **Bước 1:** Điền chỉ tiêu **[A1] - Tổng lợi nhuận kế toán trước thuế** (lấy từ Mã số 50 trên Báo cáo kết quả HĐKD).
  - **Bước 2 (Điều chỉnh tăng lợi nhuận - Các chi phí không được trừ theo luật thuế):**
    - Chi phí không có hóa đơn chứng từ hợp pháp hoặc thanh toán tiền mặt $\ge 20$ triệu: Điền vào **[B4]**.
    - Tiền phạt vi phạm hành chính, phạt chậm nộp thuế: Điền vào **[B7]**.
    - Chi phí vượt định mức (khấu hao xe ô tô dưới 9 chỗ vượt 1.6 tỷ đối với DN không kinh doanh vận tải...): Điền vào **[B4]**.
  - **Bước 3 (Thu nhập chịu thuế):**
    $$\text{Chỉ tiêu [B14]} = [\text{A1}] + [\text{B1}] - [\text{B8}]$$
  - **Bước 4 (Chuyển lỗ):** Nếu các năm trước có lỗ (tối đa 5 năm gần nhất), lập Phụ lục 03-2A/TNDN và chuyển vào chỉ tiêu **[C3]**.
  - **Bước 5 (Tính thuế phải nộp):**
    $$\text{Thu nhập tính thuế [C4]} = [\text{B14}] - [\text{C3}]$$
    $$\text{Thuế TNDN phải nộp [C8]} = [\text{C4}] \times 20\%$$
  - **Bước 6 (Đối chiếu tạm nộp):** Điền tổng số tiền thuế TNDN đã tạm nộp trong 4 quý vào chỉ tiêu **[E1]**.
    - *Lưu ý sống còn:* Tổng số tạm nộp 4 quý phải $\ge 80\%$ số quyết toán tại [C8]. Nếu thấp hơn 80%, phần chênh lệch thiếu sẽ bị tính tiền phạt chậm nộp (0.03%/ngày).

---

## PHẦN 2: CÁCH LẬP BỘ BÁO CÁO TÀI CHÍNH CHUẨN VAS (THÔNG TƯ 200 / TT 133)

Quy trình lập BCTC gồm 3 bước kế toán kinh điển:

```
[Sổ Cái các Tài Khoản] ──> [Bảng Cân Đối Số Phát Sinh] ──> [Lập B01, B02, B03, B09]
 (TK loại 1 đến loại 9)      (Trial Balance - 8 Cột)         (Bộ BCTC nộp Cơ quan Nhà nước)
```

### 1. Bảng Cân Đối Kế Toán (Mẫu B01-DN)
- **Bản chất:** Báo cáo **Thời điểm** (chụp ảnh tài sản và nguồn vốn tại ngày 31/12).
- **Nguyên tắc lập:**
  - Toàn bộ Tài sản (TK đầu 1, 2) có số dư Nợ $\to$ Lên cột **TÀI SẢN**.
  - Toàn bộ Nợ phải trả (TK đầu 3) và Vốn CSH (TK đầu 4) có số dư Có $\to$ Lên cột **NGUỒN VỐN**.
- **Quy tắc bù trừ công nợ cực kỳ quan trọng:**
  - Không được bù trừ số dư của Tài khoản 131 (Phải thu KH) và 331 (Phải trả người bán).
  - Phải tách chi tiết từng đối tượng: Khách hàng nào dư Nợ thì đưa vào Tài sản (Phải thu ngắn hạn - Mã 131); Khách hàng nào dư Có (người mua trả tiền trước) phải đưa vào Nguồn vốn (Người mua trả tiền trước - Mã 312).
- **Nguyên tắc Cân bằng:**
  $$\text{Tổng Tài Sản (Mã 270)} \equiv \text{Tổng Nguồn Vốn (Mã 440)}$$
  *(Nếu 2 con số này lệch nhau dù chỉ 1 đồng nghĩa là kế toán hạch toán sai).*

---

### 2. Báo Cáo Kết Quả Hoạt Động Kinh Doanh (Mẫu B02-DN - P&L)
- **Bản chất:** Báo cáo **Thời kỳ** (đo lường hiệu quả từ ngày 01/01 đến 31/12).
- **Nguồn số liệu:** Lấy số phát sinh kết chuyển của các tài khoản doanh thu (đầu 5), giảm trừ (521), giá vốn (632), chi phí (635, 641, 642, 811), thu nhập khác (711).
- **Công thức bậc thang:**
  1. Doanh thu thuần (Mã 10) = Tổng DT bán hàng (Mã 01) - Giảm trừ doanh thu (Mã 02).
  2. Lợi nhuận gộp (Mã 20) = Doanh thu thuần (10) - Giá vốn hàng bán (11).
  3. Lợi nhuận thuần HĐKD (Mã 30) = Lợi nhuận gộp (20) + DT tài chính (21) - CP tài chính (22) - CP bán hàng (25) - CP quản lý (26).
  4. Lợi nhuận trước thuế (Mã 50) = Lợi nhuận thuần (30) + Lợi nhuận khác (40).
  5. Lợi nhuận sau thuế (Mã 60) = LNTT (50) - Thuế TNDN hiện hành (51).

---

### 3. Báo Cáo Lưu Chuyển Tiền Tệ (Mẫu B03-DN)
- **Bản chất:** Theo dõi tiền thực vào/ra trong năm.
- **Có 2 phương pháp lập:**
  - **Phương pháp trực tiếp:** Lấy trực tiếp từ sổ cái tài khoản Tiền mặt (111) và Tiền gửi ngân hàng (112) đối ứng với các tài khoản khác (Thu tiền bán hàng Nợ 112/Có 131; Chi trả NCC Nợ 331/Có 112; Chi trả lương Nợ 334/Có 112).
  - **Phương pháp gián tiếp:** Bắt đầu từ Lợi nhuận trước thuế (Mã 01) $\to$ Cộng ngược lại Khấu hao tài sản (chi phí không bằng tiền) $\to$ Điều chỉnh các khoản biến động Vốn lưu động (Khoản phải thu, Hàng tồn kho, Khoản phải trả).
- **Kiểm tra chéo:** Số dư tiền cuối kỳ trên Báo cáo lưu chuyển tiền tệ (Mã 70) phải **bằng đúng** chỉ tiêu Tiền và tương đương tiền trên Bảng cân đối kế toán (Mã 110).

---

## PHẦN 3: CÁCH LẬP CÁC BÁO CÁO TÀI CHÍNH QUẢN TRỊ NỘI BỘ

### 1. Cách lập Báo cáo Dòng tiền Cuộn 13 Tuần (13-Week Cashflow)
Đây là công cụ quản trị tiền mặt quan trọng nhất của CFO:
- **Bước 1: Chốt số dư đầu tuần (Opening Cash):** Lấy chính xác số dư thực tế tại quỹ tiền mặt và tất cả tài khoản ngân hàng vào 08:00 sáng thứ Hai.
- **Bước 2: Dự báo Dòng tiền vào (Cash Inflow):**
  - Căn cứ vào Báo cáo Tuổi nợ phải thu (AR Aging) và điều khoản hợp đồng của các khách hàng lớn sắp đến hạn thanh toán trong tuần.
  - Doanh thu bán lẻ / thuê bao thu tiền ngay hàng ngày.
- **Bước 3: Dự báo Dòng tiền ra (Cash Outflow):**
  - Bảng lương (chi cố định vào ngày 5 hoặc 10 hàng tháng).
  - Thuế và BHXH (chi trước ngày 20 hoặc cuối tháng).
  - Nợ người bán đến hạn thanh toán (AP Aging).
  - Tiền thuê nhà, lãi vay ngân hàng.
- **Bước 4: Tính Số dư cuối tuần & Đối chiếu ngưỡng sàn:**
  $$\text{Số dư cuối tuần} = \text{Số dư đầu} + \text{Tổng tiền vào} - \text{Tổng tiền ra}$$
  - Nếu số dư cuối tuần chạm hoặc thấp hơn **Ngưỡng an toàn tối thiểu (Safety Floor)** $\to$ Kế toán trưởng phải lập tức báo động cho Giám đốc để: Thúc giục thu hồi nợ, đàm phán giãn nợ nhà cung cấp, hoặc giải ngân hạn mức vay ngân hàng.

---

### 2. Cách lập Báo cáo P&L Quản trị theo Đơn vị Kinh doanh (BU P&L)
Khác với P&L kế toán chỉ nhìn toàn bộ công ty, P&L quản trị bóc tách theo nguyên lý **Số dư đảm phí (Marginal Costing)**:
- **Bước 1:** Bóc tách Doanh thu thuần của từng BU / Dòng sản phẩm.
- **Bước 2:** Trừ đi **Biến phí trực tiếp (Direct Variable Costs)** sinh ra theo sản phẩm (Hoa hồng sales, giá vốn nguyên liệu, server cloud, cước vận chuyển).
  $$\text{Số dư đảm phí (Contribution Margin - CM)} = \text{Doanh thu} - \text{Biến phí}$$
  *(Chỉ số này cho biết mỗi BU đóng góp được bao nhiêu tiền để gánh định phí chung của công ty).*
- **Bước 3:** Trừ đi **Định phí trực tiếp của BU** (Lương cứng nhân sự riêng của BU đó, chi phí tool làm việc).
  $$\text{Lợi nhuận đóng góp của BU} = \text{CM} - \text{Định phí riêng của BU}$$
- **Bước 4:** Phân bổ **Định phí chung (Corporate Overhead)** (Tiền thuê văn phòng, lương kế toán, HR, ban giám đốc) theo tiêu thức tỷ trọng doanh thu hoặc nhân sự.
- **Kết luận:** Nếu một BU có Contribution Margin âm $\to$ **Càng bán càng lỗ**, cần dừng ngay dòng sản phẩm đó!

---

## PHẦN 4: HƯỚNG DẪN DÀNH CHO DÂN TÀI CHÍNH - NGÂN HÀNG (THẨM ĐỊNH TÍN DỤNG)

### 1. Cách Lập Bảng Tính Nhu Cầu Vốn Lưu Động & Hạn Mức Vay Ngân Hàng
Khi lập hồ sơ xin cấp Hạn mức tín dụng ngắn hạn bổ sung vốn lưu động gửi ngân hàng (Mẫu chuẩn Vietcombank, BIDV, Techcombank):

- **Bước 1: Tính Tổng Chi Phí SXKD Cần Vốn trong năm tới:**
  $$\text{Tổng chi phí bằng tiền} = \text{Tổng chi phí hoạt động kế hoạch} - \text{Chi phí khấu hao TSCĐ}$$
  *(Khấu hao là chi phí phi tiền tệ nên không cần vốn tài trợ).*
- **Bước 2: Tính Vòng quay Vốn lưu động (Vòng/năm):**
  $$\text{Vòng quay VLĐ} = \frac{\text{Doanh thu thuần kế hoạch}}{\text{Vốn lưu động bình quân}} \quad \text{hoặc} \quad \frac{365}{\text{Cash Conversion Cycle (CCC)}}$$
- **Bước 3: Tính Tổng Nhu cầu Vốn lưu động trong 1 vòng quay:**
  $$\text{Tổng nhu cầu VLĐ} = \frac{\text{Tổng chi phí bằng tiền (Bước 1)}}{\text{Vòng quay VLĐ (Bước 2)}}$$
- **Bước 4: Xác định các nguồn tài trợ tự có và chiếm dụng:**
  - Vốn tự có tham gia của doanh nghiệp (Vốn lưu động ròng = TSNH - Nợ ngắn hạn).
  - Nợ chiếm dụng hợp pháp từ người bán (Số dư nợ phải trả người bán bình quân).
- **Bước 5: Tính Hạn Mức Tín Dụng Vay Ngân Hàng Thiếu Hụt:**
  $$\text{Hạn mức vay đề nghị} = \text{Tổng nhu cầu VLĐ} - \text{Vốn tự có tham gia} - \text{Nợ chiếm dụng người bán}$$
  *(Con số này chính là hạn mức tín dụng mà Ngân hàng sẽ trình Hội đồng Tín dụng phê duyệt cho doanh nghiệp).*

---

### 2. Cách Chạy Mô Hình Dupont 3 Bước & 5 Bước
Phục vụ phân tích chuyên sâu báo cáo tài chính:
- **Dupont 3 bước:**
  $$\text{ROE} = \underbrace{\frac{\text{LNST}}{\text{Doanh thu}}}_{\text{Biên LN ròng (1)}} \times \underbrace{\frac{\text{Doanh thu}}{\text{Tổng tài sản}}}_{\text{Vòng quay tài sản (2)}} \times \underbrace{\frac{\text{Tổng tài sản}}{\text{Vốn CSH}}}_{\text{Đòn bẩy tài chính (3)}}$$
  - **Ý nghĩa thẩm định:** So sánh 3 năm liên tiếp. Nếu ROE tăng mà nhân tố (1) và (2) giảm, chỉ có nhân tố (3) tăng $\to$ Doanh nghiệp đang tăng trưởng ảo nhờ "ôm nợ vay quá mức", rủi ro vỡ nợ tiềm ẩn!

---

## PHẦN 5: CHECKLIST KIỂM TRA ĐỐI CHIẾU CHÉO (CROSS-CHECKING SECRETS)

Trước khi nộp bất kỳ báo cáo nào cho Ban Giám đốc, Cơ quan Thuế hay Ngân hàng, luôn chạy 5 bước kiểm tra chéo sau:

| Đối tượng kiểm tra | Nguồn A | Nguồn B | Yêu cầu đối chiếu |
| :--- | :--- | :--- | :--- |
| **Doanh thu** | Báo cáo P&L (Mã 01) | Tổng doanh thu trên 4 tờ khai thuế GTGT cả năm | Phải khớp nhau (nếu lệch phải có bảng giải trình doanh thu chưa xuất hóa đơn). |
| **Tiền mặt & Ngân hàng** | BCTC (Mã 110) | Sổ phụ ngân hàng tại 31/12 + Biên bản kiểm kê quỹ tiền mặt | Phải khớp 100% đến từng đồng. |
| **Khấu hao TSCĐ** | Chi phí khấu hao trên P&L | Hao mòn lũy kế tăng thêm trên Bảng cân đối KT | Số khấu hao trích trong năm trên B02 phải bằng số biến động tăng hao mòn trên B01. |
| **Dòng tiền** | Báo cáo Lưu chuyển tiền tệ (Mã 70) | Tiền và tương đương tiền trên Bảng cân đối KT (Mã 110) | Bắt buộc phải bằng nhau tuyệt đối. |
| **Nợ vay ngân hàng** | Vay ngắn hạn & dài hạn trên BCTC (Mã 320 + 330) | Bản tra cứu báo cáo quan hệ tín dụng CIC tại thời điểm chốt sổ | Số dư nợ gốc phải khớp với dư nợ thực tế các ngân hàng ghi nhận trên hệ thống CIC. |

---
*Tài liệu được biên soạn phục vụ công tác chuẩn hóa quy trình lập báo cáo và đào tạo nghiệp vụ phân tích tài chính - tín dụng ngân hàng.*
