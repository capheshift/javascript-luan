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

