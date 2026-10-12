# Viết Acceptance Criteria & Definition of Done cho User Story

## 1. Giả định

Do đề bài chưa cung cấp đầy đủ quy tắc nghiệp vụ, bài làm sử dụng các
giả định dưới đây để viết AC cụ thể. Các giả định cần được Product Owner
(PO) xác nhận trước khi triển khai:

- **Giả định 1 -- US1:** Thư viện giữ sách trong 48 giờ kể từ thời
  điểm yêu cầu đặt mượn được xác nhận thành công.
- **Giả định 2 -- US2:** Khi sách đặt trước sẵn sàng để nhận, độc giả
  được thông báo và có 48 giờ để đến nhận.
- **Giả định 3 -- US3:** Mỗi độc giả được mượn tối đa 5 cuốn sách cùng
  lúc.
- **Giả định 4 -- US2:** Một sự kiện sách sẵn sàng cho một yêu cầu đặt
  trước chỉ tạo ra một thông báo; không gửi thông báo trùng lặp cho
  cùng sự kiện.

## 2. Acceptance Criteria

### Story 1: Đặt mượn sách trực tuyến

**User Story:** Là một độc giả, tôi muốn đặt mượn online một cuốn sách
đang có sẵn để tôi không mất công đến thư viện rồi mới biết sách đã có
người mượn.

| Story | AC# | Loại       | Given                                                                                        | When                               | Then                                                                                               |
| ----- | --- | ---------- | -------------------------------------------------------------------------------------------- | ---------------------------------- | -------------------------------------------------------------------------------------------------- |
| US1   | AC1 | Happy path | Độc giả đã đăng nhập và sách còn bản có thể đặt mượn.                                        | Độc giả gửi yêu cầu đặt mượn sách. | Hệ thống xác nhận đặt mượn thành công và hiển thị thời hạn nhận sách là 48 giờ kể từ lúc xác nhận. |
| US1   | AC2 | Negative   | Sách không còn bản nào có thể đặt mượn.                                                      | Độc giả gửi yêu cầu đặt mượn sách. | Hệ thống từ chối yêu cầu và thông báo sách hiện không có sẵn.                                      |
| US1   | AC3 | Edge case  | Sách chỉ còn một bản có thể đặt mượn, nhưng bản đó vừa được giữ thành công cho độc giả khác. | Độc giả gửi yêu cầu đặt mượn sách. | Hệ thống từ chối yêu cầu và thông báo sách vừa không còn sẵn có.                                   |

---

#### Câu hỏi làm rõ cho PO --- Story 1

1.  Thời hạn giữ sách 48 giờ bắt đầu từ lúc yêu cầu đặt mượn được xác
    nhận hay từ lúc độc giả nhận thông báo?
2.  Khi hết 48 giờ mà độc giả chưa đến nhận, yêu cầu có tự hết hạn và
    sách được trả về trạng thái sẵn có không?

### Story 2: Nhận thông báo khi sách đặt trước đã có sẵn

**User Story:** Là một độc giả, tôi muốn nhận thông báo khi sách tôi đặt
trước đã có sẵn để tôi kịp đến nhận sách trước khi hết thời gian giữ
chỗ.

| Story | AC# | Loại       | Given                                                            | When                                               | Then                                                                                  |
| ----- | --- | ---------- | ---------------------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------- |
| US2   | AC1 | Happy path | Độc giả có yêu cầu đặt trước hợp lệ và sách đã sẵn sàng để nhận. | Hệ thống ghi nhận sách sẵn sàng để nhận.           | Độc giả nhận thông báo sách đã sẵn sàng và thời hạn nhận là 48 giờ.                   |
| US2   | AC2 | Negative   | Độc giả có yêu cầu đặt trước nhưng sách chưa sẵn sàng.           | Độc giả kiểm tra trạng thái yêu cầu.               | Hệ thống hiển thị sách chưa sẵn sàng và không thông báo rằng độc giả có thể đến nhận. |
| US2   | AC3 | Edge case  | Độc giả đã nhận thông báo sách sẵn sàng cho yêu cầu đặt trước.   | Hệ thống tiếp nhận lại cùng sự kiện sách sẵn sàng. | Độc giả không nhận thêm thông báo trùng lặp cho cùng sự kiện.                         |

---

#### Câu hỏi làm rõ cho PO --- Story 2

1.  Thông báo được gửi qua kênh nào: thông báo trong hệ thống, email hay
    SMS?
2.  Nếu gửi thông báo thất bại, hệ thống có cần tự động thử gửi lại
    không?
3.  Thời hạn 48 giờ bắt đầu từ khi sách sẵn sàng, khi yêu cầu giữ sách
    được xác nhận hay khi thông báo được gửi?

### Story 3: Giới hạn số sách một độc giả được mượn cùng lúc

**User Story:** Là một thủ thư, tôi muốn giới hạn số sách một độc giả
được mượn cùng lúc để tránh tình trạng một người giữ hết sách.

**Giả định nghiệp vụ:** Mỗi độc giả được mượn tối đa 5 cuốn sách cùng
lúc. Giới hạn này cần được PO xác nhận.

| Story | AC# | Loại                | Given                                                        | When                                   | Then                                                                                                        |
| ----- | --- | ------------------- | ------------------------------------------------------------ | -------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| US3   | AC1 | Happy path          | Độc giả đang mượn 3 cuốn sách và không có hạn chế mượn khác. | Thủ thư xác nhận cho mượn thêm 1 cuốn. | Hệ thống chấp nhận giao dịch và tổng số sách đang mượn tăng lên 4 cuốn.                                     |
| US3   | AC2 | Negative            | Độc giả đang mượn 5 cuốn sách.                               | Thủ thư xác nhận cho mượn thêm 1 cuốn. | Hệ thống từ chối giao dịch và thông báo độc giả đã đạt giới hạn.                                            |
| US3   | AC3 | Edge case           | Độc giả đang mượn 4 cuốn sách.                               | Thủ thư xác nhận cho mượn thêm 1 cuốn. | Hệ thống chấp nhận giao dịch và tổng số sách đang mượn là 5 cuốn.                                           |
| US3   | AC4 | Ràng buộc nghiệp vụ | Độc giả đang mượn 5 cuốn và đã trả thành công 1 cuốn.        | Thủ thư xác nhận cho mượn thêm 1 cuốn. | Hệ thống chấp nhận giao dịch nếu các điều kiện mượn khác được đáp ứng, và tổng số sách đang mượn là 5 cuốn. |

---

#### Câu hỏi làm rõ cho PO --- Story 3

1.  Giới hạn tối đa mỗi độc giả được mượn cùng lúc có phải là 5 cuốn
    không?
2.  Giới hạn này có áp dụng giống nhau cho mọi loại độc giả không?
3.  Sách đã đặt mượn nhưng chưa đến nhận có được tính vào giới hạn sách
    đang mượn không?

## 3. Definition of Done (DoD) chung của nhóm

DoD này áp dụng chung cho **mọi Product Backlog Item (PBI)**, không chỉ
riêng ba User Story trong bài. Các tiêu chí dưới đây là tiêu chuẩn chất
lượng chung, không thay thế Acceptance Criteria của từng Story.

- [ ] **Code hoàn chỉnh:** Phần thay đổi thuộc phạm vi PBI đã được
      triển khai đầy đủ, không còn phần code dang dở.
- [ ] **Code review:** Code đã được ít nhất một thành viên khác review
      và các góp ý bắt buộc đã được xử lý.
- [ ] **Kiểm thử đạt:** Các bài kiểm thử phù hợp đã chạy thành công;
      không có bài kiểm thử bắt buộc nào thất bại.
- [ ] **Không còn lỗi nghiêm trọng đã biết:** Không còn lỗi nghiêm
      trọng hoặc lỗi chặn phát hành chưa được xử lý trong phạm vi PBI.
- [ ] **Tích hợp thành công:** Thay đổi đã được tích hợp vào nhánh
      chung của nhóm mà không gây lỗi tích hợp đã biết.
- [ ] **Bảo mật được xem xét:** Thay đổi tuân thủ các yêu cầu bảo mật
      và quyền truy cập liên quan; không làm lộ dữ liệu nhạy cảm.
- [ ] **Tài liệu được cập nhật khi cần:** Tài liệu liên quan được cập
      nhật nếu thay đổi ảnh hưởng đến cách sử dụng hoặc bảo trì sản phẩm.
- [ ] **Được xác minh trong môi trường phù hợp:** Thay đổi đã được
      kiểm tra trong môi trường kiểm thử hoặc môi trường được nhóm thống
      nhất.
- [ ] **Có thể trình diễn:** Nhóm có thể trình diễn hoặc xác minh kết
      quả của PBI trong môi trường phù hợp.

## 4. Story 1 đã được coi là Done chưa?

**Chưa.** Dù Story 1 đã đáp ứng tất cả Acceptance Criteria, code vẫn
chưa được review theo DoD chung của nhóm. Vì vậy, Story 1 chưa đáp ứng
đầy đủ Definition of Done và chưa được xem là Done.

## 5. Kết luận

Acceptance Criteria mô tả các điều kiện chấp nhận riêng, có thể kiểm
tra, cho từng User Story. Definition of Done là tiêu chuẩn chất lượng
chung áp dụng cho mọi PBI; một Story chỉ được xem là Done khi đáp ứng
các điều kiện chấp nhận của chính Story đó và toàn bộ DoD của nhóm.
