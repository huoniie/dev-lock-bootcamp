### Session 06 - ỨNG DỤNG VÀ HỆ SINH THÁI WEB3
* **Student:** Chu Thị Hương
* **GitHub:** https://github.com/huoniie.git
* **Submitted:** 2026-11-18
* **Commit:** https://github.com/huoniie/dev-lock-bootcamp.git

---

#### 1. Summary

##### 1.1. Một dApp hoạt động như thế nào (Kiến trúc 4 lớp)
* **Khái niệm:** dApp (Decentralized Application) là ứng dụng có phần logic hoặc trạng thái được thực hiện bằng chương trình (smart contract) trên mạng blockchain. Giao diện người dùng vẫn có thể là trang web quen thuộc, kết hợp với máy chủ, cơ sở dữ liệu và dịch vụ bên thứ ba; mức độ phi tập trung cần xét riêng trên từng thành phần.
* **Bốn lớp cấu trúc chính:**
  1. *Frontend (Giao diện):* Hiển thị thông tin trực quan và tạo yêu cầu tương tác cho người dùng.
  2. *Wallet (Ví):* Nơi người dùng trực tiếp kiểm tra chi tiết giao dịch (tài khoản, mạng, phí gas ước tính) và dùng khóa bí mật để ký xác nhận.
  3. *Smart Contract (Hợp đồng thông minh):* Chứa toàn bộ quy tắc nghiệp vụ, điều kiện kiểm tra và quyền hạn thực thi.
  4. *Blockchain & RPC Node:* Cổng RPC (Remote Procedure Call) đưa lời gọi tới các nút mạng; blockchain thực thi giao dịch và ghi nhận thay đổi trạng thái vĩnh viễn vào sổ cái.
* **Hoạt động khi website tắt:** Nếu trang web bị sập hoặc ngừng hoạt động, dApp **vẫn có thể tiếp tục hoạt động** vì hợp đồng và trạng thái nằm trên mạng blockchain; người dùng vẫn có thể tương tác trực tiếp với hợp đồng qua giao diện khác hoặc công cụ như Etherscan, Remix. Tuy nhiên, khả năng hiển thị ảnh, metadata và các dịch vụ ngoài chuỗi có thể bị ảnh hưởng.

| Thứ tự | Lớp thành phần | Vai trò cốt lõi |
| :---: | :--- | :--- |
| **1** | **Frontend** | Hiển thị thông tin và chuẩn bị yêu cầu gọi hàm |
| **2** | **Wallet** | Cho phép người dùng kiểm tra thông tin, mạng và ký xác thực |
| **3** | **Smart Contract** | Lưu trữ mã lệnh, chứa quy tắc xử lý và kiểm tra điều kiện |
| **4** | **Blockchain** | Mạng lưới các node đồng thuận và ghi nhận trạng thái sổ cái |

##### 1.2. Đọc dữ liệu (Read) vs. Ghi dữ liệu (Write)
* **Đọc dữ liệu qua RPC (Read / `eth_call`):**
  * Truy vấn các thông tin đã lưu trên sổ cái (ví dụ: xem chủ sở hữu vé `#042`, kiểm tra `totalRegistered`).
  * Thực thi cục bộ qua node RPC mà không tạo giao dịch trên chuỗi.
  * Thường không cần chữ ký của ví và **không tốn phí gas mạng** (dù nhà cung cấp dịch vụ RPC có thể tính phí hạ tầng với nhà phát triển ứng dụng).
* **Ghi dữ liệu lên Blockchain (Write / Transact):**
  * Thực hiện hành động làm thay đổi trạng thái sổ cái (ví dụ: chuyển vé `#042`, gọi hàm `register()`).
  * Bắt buộc phải có chữ ký của chủ tài khoản có thẩm quyền.
  * Phải trả phí giao dịch (Transaction Fee) bằng coin gốc của mạng cho thợ đào / validator xử lý.

| Tiêu chí | Đọc qua RPC (Call) | Ghi lên Blockchain (Transact) |
| :--- | :--- | :--- |
| **Ví dụ minh họa** | Xem chủ vé `#042`, đọc `totalRegistered` | Chuyển vé `#042`, gọi `register()` |
| **Yêu cầu chữ ký ví** | Thường không cần | Bắt buộc người có thẩm quyền phải ký |
| **Phí mạng (Gas Fee)** | Lệnh `eth_call` không tạo giao dịch, không tốn gas | Giao dịch thực thi trên chuỗi có phí gas |
| **Kết quả tác động** | Trả về dữ liệu để hiển thị | Làm thay đổi trạng thái dữ liệu trên sổ cái |

##### 1.3. Các thao tác phân quyền trên ví: Connect, Sign và Approve
Người dùng tương tác với Web3 qua 3 cấp độ ủy quyền cần phân biệt rõ ràng:
* **Connect Wallet (Kết nối ví):**
  * Chia sẻ địa chỉ ví công khai được chọn và mạng blockchain đang dùng cho website để hiển thị thông tin.
  * **Chưa hề cấp quyền chuyển tài sản.** Tuy nhiên, địa chỉ ví có thể liên kết với toàn bộ lịch sử giao dịch công khai của người dùng.
* **Sign Message (Ký thông điệp):**
  * Ký một đoạn thông điệp văn bản ngoài chuỗi (off-chain) bằng khóa bí mật để xác thực quyền kiểm soát ví (thường dùng khi đăng nhập).
  * Không tốn phí gas mạng. Tuy nhiên, một số loại chữ ký thông điệp chuẩn (như **Permit**) có thể được giao thức sử dụng để cấp quyền chi tiêu hoặc hoàn tất giao dịch rút tài sản sau đó; do đó không thấy phí không có nghĩa là luôn an toàn.
* **Approve Token (Cấp hạn mức chi tiêu - Allowance):**
  * Cấp quyền cho một địa chỉ hợp đồng (Spender) được phép tự động khấu trừ một lượng token nhất định từ ví của người dùng.
  * *Nguyên tắc an toàn then chốt:* **Ngắt kết nối website KHÔNG tự động thu hồi quyền đã approve trên chuỗi.** Quyền chi tiêu được ghi nhận trực tiếp trên smart contract của token; muốn điều chỉnh hoặc hủy bỏ bắt buộc phải thực hiện giao dịch thu hồi (Revoke / set allowance về 0).

| Thao tác | Ý nghĩa bản chất | Điều bắt buộc phải kiểm tra |
| :--- | :--- | :--- |
| **Connect Wallet** | Chia sẻ địa chỉ ví công khai và mạng đang kết nối | Kiểm tra đúng tên miền website chính thức |
| **Sign Message** | Ký xác nhận nội dung thông điệp ngoài chuỗi | Đọc kỹ nội dung, thời hạn và quyền phát sinh (như Permit) |
| **Approve Token** | Cấp hạn mức (Allowance) cho hợp đồng chi tiêu token | Kiểm tra địa chỉ hợp đồng Spender và số lượng hạn mức cấp |

##### 1.4. Vòng đời trạng thái của một giao dịch (Transaction Lifecycle)
Một giao dịch từ khi khởi tạo sẽ trải qua các giai đoạn:
1. *Chưa ký hoặc đã từ chối:* Người dùng chưa bấm chấp thuận trên ví, chưa có yêu cầu gửi lên mạng lưới.
2. *Pending (Đang chờ):* Giao dịch đã được ký và gửi đi qua cổng RPC, đã nhận được mã **Transaction Hash**, đang nằm trong hàng đợi chờ được đóng gói vào khối. Có mã hash chưa đồng nghĩa giao dịch đã thành công.
3. *Success (Thành công):* Giao dịch đã được ghi nhận vào khối và thực thi thành công mọi logic; trạng thái và sự kiện (Event) được cập nhật.
4. *Failed / Reverted (Thất bại):* Giao dịch bị hoàn nguyên do vi phạm điều kiện logic (như gặp lệnh `require`). Nếu giao dịch đã được đưa vào khối, người dùng **vẫn bị mất phí gas xử lý**.

##### 1.5. Các ứng dụng thường gặp trong hệ sinh thái Web3
* **DeFi (Tài chính phi tập trung):** Ứng dụng smart contract để thực hiện các chức năng trao đổi tài sản (Swap), vay và cho vay thông qua các bể thanh khoản (Liquidity Pool). Mức giá thực tế nhận được phụ thuộc vào quy mô giao dịch và độ sâu thanh khoản.
* **DAO (Tổ chức tự trị phi tập trung):** Mô hình quản trị cộng đồng bằng quy tắc mã hóa, tổ chức biểu quyết các đề xuất (Proposal) và quản lý quỹ chung. Cần lưu ý: một địa chỉ ví không đồng nghĩa với một con người, quyền biểu quyết có thể bị tập trung vào nhóm cá voi, và sở hữu token quản trị không mặc nhiên đồng nghĩa với việc nắm giữ cổ phần pháp lý của một công ty.
* **Oracle (Cầu nối dữ liệu ngoài chuỗi):** Blockchain là môi trường khép kín không thể tự biết các thông tin thực tế bên ngoài (như giá vàng, tỷ giá ngoại tệ, chuyến bay bị hủy). Oracle đóng vai trò thu thập và chuyển tiếp dữ liệu ngoại vi vào smart contract. Nếu dữ liệu oracle cung cấp bị sai, trễ hoặc quá cũ, smart contract dù chạy hoàn toàn đúng mã lệnh vẫn sẽ đưa ra phán quyết sai lệch.

##### 1.6. Hợp đồng thực hành mẫu: ClassroomSeat
* **Mục đích:** Quản lý danh sách đăng ký tham dự lớp học/ghế ngồi. Mỗi địa chỉ ví chỉ được đăng ký một lần duy nhất; hợp đồng không thu phí và không tạo NFT.
* **Cấu trúc mã nguồn Solidity:**
  * `mapping(address => bool) public registered;`: Bảng ánh xạ theo dõi trạng thái đã đăng ký của từng địa chỉ ví.
  * `uint256 public totalRegistered;`: Biến trạng thái đếm tổng số lượng người đã đăng ký thành công.
  * `event Registered(address indexed attendee, uint256 total);`: Ghi log sự kiện on-chain để ứng dụng frontend lắng nghe và cập nhật.
  * `require(!registered[msg.sender], "Already registered");`: Lệnh điều kiện chặn đăng ký trùng lặp nếu địa chỉ gọi hàm đã đăng ký trước đó.

---

#### 2. Topic notes

##### 2.1. Giải đáp câu hỏi kiểm tra cuối buổi & Bài tập nhóm

* **Bài tập nhóm: Vẽ đường đi của lệnh chuyển vé (4 ô quy trình):**
  1. *Frontend hiển thị gì:* Hiển thị thông tin chiếc vé (vé số `#042`), trạng thái sở hữu hiện tại và nút bấm "Chuyển vé" để người dùng nhập địa chỉ người nhận.
  2. *Ví yêu cầu người dùng xác nhận gì:* Ví hiển thị cửa sổ xác thực yêu cầu người dùng kiểm tra địa chỉ ví nhận, mạng đang kết nối, phí gas dự kiến và bấm "Ký/Xác nhận" bằng khóa bí mật.
  3. *Contract cần kiểm tra điều kiện nào:* Smart contract thực thi câu lệnh điều kiện kiểm tra xem địa chỉ gọi (`msg.sender`) có đúng là chủ sở hữu hiện tại của vé `#042` hay không, và vé có đang ở trạng thái hợp lệ để chuyển nhượng không.
  4. *Blockchain ghi thay đổi gì:* Các node xác thực đóng block và cập nhật vĩnh viễn biến trạng thái: quyền sở hữu vé `#042` chuyển từ ví của Lan sang ví của người nhận, đồng thời ghi nhận sự kiện chuyển nhượng.

* **Bốn câu hỏi kiểm tra cuối buổi:**
  * **Câu 1: Vì sao xem dữ liệu thường không cần ký ví?**  
    *Trả lời:* Vì thao tác xem dữ liệu (lệnh `eth_call`) chỉ truy vấn trạng thái có sẵn từ node qua cổng RPC mà không làm thay đổi trạng thái trên sổ cái, do đó không tạo giao dịch và không tốn phí gas mạng.
  * **Câu 2: Connect wallet khác approve token ở đâu?**  
    *Trả lời:* **Connect wallet** chỉ chia sẻ địa chỉ ví công khai để website nhận diện danh tính và không thể tự chuyển tài sản; trong khi **Approve token** là giao dịch on-chain cấp quyền chi tiêu (allowance) cho một smart contract được phép tự động rút/chuyển một lượng token nhất định từ ví.
  * **Câu 3: Oracle có thể sai ở khâu nào?**  
    *Trả lời:* Oracle có thể sai ở **khâu nguồn dữ liệu gốc bên ngoài** (dữ liệu sai), khâu **truyền tải dữ liệu** (bị tấn công, can thiệp), hoặc do **dữ liệu bị trễ/quá cũ** không phản ánh đúng thực tế tại thời điểm hợp đồng xử lý.
  * **Câu 4: Nêu một bằng chứng giao dịch đã thực thi thành công.**  
    *Trả lời:* Tra cứu mã giao dịch (**Transaction Hash**) trên trình khám phá mạng (như Etherscan) thấy trạng thái hiển thị là **Success**, đồng thời giá trị biến trạng thái trên hợp đồng đã cập nhật tương ứng (ví dụ: `totalRegistered` tăng thêm 1 và `registered(địa_chỉ_ví)` trả về `true`).

---



#### 3. Work completed
* Nắm vững kiến trúc 4 lớp cấu thành một dApp (Frontend, Wallet, Smart Contract, Blockchain/RPC).
* Phân biệt rõ bản chất giữa truy vấn dữ liệu (`eth_call`) không tốn gas và gửi giao dịch thay đổi trạng thái có tính phí.
* Phân tích chi tiết ranh giới an toàn giữa Connect Wallet, Sign Message (cảnh giác với Permit) và Approve Token (Allowance).
* Tìm hiểu nguyên lý hoạt động của các mảnh ghép Web3 chính: DeFi, DAO và vai trò của Oracle.
* Hoàn thành đầy đủ bài tập nhóm "Vẽ đường đi của lệnh chuyển vé" và 4 câu hỏi kiểm tra cuối buổi.
* Thực hành biên dịch, triển khai và kiểm thử hợp đồng `ClassroomSeat.sol` trên cả Remix VM và Sepolia Testnet.

#### 4. Evidence


#### 5. Blockers


#### 6. Takeaway
* dApp mang lại tính minh bạch và quyền tự chủ cho người dùng, nhưng ranh giới bảo mật nằm ở thao tác ký của ví: luôn kiểm tra kỹ loại hành động (Connect, Sign hay Approve) trước khi xác nhận.
* Smart contract chỉ thực thi đúng theo dữ liệu đầu vào; tính phi tập trung và an toàn của toàn bộ hệ sinh thái Web3 phụ thuộc chặt chẽ vào chất lượng của hạ tầng RPC và nguồn cấp dữ liệu Oracle.
