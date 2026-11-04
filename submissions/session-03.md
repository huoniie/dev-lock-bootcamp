
# Session  - MẬT MÃ HỌC & VÍ
- Student: Chu Thị Hương
- GitHub: https://github.com/huoniie.git
- Submitted: 2026-11-03
- Commit: https://github.com/huoniie/dev-lock-bootcamp.git

## 1. Summary
### Hashing - Hàm băm
- Biến dữ liệu có độ dài bất kỳ thành chuỗi đầu ra có độ dài cố định.

  <img width="618" height="103" alt="image" src="https://github.com/user-attachments/assets/91a6cbab-ab92-42e4-98b4-e6aefbcb080f" />

  
  <img width="281" height="402" alt="image" src="https://github.com/user-attachments/assets/3449f892-1b29-4b2a-b1cd-2ae8457e34ab" />


  <img width="442" height="227" alt="image" src="https://github.com/user-attachments/assets/3859184d-2588-4fa4-b36a-fb97b2a676ca" />

  
- Được dùng trong

   + Định danh giao dịch - (tạo mã duy nhất cho mỗi tránection)
   + Liên kết block(Mỗi block tham chiếu hash của block trước)
   + Merkle Tree ( Tóm tắt và xác minh hàng ngàn giao dịch )
   + Proof of Work ( Tìm hash thỏa mãn điều kiện của mảng )
 
- 5 tính chất của một hàm băm:

  + Tính một chiều
  + Tính xác định
  + Tính toán nhanh
  + Hiệu ứng tuyết lở
  + Kháng xung đột
 
### Mã hóa

<img width="562" height="433" alt="image" src="https://github.com/user-attachments/assets/ea918a93-e7e1-4b1f-8d99-45c8bfccee1a" />


**Mã hóa một chiều:** Là quá trình biến đổi dữ liệu thành một định dạng không thể khôi phục lại được.

**Mã hóa hai chiều:** Là quá trình cho phép dữ liệu
được mã hóa và sau đó giải mã để lấy lại dữ liệu
gốc.


**Mã hóa đối xứng:** Sử dụng cùng một khóa
cho cả quá trình mã hóa và giải mã

<img width="435" height="166" alt="image" src="https://github.com/user-attachments/assets/c33771c0-658b-4687-81ac-52ec1835c5b2" />

Nếu khóa bí mật bị lộ, dữ liệu mã hóa có thể bị giải mã bởi bất kỳ ai có khóa 


**Mã hóa bất đối xứng:** Sử dụng một cặp khóa (public key và private key) cho quá trình mã hóa và giải mã.

<img width="586" height="311" alt="image" src="https://github.com/user-attachments/assets/e1ec835a-01f4-4e13-8bfd-e5fa14f2417a" />


<img width="614" height="346" alt="image" src="https://github.com/user-attachments/assets/6d30a506-260f-4682-b3ae-da3725600292" />


### Public Key & Private Key

Cặp khóa bất đối xứng: dễ đi xuôi, gần như không thể đi ngược

- **Private key**

  Phải giữ tuyệt đối bí mật. Số ngẫu nhiên 256-bit.

- **Private Key**

  Sinh từ private key bằng đường cong elliptic
secp256k1.

<img width="329" height="70" alt="image" src="https://github.com/user-attachments/assets/e9a3cf39-01f6-4b89-a14f-3eae96f8d508" />


### Digital Signature - Chữ ký số 

<img width="654" height="161" alt="image" src="https://github.com/user-attachments/assets/4015b832-7d10-4502-87a9-188a3b3b2a5f" />

<img width="655" height="327" alt="image" src="https://github.com/user-attachments/assets/13ad9ffc-00aa-40f4-a0fa-a1d68bf28441" />

- **Quy trình ký và xác minh**

    + A tạo giao dịch gồm người nhận, số tiền và phí.
    + Ví băm nội dung giao dịch.
    + Ví ký giá trị băm bằng khóa bí mật của A.
    + Giao dịch kèm chữ ký được gửi lên mạng.
    + Các node dùng khóa công khai của A để xác minh chữ ký.
    + Giao dịch hợp lệ được ghi vào block.


- **Các thuộc tính bảo đảm**

<img width="540" height="166" alt="image" src="https://github.com/user-attachments/assets/4fef2748-620b-4390-8c67-dbd2d23d7a00" />

### Ví và địa chỉ 
**Ví (wallet)** không chứa coin. Tài sản được ghi trên blockchain; ví chỉ lưu khóa, hiển thị số dư và ký giao dịch thay người dùng. Địa chỉ ví (address) được tạo qua một chuỗi biến đổi một chiều:

      Khóa bí mật: số bí mật 256 bit.
      Khóa công khai: tính từ khóa bí mật trên đường cong secp256k1.
      Giá trị băm: băm khóa công khai để rút gọn.
      Địa chỉ: chuỗi nhận tài sản, có thể chia sẻ công khai.

<img width="421" height="268" alt="image" src="https://github.com/user-attachments/assets/d7e3c12f-e748-4592-af74-13fa4de2a96a" />

Chia sẻ địa chỉ để nhận tài sản; không bao giờ chia sẻ khóa bí mật.

- **Ví nóng và ví lạnh**

  <img width="426" height="211" alt="image" src="https://github.com/user-attachments/assets/cdab549c-2d39-46bf-b05d-593f8505ec06" />

  <img width="513" height="229" alt="image" src="https://github.com/user-attachments/assets/fff60e67-e63c-416f-af48-c54a9e21b546" />

  ### Cụm từ khôi phục

  Cụm từ khôi phục (seed phrase) là 12 hoặc 24 từ tiếng Anh theo chuẩn BIP-39, dùng để sinh ra toàn bộ khóa của một ví phân cấp xác định (HD wallet). Người nắm cụm từ khôi phục có toàn quyền với mọi tài sản trong ví.

  <img width="640" height="265" alt="image" src="https://github.com/user-attachments/assets/a8e339a6-00cc-4b68-9daf-a5c9849ce616" />


<img width="622" height="222" alt="image" src="https://github.com/user-attachments/assets/739f661e-e73e-48b9-9cfa-4a298fcb8497" />


Mất cụm từ khôi phục và mất thiết bị đồng nghĩa với mất tài sản vĩnh viễn. Không đội ngũ chính thức nào yêu cầu bạn cung cấp cụm từ này.


### Ví lưu ký và ví tự lưu ký

Khác biệt giữa ví lưu ký (custodial) và ví tự lưu ký (non-custodial) nằm ở một câu hỏi: ai đang giữ khóa bí mật


<img width="513" height="236" alt="image" src="https://github.com/user-attachments/assets/d65dd406-6b49-43d9-afa2-f8044b9652df" />


<img width="588" height="268" alt="image" src="https://github.com/user-attachments/assets/3be51534-0164-4745-8b83-d54a9b28010a" />

### Bảo mật ví cơ bản

Kiểm soát khóa là kiểm soát tài sản. Sáu thói quen dưới đây quyết định phần lớn mức độ an toàn của ví

<img width="492" height="198" alt="image" src="https://github.com/user-attachments/assets/def2c245-8cb7-41a9-a8e5-0f12719eb7c7" />












  








  


  


## 2. Topic notes

 ### Bài thực hành
- **Ý 1**

<img width="710" height="513" alt="image" src="https://github.com/user-attachments/assets/1772e9eb-39d8-4473-a534-0e14cf74b4fe" />

- **Ý 2**
  Chưa làm được
  

- **Ý 3**
    Chưa làm được

### Câu hỏi ôn tập

1. Vì sao không thể suy ngược dữ liệu gốc từ giá trị băm?
  
  + Hàm băm là phép biến đổi một chiều. Nó nén dữ liệu có độ dài bất kỳ thành một chuỗi cố   định, ví dụ 256 bit với SHA-256 hoặc Keccak-256.
  + Quá trình này làm mất thông tin. Rất nhiều đầu vào khác nhau cho ra cùng một độ dài đầu ra, nên giá trị băm không đủ để xác định duy nhất dữ liệu gốc.
  + Hiệu ứng tuyết lở khiến đổi một ký tự đầu vào là giá trị băm thay đổi hoàn toàn. Vì vậy không có quy luật nào để “lần ngược” từ kết quả về đầu vào.
  + Cách duy nhất là đoán đầu vào, băm thử rồi so sánh. Cách này tốn chi phí tính toán quá lớn nên không khả thi.
  + Chiều xuôi thì rất nhanh, còn chiều ngược thì gần như không thể.
    
2. Khóa bí mật, khóa công khai và địa chỉ ví khác nhau như thế nào?

	Khóa bí mật |	Khóa công khai |	Địa chỉ ví
Bản chất	| Số ngẫu nhiên 256 bit | 	Tính từ khóa bí mật trên đường cong secp256k1	|Chuỗi rút gọn, tạo bằng cách băm khóa công khai
Vai trò|	Ký giao dịch | 	Xác minh chữ ký |	Nơi nhận tài sản
Chia sẻ| 	Tuyệt đối không	| Có thể	| Có thể

Ba thành phần này nối thành một chuỗi một chiều: khóa bí mật → khóa công khai → băm → địa chỉ. Mỗi bước đều không thể đi ngược. Ai nắm khóa bí mật thì có toàn quyền với tài sản gắn với địa chỉ đó.

3. Node xác minh chữ ký mà không cần khóa bí mật bằng cách nào?

+ A tạo giao dịch gồm người nhận, số tiền và phí. Ví băm nội dung đó rồi ký giá trị băm bằng khóa bí mật của A theo thuật toán ECDSA.
+ Giao dịch được gửi lên mạng kèm chữ ký.
+ Node dùng khóa công khai của A, nội dung giao dịch và chữ ký để kiểm tra theo toán học ECDSA xem chúng có khớp nhau không. Khóa công khai chỉ đủ để kiểm tra chữ ký, không đủ để tạo ra chữ ký.
+ Nếu khớp, node kết luận giao dịch do đúng chủ khóa tạo ra (xác thực) và nội dung không bị sửa sau khi ký (toàn vẹn). Người ký cũng không thể chối bỏ (chống chối bỏ).
+ Giao dịch hợp lệ sẽ được ghi vào block.

4. Vì sao nói “ví không chứa coin”?

+ Coin và số dư được ghi trên blockchain, tức là sổ cái do các node cùng duy trì. Chúng không nằm trong thiết bị hay ứng dụng ví.
+ Ví chỉ làm ba việc: lưu khóa, hiển thị số dư đọc từ blockchain, và ký giao dịch thay người dùng.
+ Vì vậy mất điện thoại không có nghĩa là mất coin. Coin chỉ mất khi mất cả khóa lẫn cụm từ khôi phục, vì khi đó không còn ai ký được giao dịch.
+ Ngược lại, ai có khóa hoặc cụm từ khôi phục thì có thể dùng tài sản từ bất kỳ thiết bị nào.

5. Khi nào nên dùng ví lưu ký, khi nào nên dùng ví tự lưu ký?

Điểm khác biệt nằm ở việc ai giữ khóa bí mật.

- Ví lưu ký (ví trên sàn tập trung) phù hợp khi:
    + bạn mới bắt đầu, giao dịch thường xuyên, giá trị nhỏ;
    + bạn cần mua bán, quy đổi ra tiền pháp định;
    + bạn muốn khôi phục được qua tài khoản nếu quên mật khẩu.
    + Đổi lại, bạn phụ thuộc vào chính sách của nền tảng. Nếu nền tảng bị hack, phá sản hoặc khóa tài khoản, bạn có thể không rút được tài sản.
- Ví tự lưu ký (MetaMask, Phantom, Lace, Ledger) phù hợp khi:
    + bạn muốn toàn quyền kiểm soát, đúng tinh thần “Not your keys, not your coins”;
    + bạn lưu trữ dài hạn hoặc giá trị lớn (nên dùng ví phần cứng như Ledger, Trezor);
    + bạn dùng ứng dụng phi tập trung (DApp).
    + Đổi lại, bạn tự chịu hoàn toàn trách nhiệm bảo mật. Mất cụm từ khôi phục cùng với thiết bị là mất tài sản vĩnh viễn.
  


## 3. Work completed



## 4. Evidence
Không có

## 5. Blockers

Không có
## 6. Takeaway




