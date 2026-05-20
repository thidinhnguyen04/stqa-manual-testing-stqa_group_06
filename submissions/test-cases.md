# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_06 |
| **Ngày tạo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — Trả sách và xử lí quá hạn (REQ-05, REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Quan hệ mượn sách | Thành viên đang mượn sách (hợp lệ) | MEM001 đang mượn BOOK003 | Cho phép trả sách |
| | Thành viên không mượn sách này | MEM001 trả BOOK007 | Không cho phép trả |
| | Sách đã được mượn trước đó | BOOK005 đã "Available" | Không cho phép trả |
| Trạng thái trả sách | Trả đúng hạn | return Date < dueDate | Trả thành công |
| | Trả vào ngày hết hạn | return Date = dueDate | Trả thành công |
| | Trả quá hạn | return Date > dueDate | Hiển thị cảnh báo trả quá hạn |
| Trạng thái sách sau khi trả  | Sách đang Borrowed | BOOK003 | Sau khi trả → chuyển thành “Available” |
| Kiểm tra quá hạn  | dueDate < currentDate | dueDate = 20/06, currentDate = 24/06 | Đánh dấu “Overdue” |
| | dueDate = currentDate (Boundary) | dueDate = 20/06, currentDate = 20/06 | Đánh dấu "Overdue" |
| | dueDate > currentDate (Boundary) | dueDate = 20/06, currentDate = 19/06 | Không quá hạn |
| Vai trò người dùng  | Librarian | LIB001 | Xem tất cả overdue records |
| | Member xem chính mình | MEM007 | Chỉ xem overdue của chính mình |
| | Member xem member khác | MEM002 xem MEM007 | Không được phép xem |

### IDM — Thành viên và hồ sơ mượn (REQ-07, REQ-08)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò thêm member | Librarian (hợp lệ) | LIB001 | Cho phép tạo member |
| | Member thường | MEM001 | Không cho phép thêm member  |
| Họ tên | Không rỗng | "Nguyen Van A" | Chấp nhận |
| | Rỗng | "" | Từ chối bắt buộc nhập |
| Email format | Có '@' và '.' ở domain (Hợp lệ) | user@domain.com | Tạo thành công |
| | Thiếu "." ở domain | user@domaincom | Báo lỗi |
| | Thiếu '@' | userdomain.com | Báo lỗi |
| | Thiếu domain | user@.com | Báo lỗi |
| Email trùng lặp  | Email chưa tồn tại | newuser@domain.com | Cho phép tạo |
| | Email đã tồn tại | existing@domain.com | Báo lỗi |
| Số điện thoại | Đúng định dạng | 0987665432 | Chấp nhận |
| | Sai định dang | abc123 | Báo lỗi |
| Quyền xem borrow record | Librarian | LIB001 | Xem tất cả records |
| | Member xem record của chính mình  | MEM001 | Chỉ được xem records của MEM001 |
| | Member xem records của member khác | MEM001 xem MEM004 | Không cho phép |
| Trạng thái borrow record | Borowwing | BR001 | Hiển thị đúng trạng thái |
| | Returned | BR002 | Hiển thị đúng trạng thái |
| | Overdue | BR003 | Hiển thị đúng trạng thái |


> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-01 | Đăng nhập thành công với tài khoản hợp lệ | Tài khoản tồn tại | 1. Mở màn hình login 2. Nhập email/password 3. Nhấn Login | ba.nguyen@email.com / password123 | Đăng nhập thành công | REQ-01 | EP |
| TC-02 | Đăng nhập sai tài khoản | Tài khoản tồn tại | Thực hiện login | binh.pham12@email.com / password123 | Hiển thị "Không tìm thấy thành viên" | REQ-01 | EP |
| TC-03 | Đăng nhập sai mật khẩu | Tài khoản tồn tại | Thực hiện login | binh.pham@email.com / passwork123 | Hiển thị " Mật khẩu không đúng " | REQ-01 | EP |
| TC-04 | Kiểm tra rỗng | Không | Để trống email/password rồi login | " " / " " | Hiển thị "Vui lòng nhập email và mật khẩu" | REQ-01 | BVA |
| TC-05 | Hiển thị danh sách sách | Đã đăng nhập | Chọn “View Books” | None | Danh sách sách hiển thị | REQ-02 | Functional |
| TC-06 | Khi sách đượn mượn/trả | Đã đăng nhập | Chọn “View Books” | None | Trạng thái cập nhật ngay lập tức | REQ-02 | Functional |
| TC-07 | Tìm kiếm sách theo tên hợp lệ | Có dữ liệu sách | Nhập tên sách vào ô search | “Python” | Hiển thị sách liên quan | REQ-03 | EP |
| TC-08 | Tìm kiếm sách theo tên hợp lệ | Có dữ liệu sách | Nhập tên sách vào ô search | “python” | Hiển thị sách liên quan | REQ-03 | EP |
| TC-09 | Tìm kiếm sách không tồn tại | Có dữ liệu sách | Search sách | “ABCXYZ” | Không tìm thấy kết quả | REQ-03 | EP |
| TC-10 | Lọc sách Available | Có sách nhiều trạng thái | Chọn filter Available | Trạng thái = Available | Chỉ hiển thị sách Available | REQ-03 | Decision Table |
| TC-11 | Mượn sách thành công | Member active, sách Available | Chọn Borrow | MEM001 + BOOK001 | Borrow thành công | REQ-04 | EP |
| TC-12 | Từ chối mượn sách đã Borrowed | BOOK003 đang được mượn | Borrow BOOK003 | MEM001 + BOOK003 | Từ chối mượn | REQ-04 | EP |
| TC-13 | Kiểm tra giới hạn mượn = 3 | Member đã mượn 3 sách | Borrow thêm sách | borrowCount = 3 | Báo vượt giới hạn | REQ-04 | BVA |
| TC-14 | Kiểm tra trạng thái thành viên | Member, sách available | Borrow sách | Member expired | Báo thành viên bị hết hạn | REQ-04 | BVA |
| TC-15 | Kiểm tra trạng thái thành viên | Member, sách available | Borrow sách | Member suspended | Báo thành viên bị tạm ngưng | REQ-04 | BVA |
| TC-16 | Trả sách thành công | Member đang borrow sách | Chọn Return | MEM003 | Return thành công, sách Available | REQ-05 | EP |
| TC-17 | Trả sách không thuộc member | Member không borrow sách đó | Return book | MEM001 trả BOOK007 | Từ chối trả sách | REQ-05 | EP |
| TC-18 | Trả sách quá hạn | Sách overdue | Return book | returnDate > dueDate | Hiển thị overdue warning | REQ-05 | BVA |
| TC-19 | Kiểm tra overdue với dueDate = currentDate | Có borrow record | Nhấn “Check Overdue" | dueDate = today | Đánh dấu Overdue | REQ-06 | BVA |
| TC-20 | Librarian xem tất cả overdue records | Login Librarian | Check Overdue | LIB001 | Hiển thị toàn bộ overdue records  | REQ-06 | Authorization  |
| TC-21 | Member chỉ xem overdue của mình  | Login Member | Check Overdue | MEM002 | Chỉ hiển thị overdue của MEM002 | REQ-06 | Authorization |
| TC-22 | Thêm member với email hợp lệ | Login Librarian | Add Member | [user@domain.com](mailto:user@domain.com) | Tạo member thành công | REQ-07 | EP |
| TC-23 | Thêm member với email thiếu '.' | Login Librarian | Add Member | user@domain | Báo lỗi email | REQ-07 | EP |
| TC-24 | Thêm member với email trùng | Email đã tồn tại | Add Member | [existing@gmail.com](mailto:existing@gmail.com) | Báo lỗi duplicate email | REQ-07 | EP |
| TC-25 | Librarian xem toàn bộ borrow records| Login Librarian | Open Borrow Records | LIB001 | Hiển thị tất cả records | REQ-08 | Authorization |
| TC-26 | Member xem borrow record của người khác | Login Member | Tra cứu record | MEM002 xem MEM003 | Từ chối truy cập | REQ-08 | Authorization |
| TC-27 | Hiển thị đúng trạng thái record | Có record Đang mượn | Mở borrow record | BR003 | Hiển thị “Đang mượn” | REQ-08 | State Testing |
| TC-28 | Hiển thị đúng trạng thái record | Có record "Đã trả" | Mở borrow record | BR004 | Hiển thị “Đã trả” | REQ-08 | State Testing |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
| ------------------------ | ------ | ------------------- | ------------------------------------------------------------------------ |
| Đăng nhập hệ thống | 4 | REQ-01 | EP, BVA |
| Xem danh sách sách | 2 | REQ-02 | Functional Testing |
| Tìm kiếm & lọc sách | 4 | REQ-03 | EP, Decision Table |
| Mượn sách | 5 | REQ-04 | EP, BVA |
| Trả sách | 3 | REQ-05 | EP, BVA, State Transition |
| Kiểm tra & xử lý quá hạn | 3 | REQ-06 | BVA, Authorization |
| Quản lý thành viên | 3 | REQ-07 | EP, Validation Testing |
| Tra cứu phiếu mượn | 4 | REQ-08 | Authorization, State Testing |

| **Tổng**  | **28** | **REQ-01 → REQ-08** | **EP, BVA, Decision Table, Authorization, State Transition, Validation** |
