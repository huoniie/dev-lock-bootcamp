### Session 04 - CƠ CHẾ ĐỒNG THUẬN & KIẾN TRÚC BLOCKCHAIN
* **Student:** Chu Thị Hương
* **GitHub:** https://github.com/huoniie.git
* **Submitted:** 2026-11-10
* **Commit:** https://github.com/huoniie/dev-lock-bootcamp.git

---

#### 1. Summary

##### 1.1. Cơ chế đồng thuận (Consensus Mechanism)
* **Khái niệm:** Là cách các node phân tán trong mạng thống nhất một trạng thái sổ cái chung duy nhất mà không cần máy chủ trung tâm.
* **Bản chất:** Là lời giải cho bài toán các vị tướng Byzantine (đạt thỏa thuận khi một số thành viên không đáng tin, bị hỏng hoặc cố tình gian lận).
* Mỗi cơ chế đồng thuận trả lời 2 câu hỏi: **Ai được đề xuất block tiếp theo?** và **Làm sao mạng lưới chấp nhận block đó?**

<!-- Ảnh Slide 4 / Hình 1 từ PDF: Nhiều node cùng thống nhất một sổ cái chung -->
<img width="800" alt="Hình 1: Nhiều node cùng thống nhất một sổ cái chung, kể cả khi có node lỗi" src="" />

```text
[Node 1] \
[Node 2] --- (Đồng thuận / Consensus) ---> [ SỔ CÁI CHUNG DUY NHẤT ]
[Node 3] /
[Node Lỗi/Gian lận] (bị loại trừ / không ảnh hưởng kết quả)
```

---

##### 1.2. Proof of Work (PoW) vs. Proof of Stake (PoS)

* **Proof of Work (Bằng chứng công việc):**
  * Cạnh tranh bằng năng lực tính toán.
  * Thợ đào (miner) lặp lại quy trình: thay đổi *nonce* $\rightarrow$ băm khối $\rightarrow$ so sánh với ngưỡng mục tiêu (*target*). Ai tìm ra hash thỏa mãn trước sẽ được thêm block và nhận thưởng.

<!-- Ảnh Slide 5 / Hình 2 từ PDF: Vòng lặp đào block PoW -->
<img width="800" alt="Hình 2: Vòng lặp đào block trong Proof of Work" src="" />

```text
+-----------------------------------------------------------+
|               VÒNG LẶP ĐÀO BLOCK (PoW)                    |
|  [ Thử Nonce ] ---> [ Băm Block ] ---> [ So sánh Target ] |
|        ^                                     |            |
|        |-------- (Nếu Hash >= Target) -------+            |
|                                              v            |
|                            (Nếu Hash < Target: Thành công)|
+-----------------------------------------------------------+
```

* **Proof of Stake (Bằng chứng cổ phần):**
  * Bảo đảm an ninh bằng tài sản ký quỹ.
  * Người xác thực (validator) khóa coin vào mạng lưới làm tài sản bảo đảm.
  * Validator được chọn để đề xuất block, các validator khác tiến hành kiểm tra xác thực. Nếu gian lận sẽ bị phạt cắt coin ký quỹ (*slashing*).

<!-- Ảnh Slide 6 / Hình 3 từ PDF: Mô hình ký quỹ PoS và Slashing -->
<img width="800" alt="Hình 3: Proof of Stake - Người xác thực ký quỹ coin để tham gia đồng thuận" src="" />

* **Bảng so sánh PoW và PoS:**

| Tiêu chí | Proof of Work (PoW) | Proof of Stake (PoS) |
| :--- | :--- | :--- |
| **Tài nguyên** | Điện năng và máy đào | Coin ký quỹ |
| **Người tạo block** | Thợ đào (Miner) | Người xác thực (Validator) |
| **Cơ chế an ninh** | Chi phí tính toán khổng lồ | Cắt coin ký quỹ (*Slashing*) |
| **Tiêu thụ năng lượng**| Mức tiêu thụ cao | Thấp hơn đáng kể |
| **Tính chung cuộc** | Xác suất | Thường nhanh hơn (xác định) |
| **Ví dụ** | Bitcoin | Ethereum, Cardano |

---

##### 1.3. Tính chung cuộc (Finality)
* **Khái niệm:** Là thời điểm một giao dịch thực sự chắc chắn và không thể bị đảo ngược.
* Giao dịch khi vừa vào block chưa chắc chắn tuyệt đối; số xác nhận cần chờ phụ thuộc vào cơ chế đồng thuận.

<!-- Ảnh Slide 8 / Hình 4 từ PDF: Tiến trình Finality qua các block xác nhận -->
<img width="800" alt="Hình 4: Mỗi block mới làm xác suất đảo ngược giao dịch giảm dần" src="" />

```text
[TX Block] ---> [+1 Block] ---> [+2 Block] ---> [+3 Block] ---> ... ---> [+6 Block]
<---------------- Xác suất bị đảo ngược giảm dần -------------->    (Chung cuộc vĩnh viễn)
```

* **Phân loại chung cuộc:**
  * **Chung cuộc theo xác suất (Bitcoin):** Mỗi block mới sinh ra chồng lên phía sau làm xác suất bị đảo ngược giảm dần (thường chờ 6 xác nhận).
  * **Chung cuộc xác định (Ethereum):** Giao dịch được chốt dứt điểm khi có đủ đa số validator xác nhận sau khi block được finalize.

---

##### 1.4. Bộ ba bất khả thi & Kiến trúc phân tầng (Layer 1 / Layer 2)
* **Bộ ba bất khả thi (Blockchain Trilemma):** Một blockchain rất khó đạt cùng lúc cả 3 yếu tố: **Phi tập trung**, **Bảo mật** và **Khả năng mở rộng**. Muốn tăng yếu tố này thường phải đánh đổi yếu tố kia, đó là lý do Layer 2 ra đời.

<!-- Ảnh Slide 9 / Hình 5 từ PDF: Tam giác Blockchain Trilemma -->
<img width="600" alt="Hình 5: Bộ ba bất khả thi của blockchain" src="" />

* **Kiến trúc Layer 1 & Layer 2:**
  * **Layer 1:** Đóng vai trò gốc về đồng thuận, lưu trữ dữ liệu và bảo mật (Bitcoin, Ethereum).
  * **Layer 2:** Tầng mở rộng giúp xử lý nhanh, gom nhiều giao dịch off-chain rồi nén kết quả ghi về Layer 1 (Lightning Network, Arbitrum, Optimism).
  * *Ẩn dụ giao thông:* Layer 1 là **đường cao tốc chính**; Layer 2 là **hệ thống đường gom** xử lý bớt lượng xe cộ rồi nhập làn về cao tốc.

<!-- Ảnh Slide 10 / Hình 6 từ PDF: Kiến trúc phân tầng Layer 1 & Layer 2 -->
<img width="800" alt="Hình 6: Kiến trúc phân tầng Layer 1 và Layer 2" src="" />

---

##### 1.5. Mô hình trạng thái: Account-based vs. UTXO

<!-- Ảnh Slide 11 / Hình 7 từ PDF: So sánh mô hình Account và UTXO -->
<img width="800" alt="Hình 7: Hai cách biểu diễn trạng thái tài sản (Account-based vs UTXO)" src="" />

* **Account-based (Mô hình tài khoản - ví dụ Ethereum):**
  * Tương tự số dư tài khoản ngân hàng, hệ thống cộng/trừ trực tiếp số dư tài khoản.
  * *Ví dụ:* An gửi Bình 30 $\rightarrow$ Số dư An giảm trực tiếp `100 -> 70`; Bình tăng `20 -> 50`.
* **UTXO (Unspent Transaction Output - ví dụ Bitcoin):**
  * Tương tự các tờ tiền mặt chưa tiêu. Giao dịch gom các đầu vào cũ (input), tiêu hủy chúng và tạo ra các đầu ra mới (output).
  * *Ví dụ:* An dùng 2 tờ 50 (tổng 100) để gửi 70 cho Bình $\rightarrow$ Đầu ra tạo thành: 70 chuyển đến Bình và 30 tiền thối thừa trả lại cho An.

---

##### 1.6. Mô hình triển khai & Ca ứng dụng thực tế

<!-- Ảnh Slide 12 / Hình 8 từ PDF: Ba mô hình triển khai Public, Private và Permissioned -->
<img width="800" alt="Hình 8: Ba mô hình triển khai blockchain (Public, Private, Permissioned)" src="" />

* **So sánh 3 mô hình triển khai:**
  * **Public (Công khai):** Mọi người đều có quyền đọc/ghi mà không cần cấp phép, tin cậy dựa vào kinh tế mạng (Bitcoin, Ethereum).
  * **Private (Riêng tư):** Do một tổ chức duy nhất kiểm soát, quyền đọc/ghi nội bộ (Mạng nội bộ doanh nghiệp).
  * **Permissioned (Cấp phép / Liên minh):** Nhiều tổ chức liên minh cùng quản trị, chỉ thành viên được cấp quyền mới được ghi dữ liệu (Hyperledger Fabric).

* **Ca ứng dụng: Cấp bằng đại học trên Blockchain:**
  * Các trường đại học lập liên minh vận hành một **Permissioned chain** để quản lý việc cấp và thu hồi bằng.
  * Định kỳ neo giá trị băm **Merkle Root** của lô bằng cấp lên **Public chain**.
  * *Bảo vệ quyền riêng tư:* Tuyệt đối không đưa dữ liệu cá nhân sinh viên lên chuỗi; Public chain chỉ lưu bằng chứng mã hóa Merkle Root để bất kỳ nhà tuyển dụng nào cũng có thể kiểm chứng tính toàn vẹn của văn bằng.

<!-- Ảnh Slide 13 / Hình 9 từ PDF: Kiến trúc hệ thống cấp bằng liên minh neo Merkle Root -->
<img width="800" alt="Hình 9: Kiến trúc hệ thống cấp bằng đại học trên blockchain" src="" />

```text
[Trường A] \
[Trường B] --- (Quản trị chung) ---> [ CHUỖI LIÊN MINH (Permissioned) ]
[Trường C] /                          (Lưu trữ dữ liệu chứng chỉ/bằng)
                                                    |
                                    (Định kỳ neo Merkle Root)
                                                    v
                                      [ PUBLIC CHAIN (Ethereum) ]
                                (Công chúng xác thực bằng chứng)
```

---

#### 2. Topic notes

##### 2.1. Giải đáp câu hỏi ôn tập
1. **Vì sao blockchain cần cơ chế đồng thuận?**  
   Vì trong mạng lưới phi tập trung không có máy chủ trung tâm và các node không tin tưởng nhau, cơ chế đồng thuận giúp thống nhất một trạng thái sổ cái duy nhất, ngăn chặn gian lận chi tiêu kép (*double-spending*) ngay cả khi có node bị lỗi hoặc gửi thông tin sai.
2. **Thợ đào (PoW) và Validator (PoS) khác nhau thế nào?**  
   *Thợ đào:* Cạnh tranh bằng sức mạnh tính toán phần cứng và điện năng để tìm *nonce*.  
   *Validator:* Khóa coin ký quỹ (*stake*) làm tài sản đảm bảo; nếu làm sai hoặc gian lận sẽ bị phạt cắt coin (*slashing*).
3. **Chung cuộc xác suất khác chung cuộc xác định ra sao?**  
   *Xác suất:* Càng nhiều block xếp sau, xác suất bị đảo ngược càng giảm dần theo thời gian (cần chờ nhiều block xác nhận).  
   *Xác định:* Giao dịch được chốt vĩnh viễn ngay khi có đủ đa số validator biểu quyết xác thực.
4. **Bộ ba bất khả thi là gì và Layer 2 giải quyết như thế nào?**  
   Bộ ba bất khả thi chỉ ra rằng một chuỗi không thể tối ưu đồng thời cả Phi tập trung, Bảo mật và Mở rộng. Layer 2 giải quyết bằng cách xử lý giao dịch off-chain nhanh chóng với chi phí rẻ, sau đó chỉ nén kết quả gửi về Layer 1 để thừa hưởng bảo mật và tính phi tập trung.
5. **Vì sao không đưa thông tin cá nhân lên Public blockchain trong bài toán cấp bằng?**  
   Dữ liệu trên blockchain là công khai và không thể xóa bỏ, nếu đưa thông tin cá nhân sẽ vi phạm quyền riêng tư nghiêm trọng. Do đó chỉ chuỗi liên minh lưu trữ dữ liệu, còn chuỗi công khai chỉ lưu mã băm **Merkle Root** làm bằng chứng kiểm chứng.

---

##### 2.2. Bằng chứng làm bài thực hành (Evidence placeholders)
* **Bài 1 (Blockchain Demo):**  
  <img width="800" alt="Ảnh chụp màn hình thử đào block và làm vỡ chuỗi trên Blockchain Demo" src="" />
* **Bài 2 (Mempool.space):**  
  <img width="800" alt="Ảnh chụp màn hình tra cứu TX Bitcoin, xác nhận và UTXO trên Mempool" src="" />
* **Bài 3 (L2BEAT):**  
  <img width="800" alt="Ảnh chụp màn hình tra cứu dự án Layer 2 và TVL trên L2BEAT" src="" />

---

#### 3. Work completed
* Nghiên cứu toàn diện các cơ chế đồng thuận (PoW, PoS), tính chung cuộc, bộ ba bất khả thi, Layer 1 & 2, UTXO, Account-based và 3 mô hình mạng lưới.
* Trả lời đầy đủ 5 câu hỏi ôn tập theo giáo trình.
* Hoàn thành các bài tập thực hành trên Blockchain Demo, Mempool.space và L2BEAT.

#### 4. Evidence
*(Xem các ảnh chụp màn hình bài thực hành đã đính kèm ở mục 2.2)*.

#### 5. Blockers
* Cần làm rõ thêm cách tính ngưỡng chịu lỗi $3f + 1$ trong các thuật toán PBFT/BFT khi áp dụng thực tế với số lượng node nhỏ.

#### 6. Takeaway
* Cơ chế đồng thuận kết hợp giữa toán học mật mã và kinh tế học hành vi (phần thưởng và hình phạt) để duy trì trật tự cho hệ thống phi tập trung.
* Kiến trúc xếp tầng (Layer 1 + Layer 2) là chìa khóa tháo gỡ điểm nghẽn mở rộng mà không làm suy yếu an ninh cốt lõi của blockchain.
