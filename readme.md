# Acceptance Criteria & Definition of Done cho User Story

## 1. Phạm vi và giả định

Bài làm xây dựng Acceptance Criteria (AC) cho ba User Story của hệ thống
thư viện cho mượn sách giấy. Mỗi AC mô tả hành vi có thể kiểm tra từ góc
nhìn người dùng theo Given--When--Then.

**Các giả định cần Product Owner (PO) xác nhận:**

-   **Giả định 1:** Mỗi độc giả được có tối đa 5 cuốn sách đang mượn
    cùng lúc. Sách đã đặt nhưng chưa nhận chưa được tính là sách đang
    mượn; tuy nhiên, mỗi độc giả chỉ được có tối đa 2 yêu cầu đặt mượn
    đang còn hiệu lực.
-   **Giả định 2:** Khi yêu cầu đặt mượn được chấp nhận, thư viện giữ
    sách trong 48 giờ kể từ thời điểm xác nhận đặt thành công.
-   **Giả định 3:** Một bản sách chỉ có thể được giữ cho một yêu cầu đặt
    mượn còn hiệu lực tại một thời điểm.
-   **Giả định 4:** Thông báo được gửi khi sách đã đặt trước sẵn sàng để
    nhận; nếu gửi thông báo thất bại thì hệ thống ghi nhận trạng thái
    gửi thất bại để có thể kiểm tra và xử lý theo quy trình vận hành
    hiện có. Việc gửi lại tự động cần PO xác nhận nếu muốn đưa vào phạm
    vi.

> Các giả định chỉ dùng để hoàn thiện bài tập, không được xem là yêu cầu
> chính thức cho đến khi PO xác nhận.

------------------------------------------------------------------------

## 2. Acceptance Criteria

## Story 1: Đặt mượn online một cuốn sách đang có sẵn

**User Story:** Là một độc giả, tôi muốn đặt mượn online một cuốn sách
đang có sẵn để tôi không mất công đến thư viện rồi mới biết sách đã có
người mượn.

  --------------------------------------------------------------------------
  AC#            Loại           Given          When           Then
  -------------- -------------- -------------- -------------- --------------
  S1-AC1         Happy path     Độc giả đã     Độc giả chọn   Hệ thống xác
                                đăng nhập,     đặt mượn cuốn  nhận đặt mượn
                                không vượt quá sách đó        thành công,
                                giới hạn đặt                  hiển thị thông
                                mượn và cuốn                  tin sách và
                                sách còn bản                  thời hạn nhận
                                có thể đặt                    sách là 48 giờ
                                                              kể từ lúc xác
                                                              nhận

  S1-AC2         Negative       Độc giả đang   Độc giả chọn   Hệ thống từ
                                xem một cuốn   đặt mượn cuốn  chối yêu cầu
                                sách nhưng     sách đó        và hiển thị
                                không còn bản                 thông báo rằng
                                nào có thể đặt                sách hiện
                                mượn                          không có sẵn
                                                              để đặt mượn

  S1-AC3         Edge case      Độc giả đang   Độc giả gửi    Hệ thống không
                                xem một cuốn   yêu cầu đặt    xác nhận đặt
                                sách có đúng 1 mượn cuốn sách mượn cho độc
                                bản còn có thể đó             giả hiện tại
                                đặt, nhưng bản                và hiển thị
                                đó vừa được                   thông báo rằng
                                giữ thành công                sách vừa không
                                cho độc giả                   còn sẵn có
                                khác trước khi                
                                yêu cầu của                   
                                độc giả hiện                  
                                tại được xác                  
                                nhận                          

  S1-AC4         Ràng buộc      Độc giả đã có  Độc giả gửi    Hệ thống từ
                 nghiệp vụ      2 yêu cầu đặt  yêu cầu đặt    chối yêu cầu
                                mượn đang còn  mượn thêm một  mới và thông
                                hiệu lực, theo cuốn sách đang báo rằng độc
                                Giả định 1     có sẵn         giả đã đạt
                                                              giới hạn 2 yêu
                                                              cầu đặt mượn
                                                              đang còn hiệu
                                                              lực
  --------------------------------------------------------------------------

### Câu hỏi làm rõ cho PO --- Story 1

1.  Một độc giả được có tối đa bao nhiêu yêu cầu đặt mượn đang còn hiệu
    lực cùng lúc?
2.  Thời hạn giữ sách 48 giờ bắt đầu từ lúc đặt thành công hay từ lúc
    độc giả nhận thông báo?
3.  Nếu độc giả không đến nhận trong 48 giờ, yêu cầu có tự hết hạn và
    bản sách được trả về trạng thái sẵn có không?

------------------------------------------------------------------------

## Story 2: Nhận thông báo khi sách đặt trước đã có sẵn

**User Story:** Là một độc giả, tôi muốn nhận thông báo khi sách tôi đặt
trước đã có sẵn để tôi kịp đến nhận sách trước khi hết thời gian giữ
chỗ.

**Giả định bổ sung:** Trong phạm vi bài tập, "đặt trước" được hiểu là
độc giả đã có một yêu cầu đặt mượn hợp lệ đang chờ sách sẵn có. Khi sách
sẵn sàng để nhận, thời hạn giữ sách 48 giờ được áp dụng theo quy định
chung của bài toán.

  --------------------------------------------------------------------------
  AC#            Loại           Given          When           Then
  -------------- -------------- -------------- -------------- --------------
  S2-AC1         Happy path     Độc giả có yêu Hệ thống ghi   Độc giả nhận
                                cầu đặt trước  nhận sách      được thông báo
                                hợp lệ và sách chuyển sang    cho biết sách
                                đã sẵn sàng để trạng thái sẵn đã sẵn sàng,
                                nhận           sàng để nhận   nơi nhận sách
                                               cho yêu cầu đó và thời hạn
                                                              nhận trong 48
                                                              giờ

  S2-AC2         Negative       Độc giả có yêu Độc giả kiểm   Hệ thống hiển
                                cầu đặt trước  tra trạng thái thị rằng sách
                                nhưng sách vẫn yêu cầu đặt    chưa sẵn sàng
                                chưa sẵn sàng  trước          và không thông
                                để nhận                       báo rằng độc
                                                              giả có thể đến
                                                              nhận sách

  S2-AC3         Edge case      Độc giả có yêu Hệ thống xử lý Độc giả chỉ
                                cầu đặt trước  sự kiện sách   nhận một thông
                                hợp lệ và sách sẵn sàng để    báo cho lần
                                vừa chuyển     nhận           chuyển trạng
                                sang trạng                    thái đó, không
                                thái sẵn sàng                 nhận các thông
                                để nhận                       báo trùng lặp
                                                              cho cùng một
                                                              sự kiện

  S2-AC4         Edge case      Độc giả có yêu Hệ thống ghi   Độc giả không
                                cầu đặt trước  nhận sách sẵn  nhận thông báo
                                nhưng yêu cầu  sàng để nhận   nhận sách cho
                                đã hết hiệu                   yêu cầu đã hết
                                lực trước khi                 hiệu lực
                                sách sẵn sàng                 
  --------------------------------------------------------------------------

### Câu hỏi làm rõ cho PO --- Story 2

1.  Thông báo được gửi qua kênh nào: thông báo trong hệ thống, email,
    SMS hay nhiều kênh?
2.  "Sách đã có sẵn" nghĩa là sách đã được trả về thư viện và sẵn sàng
    để giữ cho độc giả, hay chỉ cần có bản sách trong kho?
3.  Nếu gửi thông báo thất bại, nhóm cần thử gửi lại tự động hay chỉ ghi
    nhận lỗi để nhân viên xử lý?
4.  Thời hạn 48 giờ bắt đầu từ thời điểm sách sẵn sàng, thời điểm đặt
    giữ thành công hay thời điểm thông báo được gửi?

------------------------------------------------------------------------

## Story 3: Giới hạn số sách một độc giả được mượn cùng lúc

**User Story:** Là một thủ thư, tôi muốn giới hạn số sách một độc giả
được mượn cùng lúc để tránh tình trạng một người giữ hết sách.

**Giả định nghiệp vụ:** Mỗi độc giả được mượn tối đa **5 cuốn sách đang
mượn cùng lúc**. Đây là giới hạn tạm đặt cho bài tập và cần PO xác nhận.

  --------------------------------------------------------------------------
  AC#            Loại           Given          When           Then
  -------------- -------------- -------------- -------------- --------------
  S3-AC1         Happy path     Độc giả đang   Thủ thư xác    Hệ thống chấp
                                mượn 3 cuốn    nhận cho độc   nhận giao dịch
                                sách và không  giả mượn thêm  và số sách
                                có hạn chế     1 cuốn         đang mượn của
                                mượn khác                     độc giả tăng
                                                              lên 4

  S3-AC2         Negative       Độc giả đang   Thủ thư xác    Hệ thống từ
                                mượn 5 cuốn    nhận cho độc   chối giao dịch
                                sách, bằng     giả mượn thêm  và thông báo
                                giới hạn tối   1 cuốn         độc giả đã đạt
                                đa                            giới hạn 5
                                                              cuốn đang mượn

  S3-AC3         Edge case      Độc giả đang   Thủ thư xác    Hệ thống chấp
                                mượn 4 cuốn    nhận cho độc   nhận giao dịch
                                sách, tức còn  giả mượn thêm  và số sách
                                đúng 1 suất    1 cuốn         đang mượn của
                                trước khi đạt                 độc giả là 5,
                                giới hạn                      không vượt
                                                              giới hạn

  S3-AC4         Ràng buộc      Độc giả đang   Thủ thư xác    Hệ thống chấp
                 nghiệp vụ      mượn 5 cuốn    nhận cho độc   nhận giao dịch
                                sách và trả    giả mượn thêm  nếu các điều
                                lại thành công 1 cuốn         kiện mượn khác
                                1 cuốn                        đều được đáp
                                                              ứng và số sách
                                                              đang mượn sau
                                                              giao dịch là 5
  --------------------------------------------------------------------------

### Câu hỏi làm rõ cho PO --- Story 3

1.  Giới hạn tối đa là bao nhiêu cuốn mỗi độc giả? Có khác nhau theo
    loại độc giả không?
2.  Sách đang được giữ chờ nhận có được tính vào giới hạn mượn không?
3.  Sách quá hạn hoặc sách chưa được ghi nhận trả có tiếp tục được tính
    là sách đang mượn không?
4.  Khi độc giả đạt giới hạn, hệ thống chỉ chặn giao dịch mượn mới hay
    thủ thư có quyền ghi đè trong trường hợp ngoại lệ?

------------------------------------------------------------------------

## 3. Definition of Done (DoD) chung của nhóm

DoD dưới đây áp dụng cho **mọi Product Backlog Item (PBI)** được xem là
Done, bao gồm cả ba User Story trong bài. DoD không thay thế Acceptance
Criteria; mỗi PBI cần đáp ứng AC riêng và toàn bộ tiêu chuẩn chất lượng
chung này.

-   [ ] **Acceptance Criteria đạt yêu cầu:** Tất cả AC của PBI đã được
    kiểm tra và đáp ứng.
-   [ ] **Code hoàn thành:** Thay đổi đã được triển khai đầy đủ theo
    phạm vi của PBI, không còn phần triển khai dang dở.
-   [ ] **Code review hoàn tất:** Code đã được ít nhất một thành viên
    khác review và các góp ý bắt buộc đã được xử lý.
-   [ ] **Kiểm thử thành công:** Các bài kiểm thử phù hợp, bao gồm kiểm
    thử hồi quy liên quan, đã chạy thành công.
-   [ ] **Không còn lỗi nghiêm trọng đã biết:** Không còn lỗi nghiêm
    trọng hoặc lỗi chặn phát hành chưa được xử lý trong phạm vi PBI.
-   [ ] **Tích hợp thành công:** Thay đổi đã được tích hợp vào nhánh
    chung của nhóm và không gây lỗi tích hợp đã biết.
-   [ ] **Bảo mật và quyền truy cập được kiểm tra:** Các thay đổi không
    làm lộ dữ liệu nhạy cảm và tuân thủ quyền truy cập phù hợp.
-   [ ] **Tài liệu được cập nhật khi cần:** Tài liệu người dùng hoặc tài
    liệu kỹ thuật liên quan đã được cập nhật nếu PBI làm thay đổi hành
    vi hoặc cách sử dụng sản phẩm.
-   [ ] **Có thể kiểm chứng trong môi trường phù hợp:** Chức năng đã
    được xác minh trong môi trường kiểm thử hoặc môi trường được nhóm
    thống nhất trước khi tuyên bố Done.

### Minh họa DoD với ba Story

-   **Story 1 --- Đặt mượn online:** Ngoài việc đáp ứng các AC về đặt
    thành công, sách hết và giới hạn đặt, thay đổi còn phải qua review
    và kiểm thử.
-   **Story 2 --- Thông báo sách sẵn sàng:** Ngoài việc đáp ứng các AC
    về nội dung và điều kiện gửi thông báo, chức năng phải qua kiểm thử
    và được tích hợp thành công.
-   **Story 3 --- Giới hạn số sách:** Ngoài việc đáp ứng các AC về giới
    hạn 5 cuốn theo giả định, thay đổi phải được review và kiểm thử các
    trường hợp ngay dưới, đúng bằng và vượt giới hạn.

------------------------------------------------------------------------

## 4. Story 1 đã Done chưa?

**Chưa.** Dù Story 1 đã đáp ứng tất cả Acceptance Criteria, code vẫn
chưa được review theo DoD chung của nhóm. Vì vậy, Story 1 chưa đáp ứng
đầy đủ Definition of Done và chưa được xem là Done.

------------------------------------------------------------------------

## 5. Kết luận

Acceptance Criteria xác định điều kiện chấp nhận riêng của từng User
Story và mô tả hành vi quan sát được từ góc nhìn người dùng. Definition
of Done là tiêu chuẩn chất lượng chung của nhóm, áp dụng cho mọi PBI;
một Story chỉ được xem là Done khi vừa đáp ứng AC của nó, vừa đáp ứng
DoD chung.
