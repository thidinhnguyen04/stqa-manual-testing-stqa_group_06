<img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/2f3e5da9-ecb9-4059-9749-3340f4c12aec" /># Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_06 |
| **Ngày thực thi** | 19/05/2026 |
| **Trình duyệt** | Chrome 148 |
| **Hệ điều hành** | macOS |

---

## Kết quả chi tiết

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-01 | Login | User logs in successfully with valid credentials | Login successful and dashboard displayed | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/7b3eab0a-11a3-424d-8a8d-dc5aa68ef0ba" />
 | None |
| TC-02 | Login | Display "Member not found" message | Correct error message displayed | Pass | Screenshot of error message | None |
| TC-03 | Login | Display "Incorrect password" message | Correct error message displayed | Pass | Screenshot of error message | None |
| TC-04 | Login Validation | Display validation for empty fields | Validation message displayed correctly | Pass | Screenshot of validation popup/message | None |
| TC-05 | Book Management | Book list displayed successfully | Book list loaded correctly | Pass | Screenshot of book list page | None |
| TC-06 | Book Management | Book status updates immediately after borrow/return | Status updated correctly | Pass | Screenshot before and after status change | None |
| TC-07 | Search | Correct book displayed when searching by title | BOOK001 displayed correctly | Pass | Screenshot of search result | None |
| TC-08 | Search | Correct book displayed when searching by author | BOOK002 displayed correctly | Pass | Screenshot of search result | None |
| TC-09 | Search & Filter | Correct filtered result displayed | BOOK002 displayed correctly | Pass | Screenshot of filtered result | None |
| TC-10 | Search | Search is case-insensitive | Same result returned for "Python" and "python" | Pass | Screenshot of both search results | None |
| TC-11 | Search | No result displayed for non-existent keyword | No results shown | Pass | Screenshot of empty result | None |
| TC-12 | Search | System supports search without Vietnamese accents | No book displayed  | Fail | Screenshot of search result | None |
| TC-13 | Borrow Book | Borrow request succeeds | Book borrowed successfully | Pass | Screenshot of borrow confirmation | None |
| TC-14 | Borrow Book | Reject borrowing already borrowed book | Borrow rejected correctly | Pass | Screenshot of warning message | None |
| TC-15 | Borrow Limit | Allow borrowing the 3rd book | Borrow successful | Pass | Screenshot of borrow record | None |
| TC-16 | Borrow Limit | Reject borrowing the 4th book | Borrow successfully | Fail | Screenshot of  message | None |
| TC-17 | Session Security | Redirect expired session to login page | User redirected correctly | Pass | Screenshot of login redirect | None |
| TC-18 | Member Validation | Notify expired member account | Correct notification displayed | Pass | Screenshot of notification | None |
| TC-19 | Member Validation | Notify suspended member account | Correct notification displayed | Pass | Screenshot of notification | None |
| TC-20 | Return Book | Return succeeds and book becomes available | Return processed correctly | Pass | Screenshot of updated status | None |
| TC-21 | Return Book | Reject invalid return request | Return rejected correctly | Pass | Screenshot of error message | None |
| TC-22 | Overdue Handling | Display overdue warning | Warning displayed correctly | Pass | Screenshot of overdue warning | None |
| TC-23 | Overdue Check | Record not marked overdue when dueDate = today | System incorrectly marks record as Overdue | Fail | Screenshot of overdue status | BUG-03 |
| TC-24 | Authorization | Librarian can view all overdue records | All overdue records displayed | Pass | Screenshot of overdue records page | None |
| TC-25 | Authorization | Member only views own overdue records | Only member records displayed | Pass | Screenshot of member overdue page | None |
| TC-26 | Member Management | Member created successfully | Member added successfully | Pass | Screenshot of created member | None |
| TC-27 | Member Management | Display email validation error | Validation displayed correctly | Pass | Screenshot of validation message | None |
| TC-28 | Member Management | Reject duplicate email | Duplicate email error displayed | Pass | Screenshot of error message | None |
| TC-29 | Borrow Records | Librarian views all borrow records | All records displayed correctly | Pass | Screenshot of borrow records page | None |
| TC-30 | Authorization | Reject unauthorized record access | Access denied displayed | Pass | Screenshot of access denied message | None |
| TC-31 | Record Status | Display status "Borrowing" correctly | Status displayed correctly | Pass | Screenshot of record status | None |
| TC-32 | Record Status | Display status "Returned" correctly | Status displayed correctly | Pass | Screenshot of record status | None |
| TC-33 | Record Status | Display status "Overdue" correctly | Status displayed correctly | Pass | Screenshot of record status | None |


## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 33 |
| Pass | 30 |
| Fail | 3 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 90.9% |

### Kết quả theo nhóm chức năng

| Functional Group | Total TC | Pass | Fail | Pass Rate |
|---|---|---|---|---|
| Login | 4 | 4 | 0 | 100% |
| Book Management | 2 | 2 | 0 | 100% |
| Search | 6 | 5 | 1 | 83.33% |
| Borrow Book | 7 | 6 | 1 | 85.71% |
| Return Book | 3 | 3 | 0 | 100% |
| Overdue Management | 3 | 2 | 1 | 66.7% |
| Member Management | 3 | 3 | 0 | 100% |
| Borrow Records | 5 | 5 | 0 | 100% |
| Total | 33 | 30 | 3 | 90.9% |
