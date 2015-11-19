# Functions and side effects
Function có thể tạm chia thành những chức năng được gọi để dùng chức năng phụ và những chức năng được gọi để dùng các giá trị trả về. (Mặc dù nó chắc chắn trả về cả chức năng phụ lẫn trả về giá trị).

Các chức năng trợ giúp đầu tiên trong ví dụ trang trại, printZeroPaddedWithLabel, được gọi để dùng chức năng phụ: in một dòng. Trong version thứ hai, zeroPad, hàm này được gọi để sử dụng giá trị trả về của nó. Version thứ hai hữu ích hơn version thứ nhất trong nhiều tình huống. Function tạo ra và trả về các giá trị dễ dàng kết hợp và sử dụng theo những cách mới hơn so với các function được gọi để sử dụng các chức năng phụ.

Một function *thuần khiết* là một loại function cụ thể thuộc loại value-producing, nó không chỉ không có các chức năng phụ mà còn không dựa trên các chức năng phụ của các code khác. Ví dụ nó không đọc các biến global, các biến này đôi khi bị thay đổi bởi các code khác. Một chức năng thuần khiết có tính chất dễ chịu, khi được gọi với những đối số tương tự, nó luôn luôn trả về giá trị giống nhau (và không làm bất cứ điều gì khác). Khi bạn không chắc chắn rằng một chức năng thuần khiết làm việc một cách chính xác, bạn có thể kiểm tra nó bằng cách đơn giản là gọi nó, nếu nó hoạt động trong bối cảnh đó thì nó sẽ làm việc trong mọi hoàn cảnh. Các function không thuần khiết có thể trả về giá trị khác nhau. 

Tuy nhiên, không cần phải cảm thấy xấu khi viết các chức năng không tinh khiết hay tiến hành xóa chúng khỏi code của bạn. Các tác dụng phụ thường hữu ích. Sẽ không có cách nào để viết một phiên bản thuần khiết của console.log, và console.log chắc chắn là hữu ích. Một số hành động có thể dễ dàng thể hiện một cách hiệu quả khi chúng ta sử dụng tác dụng phụ, tốc độ tính toán có thể là một lý do để tránh sự thuần khiết.

