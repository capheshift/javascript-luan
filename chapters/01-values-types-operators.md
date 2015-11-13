
---
## Chapter 1: Values, Types, and Operators

*Trong thế giới máy tính, chỉ có một thứ duy nhất là dữ liệu (data). Bạn có thể đọc, sửa, tạo mới dữ liệu - nhưng bất cứ thứ gì khác không phải là dữ liệu, đơn giản là nó không tồn tại. Tất cả dữ liệu được lưu trữ trong một thứ tự dài của các bits.*

### Values
*Tưởng tượng chúng ta có một đại dương chứa các bits. 1 máy tính cổ điển có hơn 30 tỉ bits lưu trữ.*

![alt text](../img/bit-sea.png "Logo Title Text 1")

Để có thể làm việc với khối lượng bits lớn mà không làm hao hụt nó, bạn có thể chia chúng ra thành các phần nhỏ đại diện cho các mảnh thông tin. Trong môi trường của Javascript, các mảnh đó được gọi là Values ( giá trị). Tất cả những giá trị này được tạo nên bởi bits, giữ những vai trò khác nhau. Mỗi values có một kiểu giá trị (type) để xác định vai trò của chính nó.

Có sác kiểu giá trị cơ bản của values trong Javascript: `numbers` (số), `strings` (chuỗi kí tự), `Booleans` (giá trị `true`/ `false` (đúng/ sai)), `objects` (đối tượng), `functions` (hàm) và `undefined values` (giá trị chưa xác định).

Để tạo 1 value, bạn chỉ đơn giản là gọi tên của nó, chỉ cần gọi tên, và bạn đã có 1 giá trị. Mỗi values được lưu trữ ở đâu đó, và nếu bạn muốn sử dụng một số lượng khổng lồ của chúng cùng thời điểm, có lẽ bạn sẽ gặp một chút vấn đề với với việc vượt quá số bits. May mắn là vấn đề này chỉ xảy ra nếu bạn cần tất cả chúng cùng một lúc. Trong một khoảng thời gian dài không sử dụng đến, nó sẽ được giải phóng.

DUYỆT
---

TRÍ
---

---
### Summary

Chúng ta đã có cái nhìn sơ lược về 4 kiểu giá trị của Javascript trong chương 1 : `numbers`, `strings`, `Boolean`, và `undefined values`. Những giá trị được tạo ra bằng các gọi tên hoặc giá trị của nó, bạn có thể gộp chúng lại và thay đổi giá trị của chúng bằng các phép toán: (`+, -, *, /, và %`), phép nối chuỗi (`+`), so sánh (`==, !=, ===, !==, <, >, <=, >=`), và phép logic (`&&, ||`).
