---
## Chapter 3: Functions

### Giá trị hàm (Function as values)
Các biến số hàm (function variables) thường chỉ đóng vai trò đơn giản như tên cho 1 phần riêng biệt của chương trình. Các biến số như vậy, chỉ được định nghĩa 1 lần và không bao giờ thay đổi. Điều này làm chúng ta dễ nhầm lẫn giữa hàm (function) và tên của nó.
Tuy nhiên, cả 2 là khác biệt. 1 giá trị hàm (function value) có thể làm tất cả những thứ mà các giá trị (values) có thể làm - bạn có thể sử dụng nó trong các biểu thức tùy ý, chứ không phải đơn giản là gọi nó. Ta có thể lưu giá trị hàm (function value) ở 1 nơi mới, truyền nó như 1 đối số vào 1 hàm khác, và hơn thế nữa. Tương tự vậy, 1 biến có thể lưu trữ hàm như 1 biến bình thường và có thể được gán 1 giá trị mới, như:
```javascript
  var launchMissiles = function(value) {
    missileSystem.lauch("now");
  };
  if (safeMode)
    launchMissiles = function(value) { /* do nothing */};
```
Trong [Chương 5](), chúng ta sẽ bàn luận về những điều tuyệt vời chúng ta có thể làm bằng việc truyền các giá trị hàm (function values) vào các hàm khác.

### Kí hiệu khai báo (Declaration notation)
Ở đây có 1 cách ngắn gọn hơn để nói "`var square = ...function`". Từ khóa `function` có thể được dùng ở đầu cú pháp, như trong trường hợp dưới đây:
```javascript
  function square(x) {
    return x * x;
  }
```
Đây là một *khai báo* hàm (function *declaration*). Cú pháp trên định nghĩa biến (variable) `square` và trỏ (point) nó vào hàm được cho. Cho đến bây giờ mọi thứ đều tốt đẹp. Ở đây có 1 sự tinh tế với hình thức khai báo hàm này, tuy nhiên.
```javascript
  console.log("The future says:", future());

  function future() {
    return "We STILL have no flying cars.";
  }
```
Đoạn mã (code) trên hoạt động, mặc dù hàm được định nghĩa *bên dưới* (*below*) phần mã (code) dùng đến nó. Đó là bởi vì việc khai báo hàm (function declarations) không phải là 1 phần của quá trình *từ-trên-xuống* (top-to-bottom) thông thường. Chúng được xem như di chuyển đến đỉnh (top) phạm vi (scope) của chúng và có thể được sử dụng bởi tất cả đoạn mã (code) thuộc cùng phạm vi (scope). Điều này đôi lúc hữu dụng bởi nó cho chúng ta tự do sắp xếp (order) mã (code) theo cách trông có nghĩa nhất, mà không cần phải lo lắng về việc phải định nghĩa (define) tất cả hàm bên trên, trước khi chúng được dùng đến.
Điều gì xảy ra khi ta đưa 1 định nghĩa hàm (function definition) vào trong 1 khối điều kiện (*if*) hay vòng lặp? Chà, đừng làm điều đó. Sự khác biệt của nền tảng JavaScript trong từng trình duyệt (browser) theo thường lệ sẽ thực hiện những công việc khác nhau tùy tình huống, và chuẩn (standard) mới nhất hầu như không cho phép điều này. Nếu bạn muốn chương trình của mình được ổn định (consistently), chỉ sử dụng hình thức định nghĩa hàm (function-definition) này ở khối hàm (function) hay chương trình (program) ngoài cùng nhất.
```javascript
  function example() {
    function a() {} // Okay
    if (something) {
      function b() {} // Danger!
    }
  }
```

### Ngăn xếp lời gọi (The call stack)
Có một cái nhìn gần hơn về cách sự điều khiển chảy qua các hàm (control flows through functions) là rất hữu ích.
```javascript
  function greet(who) {
    console.log("Hello " + who);
  }
  greet("Harry");
  console.log("Bye");
```
Duyệt qua chương trình (program) này, mọi thứ diễn ra đại khái như sau: lời gọi đến `greet` làm cho control (điều khiển) nhảy đến điểm bắt đầu của hàm đó (dòng 2). Nó gọi `console.log` (một hàm xây dựng sẵn của trình duyệt) (a built-in browser function), `console.log` lấy quyền điều khiển (control), làm công việc của nó, và sau đó trả điều khiển (control) về dòng 2. Sau đó nó đi đến đoạn cuối của hàm `greet`, sau đó trở lại nơi đã gọi nó, tại dòng 4. Dòng này sau đó gọi `console.log` một lần nữa.
Chúng ta có giản đồ dòng chảy của điều khiển (flow of control) như sau:
```
  top
    greet
      console.log
    greet
  top
    console.log
  top
```
Bởi vì 1 hàm phải nhảy trở lại (jump back) nơi gọi nó khi trở về (return), máy tính phải ghi nhớ ngữ cảnh từ đâu hàm được gọi. Trong trường hợp trên, `console.log` phải nhảy ngược trở lại hàm `greet`. Trong các trường hợp khác, nó nhảy ngược trở lại điểm kết thúc của chương trình.
Nơi mà máy tính lưu trữ các ngữ cảnh này được gọi là *ngăn xếp lời gọi* (*call stack*). Mỗi lần hàm được gọi, ngữ cảnh hiện thời (current context) được đẩy vào đỉnh của "ngăn xếp" (stack) này. Khi hàm trở về (return), máy tính loại bỏ ngữ cảnh ở đỉnh của ngăn xếp (stack) và dùng nó để tiếp tục thực thi.
Lưu ngăn xếp (stack) này đòi hỏi 1 lượng bộ nhớ của máy tính. Khi ngăn xếp (stack) trở nên quá lớn, máy tính xuất ra thông điệp lỗi như "hết bộ nhớ stack" (out of stack space) hay "quá nhiều sự quay về" (too much recursion). Đoạn mã (code) sau đây minh họa cho điều này bằng cách yêu cầu máy tính 1 câu hỏi khá khó, sẽ dẫn đến việc gọi tới-lui (back-and-forth) vô hạn (infinite) giữa 2 hàm. Đúng hơn, điều đó *sẽ là* vô hạn (infinite), nếu máy tính có 1 ngăn xếp (stack) vô hạn (infinite). Và vì không phải như vậy, chúng ta sẽ cạn bộ nhớ (run out of space), hoặc "làm nổ stack" (blow the stack).
```javascript
  function chicken() {
    return egg();
  }
  function egg() {
    return chicken();
  }
  console.log(chicken() + " came first.");
  // -> ??
```

TAN
---

THANH
---
