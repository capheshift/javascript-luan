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

### Tham số tùy chọn
Đoạn code bên dưới được cho phép và có thể thực thi suông sẻ mà không gặp bất cứ vấn đề gì.
```javascript
alert("Hello", "Good Evening", "How do you do?");
```
Do hàm alert chỉ nhận một tham số truyền vào nên trong ví dụ trên các tham số khác đã bị bỏ qua và khi thực thi ta chỉ nhận được kết qủa là "Hello".

Javascript rất sáng suốt trong việc đặt tham số, nếu như bạn đặt qúa nhiều tham số vào một hàm, thì một số tham số không cần thiết sẽ bị bỏ qua và nếu bạn đặt qúa ít tham số thì những tham số bị thiếu sẽ có gía trị mặc định là undifined. Mặc khác đây cũng chính là nhược điểm của javascript bởi vì nếu bạn đặt sai số lượng tham số và một hàm thì cũng không ai thông báo cho bạn biết, điều đó có thể làm chương trình của bạn chạy không chính xác.

Ngược lại lợi ích của nó là có thể được sử dụng để tạo ra một hàm cho phép lựa chọn tham số linh hoạt. Như ví dụ bên dưới hàm power có thể được gọi với 2 tham số hoặc chỉ một tham số, trong trường hợp truyền vào 1 tham số thì exponent sẽ được gán mặc định là 2.
```javascript
function power(base, exponent) {
  if (exponent == undefined)
    exponent = 2;
  var result = 1;
  for (var count = 0; count < exponent; count++)
    result *= base;
  return result;
}

console.log(power(4));
// → 16
console.log(power(4, 3));
// → 64
```
Trong chương kế tiếp chúng ta sẽ thấy được cách lấy chính xác danh sách các tham số đã được truyền vào. Ví dụ: console.log sẽ thực hiện điều đó, nó xuất ra tất cả các gía trị mà nó nhận được.
```javascript
console.log("R", 2, "D", 2);
// → R 2 D 2
```

### Closure
Đây là khả năng xử lý các hàm như là gía trị, liên hệ với thực tế ta thấy biến cục bộ sẽ được tái tạo lại mỗi khi hàm được gọi, điều này gợi cho chúng ta một câu hỏi thú vị là điều gì sẽ xảy ra với các biến cục bộ khi lời gọi hàm đã tạo ra chúng không còn hoạt động?

Bên dưới là một đoạn code minh họa cho điều đó, nó định nghĩa một hàm wrapValue, tạo ra một biến cục bộ. Sau đó nó trả về một hàm, mà hàm này sẽ truy cập đến biến cục bộ và trả về gía trị của biến này.
```javascript
function wrapValue(n) {
  var localVariable = n;
  return function() { return localVariable; };
}

var wrap1 = wrapValue(1);
var wrap2 = wrapValue(2);
console.log(wrap1());
// → 1
console.log(wrap2());
// → 2
```
Điều này được cho phép và làm việc như bạn hy vọng, các biến vẫn có thể được truy cập. Thật vậy, nhiều trường hợp các biến có thời gian sống là như nhau, đó là một minh họa tốt cho khái niệm biến cục bộ được tái tạo lại sau mỗi lời gọi hàm, các lời gọi hàm khác nhau không thể tác động đến các biến cục bộ của nhau.

Tính năng này có thể được liên hệ đến một trường hợp đặc biệt của biến cục bộ trong một hàm kèm theo được gọi là closure. Một hàm đặt trên biến cục bộ được gọi là một closure. Điều này không những giúp chúng ta khỏi phải lo lắng về thời gian sống của các biến mà còn cho phép chúng ta sáng tạo trong việc sử dụng các gía trị của hàm.

Với một chút thay đổi, chúng ta có thể biến các ví dụ trước thành một hàm mà có thể thực hiện việc nhân một số tùy ý.
```javascript
function multiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

var twice = multiplier(2);
console.log(twice(5));
// → 10
```
Biến cục bộ trong ví dụ hàm wrapValue là một biến được khai báo tường minh không cần thiết vì một tham số là một biến cục bộ của chính nó.

### Đệ quy
Cho phép một hàm gọi chính bản thân nó, miền là nó được chú ý để không làm tràn stack. Đệ quy cho phép ta viết một số hàm với phong cách khác nhau. Lấy ví dụ bằng việc thay đổi hàm power như sau:
```javascript
function power(base, exponent) {
  if (exponent == 0)
    return 1;
  else
    return base * power(base, exponent - 1);
}
```
Điều này khá giống với việc xác định lũy thừa trong toán học và các khái niệm của nó được mô tả một cách trang trọng hơn so với các biến thể lặp khác. Các hàm tự gọi chính nó nhiều lần với các tham số khác nhau để có được các phép nhân lặp đi lặp lại.

Nhưng việc triển khai đệ quy sẽ gây ra một vấn đề nghiêm trọng: trong triển khai javascript truyền thống, nó chậm hơn gấp 10 lần so với việc dùng vòng lặp. Thực thi một vòng lặp đơn giản sẽ tiết kiệm hơn nhiều so với việc lặp đi lặp lại một hàm.

Vấn đề về tốc độ so với sự sang trọng là một trong những điều khá thú vị. Hầu như bất kì chương trình nào cũng có thể được thực hiện nhanh hơn bằng cách làm cho nó lớn hơn và phức tạp hơn. Các lập trình viên sẽ phải quyết định để có được sự cân bằng thích hợp.

Trong trường hợp hàm power thì việc lặp vẫn còn đơn giản và dễ dàng đọc được. Nó không có nhiều ý nghĩa để thay thế nó bằng đệ quy. Thông thường một chương trình với những khái niệm phức tạp như vậy mà có thể từ bỏ đi được một số hiệu qủa để làm chương trình đơn giản hơn là một sự lựa chọn hấp dẫn. Đôi khi với một lập trình viên giàu kinh nghiệm có thể thấy ngay rằng một cách tiếp cận đơn giản thì không bao giờ đủ nhanh.

Một số lập trình viên lại tập trung qúa nhiều vào hiệu qủa, kể cả những chi tiết nhỏ nhặt nhất. Điều này sẽ làm tốn rất nhiều thời gian để viết hơn là việc sử dụng các thuật toán đơn giản mà thường chạy nhanh hơn. Đệ quy không phải lúc nào cũng kém hiệu qủa hơn vòng lặp. Với một số vấn đề thì giai quyết bằng đệ qui sẽ dễ dàng hơn so với dùng vòng lặp. 

### Summary
