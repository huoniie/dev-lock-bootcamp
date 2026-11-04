
# Session 02 - MẬT MÃ HỌC & 
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


  








  


  


## 2. Topic notes

 dữ liệu trên blockchain 

## 3. Work completed

Không có
## 4. Evidence
Không có

## 5. Blockers

Không có
## 6. Takeaway




