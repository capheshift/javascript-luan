
---
## Chapter 1: Values, Types, and Operators

*Trong thế giới máy tính, chỉ có một thứ duy nhất là dữ liệu (data). Bạn có thể đọc, sửa, tạo mới dữ liệu - nhưng bất cứ thứ gì khác không phải là dữ liệu, đơn giản là nó không tồn tại. Tất cả dữ liệu được lưu trữ trong một thứ tự dài của các bits.*

### Values
*Tưởng tượng chúng ta có một đại dương chứa các bits. 1 máy tính cổ điển có hơn 30 tỉ bits lưu trữ.*

![alt text](../img/bit-sea.png "Logo Title Text 1")

Để có thể làm việc với khối lượng bits lớn mà không làm hao hụt nó, bạn có thể chia chúng ra thành các phần nhỏ đại diện cho các mảnh thông tin. Trong môi trường của Javascript, các mảnh đó được gọi là Values ( giá trị). Tất cả những giá trị này được tạo nên bởi bits, giữ những vai trò khác nhau. Mỗi values có một kiểu giá trị (type) để xác định vai trò của chính nó.

Có sáu kiểu giá trị cơ bản của values trong Javascript: `numbers` (số), `strings` (chuỗi kí tự), `Booleans` (giá trị `true`/ `false` (đúng/ sai)), `objects` (đối tượng), `functions` (hàm) và `undefined values` (giá trị chưa xác định).

Để tạo 1 value, bạn chỉ đơn giản là gọi tên của nó, chỉ cần gọi tên, và bạn đã có 1 giá trị. Mỗi values được lưu trữ ở đâu đó, và nếu bạn muốn sử dụng một số lượng khổng lồ của chúng cùng thời điểm, có lẽ bạn sẽ gặp một chút vấn đề với với việc vượt quá số bits. May mắn là vấn đề này chỉ xảy ra nếu bạn cần tất cả chúng cùng một lúc. Trong một khoảng thời gian dài không sử dụng đến, nó sẽ được giải phóng.

### Number

*Trong JavaScript Number là một kiểu dữ liệu cũng là một object. Nó có 2 dạng là số có dấu chấm động hoặc không có dâu chấm động.*

Số thập phân được biểu diển bởi dấu chấm

`19.92`

Nếu số quá lớn thì ta có thể dùng số mũ để biểu diễn.

`123e5; // this is 12300000`

### Arithmetic (toán học)

*Tương tự như các ngôn ngữ khác, JavaScript cũng thực hiện `x`, `/` trước `+`, `-` sau, ưu tiên biểu thức trong dấu ngoặc trong đa thức. `%` là chia lấy phần dư*

```javascript
var x = (1+2)*10 + 5; // x = 35
x % 10;  // = 5
```

### Special Number

*Có 3 giá trị đặc biệt trong JavaScript:*

`Infinity` dương vô cùng.

`-Infinity` âm vô cùng.

`NaN` (không phải là số) là cái gì đó không tồn tại trong tập hợp R.

VD:  `var x = 0 / 0; // x NaN`
hay var x = x / x; // x `NaN`

### strings

*Một kiểu dữ liệu cơ bản nữa đó là `string`* một chuổi được bao bọc bởi dấu nháy đơn `'abc'` hoặc dấu nháy kép `"abc"`. Dấu backslach `(\)` được đùng để biểu diển những ký tự đặc biệt trong chuổi.

VD: 'CapheShift is a group of wonder coders.\nJoint to become a wonder coder'

đoạn code sẽ hiển thị như sau:

```CapheShipt is a group of wonder coders.
Joint to become a wonder coder```

Ta có thể dùng dấu `+` để cộng các chuổi lại với nhau

VD:
```javascript
var x = 'We '+'are '+'CapheShift'; // x = We are CapheShift
```

Có rất nhiều thao tác chuỗi ta sẽ tìm hiểu sâu hơn trong chương 4

### Unary operators (toán tử một ngôi)

*Có thể hiểu toán tử một ngôi là toán tử chỉ có một giá trị*

VD: `1 + 2; // là toán tử hai ngôi (binary operators)

typeof 1; // là toán tử một ngôi

Ta có các toán tử một ngôi sau:

- `delete` xóa một một đối tượng, thuộc tính của đối tượng, hoặc một phần tử trong mảng.

```javascript
var x = 123;
delete x;
delete Math.PI;
var num = [1, 2, 3, 4, 5];
delete num[2]; // xóa phàn tử thứ 2
```

- `typeof` trả về kiểu của đối tượng

```javascript
typeof 'abc'; // string
```

- `void` trả về không là gì cả của một biểu thức

VD:
```javascript
var x = function(){
  return 1+2;
};
console.log(x());  // 3
console.log(void(x())); //undefined
```

### Boolean

*Giống như mọi ngôn ngữ khác boolean có 2 giá trị true và false. được sử dụng cho một sự kiện chỉ có 2 khả năng xãy ra: co hoặc không*

TRÍ
---

---
### Summary

Chúng ta đã có cái nhìn sơ lược về 4 kiểu giá trị của Javascript trong chương 1 : `numbers`, `strings`, `Boolean`, và `undefined values`. Những giá trị được tạo ra bằng các gọi tên hoặc giá trị của nó, bạn có thể gộp chúng lại và thay đổi giá trị của chúng bằng các phép toán: (`+, -, *, /, và %`), phép nối chuỗi (`+`), so sánh (`==, !=, ===, !==, <, >, <=, >=`), và phép logic (`&&, ||`).
