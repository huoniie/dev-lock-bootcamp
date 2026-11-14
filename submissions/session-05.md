### Session 05 - HỢP ĐỒNG THÔNG MINH & TÀI SẢN SỐ
* **Student:** Chu Thị Hương
* **GitHub:** https://github.com/huoniie.git
* **Submitted:** 2026-11-14
* **Commit:** https://github.com/huoniie/dev-lock-bootcamp.git

---

#### 1. Summary

##### 1.1. Hợp đồng thông minh (Smart Contract)
* **Bản chất:** Là một chương trình máy tính gồm mã lệnh và dữ liệu được lưu trực tiếp trên blockchain, tự động kiểm tra và thực thi nhất quán theo quy tắc khi nhận được lời gọi hợp lệ.
* **Đặc tính hoạt động:**
  * Cập nhật trạng thái (State) theo logic mã lệnh.
  * Hợp đồng chỉ nhận diện địa chỉ gọi hàm (address), không tự biết danh tính người thực hay các sự kiện ngoài đời thực nếu không có dữ liệu đầu vào phù hợp.
  * *Ẩn dụ chiếc vé của Lan:* Lan mua vé xem ca nhạc, dữ liệu vé được lưu trên blockchain. Nếu website bán vé ngừng hoạt động, Lan vẫn chứng minh được quyền sở hữu vé thông qua bản ghi on-chain. Khi Lan chuyển vé cho Minh, trạng thái chủ vé cập nhật sang Minh, nhưng toàn bộ lịch sử lần chuyển trước đó vẫn được lưu giữ bất biến.

##### 1.2. Phân biệt Native Coin và Token
* **Native Coin (Đồng coin gốc):** Là tài sản gốc gắn liền với sự vận hành của mạng lưới (ví dụ: ETH trên Ethereum, SOL trên Solana), có vai trò bắt buộc dùng để chi trả phí xử lý giao dịch mạng lưới (Gas fee).
* **Token (Tài sản phái sinh):** Là tài sản được tạo ra và quản lý bởi hợp đồng thông minh hoặc chương trình trên nền tảng có sẵn (ví dụ: USDC, token điểm thưởng, vé NFT).
* **Tình huống thực tế:** Lan có 100 USDC trên Ethereum nhưng ví không có ETH thì không thể thực hiện giao dịch chuyển USDC thông thường, vì phí mạng bắt buộc phải thanh toán bằng ETH.

| Tiêu chí | Native Coin | Token |
| :--- | :--- | :--- |
| **Bản chất** | Tài sản gốc của mạng lưới | Tài sản do smart contract quản lý |
| **Ví dụ** | ETH (Ethereum), SOL (Solana) | USDC, Token điểm thưởng CLB, NFT |
| **Trả phí mạng** | Trực tiếp làm phí giao dịch | Cần coin gốc của mạng để trả phí |
| **Nhận diện** | Tên mạng và ký hiệu tài sản gốc | Tên mạng và địa chỉ hợp đồng (Contract Address) |

##### 1.3. Vòng đời Token: Mint, Transfer và Burn
Sự biến động của tổng cung token (Total Supply) do các hàm trong smart contract quy định:
* **Mint (Đúc/Tạo mới):** Tạo thêm các đơn vị token mới đưa vào lưu thông $\rightarrow$ **Làm tăng tổng cung**.
* **Transfer (Chuyển khoản):** Di chuyển token giữa các địa chỉ ví $\rightarrow$ **Tổng cung không đổi**, chỉ thay đổi số dư từng tài khoản.
* **Burn (Đốt/Tiêu hủy):** Hủy bỏ vĩnh viễn các đơn vị token theo cơ chế hợp đồng $\rightarrow$ **Làm giảm tổng cung**.
* *Lưu ý:* Việc gửi token vào một địa chỉ rác hoặc ví không dùng nữa chưa chắc đã kích hoạt cơ chế burn hoặc làm giảm trường `totalSupply` ghi nhận trên hợp đồng.

| Thao tác | Hành động | Biến động tổng cung (Ví dụ) |
| :--- | :--- | :--- |
| **Mint 20** | Tạo thêm 20 token mới | $100 \rightarrow 120$ |
| **Transfer 10** | Chuyển 10 token giữa hai ví | Giữ nguyên ở $120$ |
| **Burn 5** | Tiêu hủy 5 token khỏi lưu thông | $120 \rightarrow 115$ |

##### 1.4. Stablecoin & Hiện tượng Mất neo (Depeg)
* **Khái niệm:** Là token được thiết kế nhằm mục đích bám theo một giá trị tham chiếu cố định (thường là $1 \text{ token} \approx 1 \text{ USD}$) để tạo sự ổn định trong giao dịch và thanh toán.
* **Ba nhóm cơ chế giữ giá:**
  1. *Dự trữ tiền pháp định (Fiat-backed):* Bảo đảm bằng tiền mặt hoặc tài sản thanh khoản gửi tại ngân hàng theo tỷ lệ 1:1 (ví dụ USDC của Circle).
  2. *Thế chấp mã hóa (Crypto-collateralized):* Khóa tài sản mã hóa khác vào hợp đồng với tỷ lệ thế chấp vượt mức (over-collateralized) kèm cơ chế thanh lý tự động.
  3. *Thuật toán (Algorithmic):* Điều tiết nguồn cung tự động theo biến động cung - cầu thị trường.
* **Hiện tượng Depeg:** Xảy ra khi giá thị trường của stablecoin lệch khỏi mức tham chiếu (ví dụ $1 \text{ token} = 0,97 \text{ USD}$). Tuyệt đối không lấy mục tiêu 1 USD thay thế cho giá giao dịch thực tế.

##### 1.5. NFT (Non-Fungible Token) & Bản chất quyền sở hữu
* **Tính chất:** Khác với Fungible Token (các đơn vị có thể thay thế cho nhau), mỗi NFT là một đơn vị độc bản, không thể hoán đổi tương đương (ví dụ vé `#042` khác hoàn toàn vé `#043`).
* **Định danh NFT:** Cần đủ 3 yếu tố: **Tên mạng** + **Địa chỉ hợp đồng (Contract Address)** + **Token ID**.
* **Phân biệt ba thành phần của NFT:**
  1. *Bản ghi trên chuỗi (On-chain record):* Thể hiện địa chỉ ví nào đang sở hữu Token ID nào và lịch sử chuyển nhượng.
  2. *Metadata & Nội dung:* Tên gọi, thuộc tính, đường dẫn hình ảnh (thường lưu trữ off-chain như IPFS hoặc máy chủ web). Nếu máy chủ ảnh gặp sự cố, ảnh có thể không hiển thị nhưng bản ghi token vẫn tồn tại.
  3. *Quyền sử dụng:* Do đơn vị phát hành quy định. Nắm giữ NFT **không tự động trao bản quyền tác giả hình ảnh** hay bảo đảm sự kiện ngoài đời bắt buộc phải diễn ra.

##### 1.6. Phí giao dịch (Gas) & Môi trường thực thi
* **Gas:** Thước đo lượng công việc tính toán, lưu trữ mà mạng lưới phải thực hiện cho mỗi giao dịch.
* **Công thức tính phí:**
  $$\text{Transaction Fee} = \text{Gas đã dùng (Gas Used)} \times \text{Đơn giá Gas (Gas Price)}$$
  
* **Xử lý giao dịch lỗi:**
  * *Bấm hủy trên ví trước khi ký:* Không có giao dịch gửi lên mạng $\rightarrow$ Không mất phí.
  * *Giao dịch đã vào block nhưng bị Revert (thất bại):* Mọi thay đổi trạng thái bị hoàn tác, nhưng **vẫn bị trừ phí Gas** vì validator đã tiêu tốn tài nguyên máy tính để chạy mã lệnh đến điểm dừng lỗi.
* **Môi trường thực thi (Virtual Machine / Runtime):**
  * *EVM (Ethereum Virtual Machine):* Chuẩn máy ảo của Ethereum và các mạng tương thích (BSC, Polygon, Arbitrum).
  * *SVM (Solana Virtual Machine):* Môi trường thực thi tối ưu xử lý song song các chương trình biên dịch sBPF trên Solana.
  * *WASM (WebAssembly):* Định dạng mã nhị phân độc lập nền tảng được dùng trên một số mạng như CosmWasm.

---

#### 2. Topic notes



* **Bài tập ghép đúng khái niệm:**
  1. *ETH trên Ethereum* $\rightarrow$ **Native Coin**
  2. *Vé #042 có thể chuyển nhượng* $\rightarrow$ **NFT**
  3. *Tạo thêm 100 điểm thành viên* $\rightarrow$ **Mint**
  4. *USDC bám theo USD* $\rightarrow$ **Stablecoin**
  5. *Chuyển vé từ Lan sang Minh* $\rightarrow$ **Transfer**

* **Ba câu hỏi kiểm tra cuối buổi:**
  * **Câu 1: Burn có bảo đảm giá tăng không? Vì sao?**  
    *Trả lời:* Không bảo đảm, vì giá token trên thị trường còn phụ thuộc vào nhu cầu mua thực tế và tính thanh khoản chứ không chỉ phụ thuộc vào việc giảm nguồn cung.
  * **Câu 2: Mua NFT của một ảnh có tự có bản quyền ảnh không?**  
    *Trả lời:* Không, việc sở hữu bản ghi token trên blockchain không đồng nghĩa với việc được chuyển giao quyền sở hữu trí tuệ hay bản quyền tác giả của tác phẩm.
  * **Câu 3: Giao dịch revert sau khi vào block có thể mất phí không?**  
    *Trả lời:* Có, vì các validator đã phải tiêu tốn tài nguyên tính toán (CPU, bộ nhớ) để xử lý các lệnh của giao dịch cho đến khi gặp điều kiện lỗi hoàn nguyên.

* **Tình huống Lan chuyển 100 USDC:**
  * *Cản trở:* Ví Lan không có ETH để trả phí gas cho mạng Ethereum.
  * *Giải pháp:* Nạp một lượng nhỏ ETH vào ví làm phí gas; dùng cầu nạp gas (Gas Refuel) từ Layer 2; hoặc sử dụng ví thông minh hỗ trợ tài trợ phí / Paymaster (ERC-4337 / Permit EIP-2612).

---

#### 3. Work completed
* Nắm vững nguyên lý hoạt động của Smart contract và cách cập nhật trạng thái trên chuỗi.
* Phân biệt rõ ràng Coin gốc, Token ERC-20, Stablecoin và NFT ERC-721.
* Hiểu rõ cơ chế biến động tổng cung (Mint, Transfer, Burn) và cơ chế tính phí Gas trên EVM.
* Hoàn thành đầy đủ bài tập nối khái niệm, 3 câu kiểm tra cuối buổi và phân tích tình huống thực tế.
* Thực hành đọc và phân tích dữ liệu token USDC trên Etherscan.

#### 4. Evidence


#### 5. Blockers

#### 6. Takeaway
* Smart contract là bộ quy tắc bất biến quản lý tài sản, nhưng nó chỉ biết dữ liệu on-chain và địa chỉ ví, không tự biết sự kiện ngoài đời thực.
* Người dùng cần luôn kiểm tra kỹ mạng lưới, địa chỉ hợp đồng chính thức và hiểu rõ nội dung giao dịch trước khi bấm ký xác nhận trên ví.
