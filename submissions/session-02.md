
# Session 02 - How Blockchain Works
- Student: Chu Thị Hương
- GitHub: https://github.com/huoniie.git
- Submitted: 2026-10-22
- Commit: https://github.com/huoniie/dev-lock-bootcamp.git

## 1. Summary


- **Block & Blockchain Structure**
  
Các block được liên kết với nhau thông qua mã hash của block trước đó

- **Transaction**
  
-Là đơn vị công việc nhỏ nhất làm thay đổi trạng thái của mạng lưới

    +Chuyển đổi giá trị
    
    +Thực thi logic 
    
    +Xác thực chữ ký

- **Ledger / State**
  
    -Ledger:Sổ cái lưu trữ mọi giao dịch(lịch sử biến động)
    
    -State: Trạng thái hiện tại( snapshot dữ liệu tại thời điểm hiện tại )

- **Nodes & P2P Network**

**P2P (Peer-to-Peer)** là mô hình Server-Server. 

Mỗi **Node** trong mạng lưới 

    +Đóng vai trò là client (nhận dữ liệu), 

    +Là server (cung cấp dữ liệu và xác thực)
    
**Full node**

    + Tải • xác minh • lưu lịch sử
    
    + Thực thi luật đồng thuận

**Light node**

    + Chỉ tải block header
    
    + Nhanh, nhẹ — phù hợp ví di động

- **Transaction Lifecycle**
  
<img width="857" height="353" alt="image" src="https://github.com/user-attachments/assets/83888fda-518b-48e4-975d-892bcc156c6f" />


- **Blockchain Explorer**(Trình khám phá blockchain)

Công cụ tìm kiếm trực tuyến cho phép bạn tra cứu, theo dõi và phân tích toàn bộ dữ liệu lịch sử cũng như các hoạt động đang diễn ra trên một mạng lưới blockchain

## 2. Topic notes

- **Block & Blockchain Structure**
  
  - 1 block
    
    + 1 mã hash chính nó

    + 1 mã hash của khối trước nó

    + thông tin
    
    + hình vẽ
      
      [khối N] - [Khối N+1]
      
      [Khối N+1] chứa mã hash chính nó và mã hash của khối N

   Note:
  
      1 khối block còn có phần head và body nữa ( liên quan tới light node)
  
      Đặc biệt khối block đầu sẽ không chứa mã hash của khối trước nó ( vì có đâu mà chứa)
  
  trước------[Khối]----sau
     
- **Transaction**

Block chứa thông tin giao dịch nhưng thông tin giao dịch là gì???
Thông tin giao dich
+ chuyển tiền
+ thực thi hành động trên hệ thống
+ gọi một chức năng nào đó của hợp đồng thông minh
+ hành động của bạn trên blockchain


- **Ledger / State**

      tưởng tượng về tài khoản ngân hàng của bản thân cuối tháng
  
      +Lúc nhìn số dư còn 5.000VND ( thì đây là state)
  
      +Kiểm tra lại mình đã tiêu vào đâu mà chưa cuối tháng đã âm tiền vào lịch sử giao dịch kiểm tra ( đây là ledger)
      
- **Nodes & P2P Network**
  P2P : kiểu là mô hình bình đẳng
  hiểu đơn giản trong mạng lưới có hàng ngàn node và node nào cũng có quyền vừa làm client vừa làm server. Nó giúp cho việc xử lý dữ liệu nhanh hơn và gọn hơn.
  còn mô hình cũ trước đây chúng ta chỉ có duy nhất 1 server khi đó server phải phải thực hiện rất nhiều yêu cầu từ phía client đến một mức nào đó có thể chậm và thậm chí quá tải
   

- **Transaction Lifecycle**
  4 bước
  +tạo giao dịch
  +gửi đến mạng
  +kiểm tra xem nó hợp lệ không
    nếu có sẽ được cho vô 1 cái bể chờ bước 4
    nếu không thì bị loại
  + cuối cùng là đưa vào 1 block mới
- **Blockchain Explorer**
  nơi mà mình xem chi tiết dữ liệu trên blockchain 

## 3. Work completed

Không có
## 4. Evidence
Không có

## 5. Blockers

Không có
## 6. Takeaway

chỗ này
<img width="349" height="279" alt="image" src="https://github.com/user-attachments/assets/6d91258e-e47a-49b6-824e-0c7ff1d59b51" /> 

em đang chưa phân biệt được cái node này là trong một khối block hay nó là một tập hợp khối block




