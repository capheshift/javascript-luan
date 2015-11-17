---
## Chapter 3: Functions

>Người ta nghĩ rằng khoa học máy tính là nghệ thuật của những thiên tài nhưng thực tế thì ngược lại, chỉ cần nhiều người làm các công việc cùng nhau, giống như một bức tường được tạo nên từ những viên đá nhỏ. - Donald Knuth

Hàm là một công cụ để cấu trúc nên một chương trình lớn, để giảm sự lặp đi lặp lại và cô lập các chương trình con với nhau.

Những câu lệnh được hổ trợ sẵn thì khá cứng nhắc, vì vậy ta cần phải sử dụng thêm ngôn ngữ của chính mình để tạo nên sự linh hoạt hơn trong lập trình.

### Định nghĩa một hàm
Việc định nghĩa hàm cũng giống như định nghĩa một biến thông thường. Ví dụ: đoạn code sau đây định nghĩa một biến square như một hàm để thực hiện bình phương một số.

```javascript
var square = function(x) {
  return x * x;
};
```

- Một hàm được tạo ra bởi một biểu thức bắt đầu bằng từ khóa `function`. Một hàm gồm có một bộ các tham số và thân hàm chứa các câu lệnh sẽ được thực thi khi hàm được gọi. Thân hàm phải luôn luôn được chứa trong cặp dấu hoặc nhọn, ngay khi chỉ có một dòng lệnh.
- Một hàm có thể có nhiều tham số hoặc không có tham số nào cả. Như trong ví dụ bên dưới, hàm `makeNoise` không chứa bất kỳ một tham số nào, trong khi đó hàm  `power` có hai tham số truyền vào.

```javascript
var makeNoise = function() {
  console.log("Pling!");
};

makeNoise();
// → Pling!

var power = function(base, exponent) {
  var result = 1;
  for (var count = 0; count < exponent; count++)
    result *= base;
  return result;
};

console.log(power(2, 10));
// → 1024
```

Một vài hàm sẽ trả về một giá trị, như hàm `power` và hàm `square`, trong khi một số khác thì không như hàm `makeNoise`. Câu lệnh `return` sẽ quyết định giá trị trả về của hàm. Khi chương trình thực thi đến câu lệnh `return` thì ngay lập tức sẽ thoát ra khỏi hàm hiện tại và trả về giá trị cho đối tượng đã gọi hàm đó. Nếu từ khóa `return` mà không kèm theo một biểu thức nào đằng sau nó thì hàm sẽ trả về giá trị là `undefined`.

### Parameters and scopes
Một tính chất quan trọng của function là các biến được tạo ra bên trong function, bao gồm các đối số của nó, đều là các biến local. Ví dụ biến kết quả `result` trong ví dụ hàm `power` sẽ được tạo mới mỗi khi hàm được gọi, và mỗi các biến được tạo ra ở mỗi lần gọi riêng biệt không can thiệp đến nhau.
Tính chất local chỉ áp dụng cho các biến được khai báo với từ khóa `var` bên trong function. Các biến được khai báo bên ngoài `function` được gọi là `global`, các biến này có thể được sử dụng ở mọi nơi trong chương trình. Có thể truy cập các biến như vậy từ bên trong `function`, miễn là trong `function` không khai báo một biến local có cùng tên.
Đoạn code sau chứng tỏ điều này. Nó định nghĩa và gọi 2 `function`, cả 2 `function` này đều gán một giá trị cho biến `x`. Function đầu tiên khai báo biến `x` là biến local, vì vậy các thay đổi chỉ có tác dụng ở mức độ local tức là bên trong fuction. `Function` thứ 2 không khai báo biến `x` là biến local, vì vậy mọi sự thay đổi `x` bên trong fucntion đều sẽ ảnh hưởng đến giá trị của biến `x` đã khai báo trên cùng.

``` javascript
var x = "outside";

var f1 = function() {
  var x = "inside f1";
};
f1();
console.log(x);
// → outside

var f2 = function() {
  x = "inside f2";
};
f2();
console.log(x);
// → inside f2
```

Hành vi này giúp ngăn chặn sự can thiệp ngẫu nhiên giữa các chức năng. Nếu tất cả các biến đều được chia sẻ trong toàn bộ chương trình thì sẽ gặp nhiều khó khăn để đảm bảo rằng không có một tên biến nào lại được sử dụng cho hai mục đích khác nhau.Nếu bạn sử dụng lại một tên biến, bạn sẽ thấy nhiều kết quả không mong muốn và code của bạn sẽ rối tung lên. Việc xử lý biến local xuất hiện trong `function` làm cho chương trình có thể đọc hiểu mà không cần lo lắng đến các thành phần khác ngoài `function`.

### Nested Scopes

Javascript không chỉ phân biệt giữa biến local và global. `Function` có thể được tạo ra bên trong các function khác, tạo ra mức độ local của `function`.

Ví dụ, hàm khá vô lý sau có 2 `function` bên trong nó:

```javascript
var landscape = function() {
  var result = "";
  var flat = function(size) {
    for (var count = 0; count < size; count++)
      result += "_";
  };
  var mountain = function(size) {
    result += "/";
    for (var count = 0; count < size; count++)
      result += "'";
    result += "\\";
  };

  flat(3);
  mountain(4);
  flat(6);
  mountain(1);
  flat(1);
  return result;
};

console.log(landscape());
// → ___/''''\______/'\_
```

Các function `flat` và `mountain` có thể "nhìn thấy" biến `result`, vì 2 hàm này nằm bên trong hàm định nghĩa nó.Nhưng chúng không thể "nhìn thấy" các biến số của nhau vì chúng nằm bên ngoài phạm vi của nhau. Các biến bên ngoài function `landscape` sẽ không thấy bất kì biến nào bên trong `landscape`.
Cách tiếp cận biến và hàm  như trên được gọi là `lexical scoping`.
Những lập trình viên có kinh nghiệm với các ngôn ngữ khác có thể mong đợi các đoạn code trong các dấu ngoặc tạo ra một môi trường mới. Nhưng trong JavaScript, function là thứ duy nhât tạo ra một phạm vi mới. Bạn được phép sử dụng các khối code đứng tự do.

```javascript
var something = 1;
{
  var something = 2;
  // Do stuff with variable something...
}
// Outside of the block again...
```

Biến `something` bên trong block giống biến ở bên ngoài block. Thực tế việc này được cho phép và nó chỉ có ích khi block này là phần điều kiện của lệnh if hoặc vòng lặp.
Version tiếp theo của JavaScript sẽ giới thiệu từ khóa `let`, nó hoạt động như `var` nhưng chỉ có tác dụng trong vùng scope cận kề với nó trong khi với `var` thì biến có thể truy cập được ở bất kì vị trí nào trong hàm.
