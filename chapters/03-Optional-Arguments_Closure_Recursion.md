---
## Chapter 3: (Tiếp tục)

### Biến tùy chọn (Optional Arguments)

Đoạn code bên dưới được chấp nhận và chạy mà không báo lỗi:

```javascript
alert("Hello", "Good Evening", "How do you do?");
```

Hàm `alert` chỉ chấp nhận một đối số. Tuy nhiên, khi bạn gọi hàm như trên, nó sẽ không báo lỗi mà bỏ qua các đối số khác và chỉ hiện "Hello".

JavaScript hoàn toàn tự do về số lượng đối số mà bạn truyền vào một hàm. Nếu bạn truyền quá nhiều, đối số dư sẽ bị bỏ qua. Nếu bạn truyền quá ít, tham số bị thiếu sẽ được gán bằng giá trị chưa xác định (mặc định).

Nhược điểm là chúng ta sẽ có khả năng, thậm chí vô tình truyền sai số lượng đối số và không ai báo với bạn về chuyện đó.

Tuy nhiên, ưu điểm của hành động này là có thể sử dụng các đối số "tùy chọn". Ví dụ, một cách tình lũy thừa có thể được gọi bởi 2 đối số hoặc 1 đối số, trong trường hợp này giả sử số mũ là 2 và hàm này giống như tính bình phương.
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

Trong chương tiếp theo, chúng ta sẽ tìm hiểu cách mà hàm dùng để truyền chính xác danh sách đối số. Điều này rất hữu ích vì nó cho hàm chấp nhận một số lượng đối số tùy ý. Ví dụ như `console.log`, nó xuất tất cả các giá trị mà nó nhận.

```javascript
console.log("R", 2, "D", 2);
// → R 2 D 2
```

### Tính bao đóng (Closure)

Khả năng xử lý các hàm như là các giá trị, kết hợp với thực tế là biến cục bộ được tái tạo" (“re-created”) mỗi khi một hàm được gọi. Một câu hỏi thú vị là điều gì sẽ xảy ra với các biến cục bộ khi cuộc gọi hàm đã tạo ra chúng không còn hoạt động?

Đoạn code sau đây cho thấy một ví dụ về điều này. Nó định nghĩa một hàm tên wrapValue, chức năng là tạo ra một biến cục bộ. Sau đó nó sẽ trả về một hàm có thể truy cập và trả biến cục bộ này về.

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

Điều nay được cho phép và hoạt động như bạn mong muốn, biến vẫn có thể được truy cập. Thực tế, nhiều trường hợp của biến có thể tồn tại cùng lúc, đó là một ví dụ khác của ý tưởng: biến cục bộ thực sự tái tạo cho mỗi lần gọi, các lần gọi không thể trùng với một biến cục bộ khác.

Tính năng này có thể tham chiếu một ví dụ/yê cầu cụ thể của các biến cục bộ trong một hàm kèm theo - gọi là bao đóng (closure). Một hàm mà "đóng" thì một số biến cục bộ được gọi là closure. Hành vi này không chỉ giải phóng bạn khỏi phải lo lắng về thời gian sống của các biến mà còn cho phép  bạn sử dụng sáng tạo các giá trị của hàm.

Với một chút thay đổi, chúng ta có thể biến các ví dụ trước thành một cách để tạo ra các hàm mà nhân lên bởi một số lượng tùy ý.

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

Các biến localVariable từ ví dụ wrapValue rõ ràng là không cần thiết bởi vì chính tham số là một biến cục bộ.

Nghĩ về các chương trình như thế này để lấy một số ví dụ. Một mô hình tinh thần (mental model) tốt là suy nghĩ về các từ khóa hàm như "đóng băng" đoạn code trong body của hàm và gói nó vào một package (giá trị chức năng - the function value). Vì vậy, khi bạn đọc `return function(...) {...}`, nghĩ về nó như là trả về một xử lý cho một phần tính toán, đóng băng nó lại để sử dụng sau.

Trong ví dụ, hàm `multiplier` trả về một mảnh đã được đóng băng của đoạn code mà nó sẽ được lưu trữ 2 lần. Dòng cuối cùng gọi giá trị trong biến này, dẫn đến đoạn code đóng băng `(return number * factor;)` được kích hoạt. Nó vẫn tiếp tục truy cập vào biến `factor` được tạo khi gọi hàm `multiplier`, thêm vào đó, nó cũng truy cập vào đối số được truyền thông qua tham số `number` khi nó được "phá băng".


## Đệ quy (Recursion)

Một hàm có thể gọi chính nó là điều hoàn toàn có thể, miễn là nó đảm bảo không tràn ngăn xếp. Một hàm mà có thể gọi chính nó được gọi là đệ quy. Đệ quy cho phép một số hàm có thể viết bằng các cách khách nhau. Ví dụ, đây là một cách thực hiện hàm `power`:

```javascript
function power(base, exponent) {
  if (exponent == 0)
    return 1;
  else
    return base * power(base, exponent - 1);
}

console.log(power(2, 3));
// → 8
```
`(Note: Thanh lịch - Code đẹp, khoa học)`
Cách này thì gần giống với định nghĩa lũy thừa trong toán học và được cho là mô tả khái niệm một cách thanh lịch hơn so với việc dùng vòng lặp cho các biến. Hàm này gọi nó nhiều lần với nhiều đối số khác nhau để lặp lại phép nhân.

Tuy nhiên cách thực hiện này có một vấn đề quan trọng là: thực hiện nó trong JavaScript sẽ chậm đi khoảng 10 làn so với dùng vòng lặp. Chạy một vòng lặp đơn giản là ít tốn hơn rất nhiều so với gọi một hàm nhiều lần. 

Vấn đề so sánh tốc độ với thanh lịch là một vấn đề thú vị. Bạn có thể xem đó như một loại so sánh giữa "thân thiện với con người" và "thân thiện với máy". Hầu như bất kỳ chương trình có thể được thực hiện nhanh hơn bằng cách làm cho nó lớn hơn và phức tạp hơn. Các lập trình viên phải quyết định một sự cân bằng thích hợp.

Trong trường hợp của hàm `power` trước, phiên bản "khiếm nhã" (looping) vẫn còn khá đơn giản và dễ dọc. Nó không có ý nghĩa nhiều để thay thế bởi phiên bản đệ quy. Thông thường, mặc dù, một chương trình với một khái niệm phức tạp như vậy thì thỏa hiệp để từ bỏ hiệu suất để làm cho chương trình trở nên đơn giản là một sự lựa chọn hấp dẫn.

Nguyên tắc cơ bản đã được lặp đi lặp lại bởi nhiều lập trình viên và cùng với đó tôi hoàn toàn đồng ý: đừng quá lo lắng về hiệu năng cho đến khi bạn biết chắc chắn rằng chương trình quá chậm. Nếu vậy, tìm ra các phần chiếm nhiều thời gian nhất, và bắt đầu chuyển từ "thanh lịch"  sang "hiệu năng" ở những phần này.

Tất nhiên, điều này không có nghĩa là bạn nên bắt đầu hoàn toànbỏ qua hiệu năng. Trong nhiều trường hợp, như hàm `power`, không quá đơn giản để để đạt được cách tiếp cận "thanh lịch". Và đôi khi, một lập trình viên kinh nghiệm có thể thấy ngay rằng một cách tiếp cận đơn giản không bao giờ là đủ nhanh.

The reason I’m stressing this is that surprisingly many beginning programmers focus fanatically on efficiency, even in the smallest details. The result is bigger, more complicated, and often less correct programs, that take longer to write than their more straightforward equivalents and that usually run only marginally faster.

Lý do tôi nhấn mạnh điều này là đáng ngạc nhiên bởi vì nhiều lập trình viên bắt đầu tập trung một cách cuồng tín vào hiệu quả, ngay cả trong những chi tiết nhỏ nhất. Kết quả dẫn đến là chương trình lớn hơn, phức tạp hơn, và thường ít đúng, mà phải mất nhiều thời gian để viết hơn so với cách viết tương đương đơn giản hơn và thường chỉ để chạy nhẹ nhanh hơn.

Nhưng đệ quy không phải là luôn luôn chỉ cần một thay thế kém hiệu quả hơn so với vòng lặp. Một số vấn đề được giải quyết với đệ quy dễ dàng hơn so với các vòng lặp. Thường xuyên nhất là những vấn đề đòi hỏi phải khám phá, xử lí nhiều "nhánh", mỗi nhánh trong số đó có thể chia ra thành nhiều nhánh nữa.

Hãy xem xét câu đố này: bắt đầu từ số 1 và lặp đi lặp lại, hoặc thêm 5 hoặc nhân với 3, một số lượng vô hạn các số mới có thể được tạo ra. Làm thế nào để viết một hàm như vậy, cho một số, thử tìm một chuỗi các phép cộng và phép nhân để sản xuất ra con số đó? Ví dụ, số 13 có thể đạt được bằng cách đầu tiên nhân với 3 và sau đó thêm số 5 hai lần, trong khi đó số 15 không thể tìm được.

Và đây là cách giải đệ quy:
```javascript
function findSolution(target) {
  function find(start, history) {
    if (start == target)
      return history;
    else if (start > target)
      return null;
    else
      return find(start + 5, "(" + history + " + 5)") ||
             find(start * 3, "(" + history + " * 3)");
  }
  return find(1, "1");
}

console.log(findSolution(24));
// → (((1 * 3) + 5) * 3)
```
Lưu ý rằng chương trình này không nhất thiết phải tìm chuỗi ngắn nhất của các phép tính. Nó thỏa mãn khi nó tìm thấy bất kỳ chuỗi nào. 

Tôi không nhất thiết mong bạn hiểu cách nó hoạt động ngay lập tức. Nhưng chúng ta hãy làm việc thông qua nó, bởi vì đo là một bài tập tuyệt vời trong suy nghĩ đệ quy.

Các hàm bên trong thực sự không đệ quy thực. Phải mất hai đối số - số lượng hiện tại và một chuỗi ghi lại cách chúng ta đạt đến số lượng và trả về này hoặc là một chuỗi cho thấy làm thế nào để đạt được mục tiêu hoặc null.

Để làm điều này, hàm phải thực hiện một trong ba hành động. Nếu số hiện tại là số cần tìm, lịch sử hiện tại là một cách để đạt được số cần tìm, vậy đơn giản chỉ cần trả về kết quả. Nếu số hiện tại lớn hơn số cần tìm, điều đó trở nên vô nghĩa trong các bước thử tiếp theo gì bởi vì phép cộng và nhân chỉ làm số đó lớn hơn. Và cuối cùng, nếu chúng vẫn bé hơn số cần tìm, hàm sẽ thử cả hai cách có thể là bắt đầu từ số hiện tại, bằng cách gọi chính nó hai lần, mỗi lần cho phép những bước tiếp theo thực hiện. Nếu lần gọi đầu tiên trả về một cái gì đó không phải là null thì nó được trả về. Nếu không, lần gọi thứ hai được trả về - cho dù nó tạo ra một chuỗi hoặc null.

Để hiểu rõ hơn về cách mà hàm này tạo ra kết quả mà chúng ta đang tìm kiếm, hãy xem tất cả các lần gọi hàm để hiểu cách chúng thực hiện khi tìm kiếm lời giải cho con số 13.


```javascript
find(1, "1")
  find(6, "(1 + 5)")
    find(11, "((1 + 5) + 5)")
      find(16, "(((1 + 5) + 5) + 5)")
        too big
      find(33, "(((1 + 5) + 5) * 3)")
        too big
    find(18, "((1 + 5) * 3)")
      too big
  find(3, "(1 * 3)")
    find(8, "((1 * 3) + 5)")
      find(13, "(((1 * 3) + 5) + 5)")
        found!
```

Thụt đầu dòng cho thấy độ sâu của stack. Lần đầu tiên tìm thấy được gọi là nó tự gọi hàm hai lần để tìm ra những giải pháp bắt đầu bằng `(1 + 5)` và `(1 * 3)`. Lần gọi hàm đầu tiên cố gắng để tìm một giải pháp mà bắt đầu bằng `(1 + 5)`, và sử dụng đệ quy, tìm ra mọi giải pháp đó mang lại một số nhỏ hơn hoặc bằng số cần tìm. Kể từ khi nó không tìm thấy một giải pháp đúng số cần tìm, nó trả về null cho lần gọi hàm đầu tiên. Toán tử `||` là nguyên nhân để lần gọi làm mà trường hợp `(1 * 3)` xảy ra. Lần tìm kiếm này may mắn hơn lần gọi đệ quy đầu tiên của chính nó, thông qua một lần gọi đệ quy khác, nó gần hơn số cần tìm - số `13`. Đây gọi đệ quy trong cùng trả về một chuỗi, và mỗi toán tử `||` trong các lần gọi trung gian, các chuỗi được truyền qua cùng, cuối cùng trở về giải pháp của chúng ta.
