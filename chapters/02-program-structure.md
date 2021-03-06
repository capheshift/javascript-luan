
---
## Chapter 2: Program Structure
HÀ
---

THẮNG
---

### Control flow
Khi chương trình của bạn có nhiều hơn một thông báo, các báo cáo được thực hiện, dự đoán, từ trên xuống dưới. Như một ví dụ cơ bản, chương trình này có hai câu.

![alt text][logoStraight]

[logoStraight]: ../img/controlflow_straight.png "Logo Title Text 2"

Hàm số chuyển đổi một giá trị cho một số. Chúng ta cần chuyển đổi mà vì kết quả nhanh chóng là một chuỗi giá trị, và chúng tôi muốn có một số. Có chức năng tương tự được gọi là chuỗi và Boolean chuyển đổi giá trị để các loại.

### Conditional execution
Thực hiện báo cáo theo thứ tự đường thẳng không phải là lựa chọn duy nhất chúng ta có. Một cách khác là điều kiện thực hiện, nơi mà chúng tôi lựa chọn giữa hai con đường khác nhau dựa trên một giá trị Boolean.

![alt text][logoIf]

[logoIf]: ../img/controlflow_if.png "Logo Title Text 2"

Điều kiện thực hiện được viết với nếu từ khóa trong JavaScript. Trong trường hợp đơn giản, chúng tôi chỉ muốn có một số mã được thực hiện khi và chỉ khi, một điều kiện nhất định nắm giữ. Ví dụ, trong các chương trình trước đây, chúng ta có thể muốn hiển thị các hình vuông của các đầu vào chỉ khi đầu vào thực sự là một con số.

```javascript
theNumber = Number(prompt("Pick a number", ""));
alert("Your number is the square root of " +
      theNumber * theNumber);
```
Các từ khóa nếu thực hiện hoặc bỏ qua một tuyên bố tùy thuộc vào giá trị của một biểu thức Boolean. Các biểu hiện quyết định được viết sau từ khóa, giữa dấu ngoặc đơn, sau đó là tuyên bố để thực thi.

Hàm `isNaN` chức năng là một hàm JavaScript chuẩn mà trả về đúng chỉ khi tham số đó được cho là `NaN`. Các số chức năng sẽ xảy ra để trả lại `NaN` khi bạn cung cấp cho nó một chuỗi mà không đại diện cho một số hợp lệ.

Bạn sẽ thường xuyên không chỉ có mã thực thi khi một điều kiện đúng, nhưng cũng đang xử lý các trường hợp khác. Con đường thay thế này được đại diện bởi các mũi tên thứ hai trong biểu đồ. Các khác từ khóa có thể được sử dụng, cùng với nếu, để tạo ra hai riêng biệt, đường dẫn thực thi thay thế.

```javascript
var theNumber = Number(prompt("Pick a number", ""));
if (!isNaN(theNumber))
  alert("Your number is the square root of " +
        theNumber * theNumber);
else
  alert("Hey. Why didn't you give me a number?");
```
Nếu chúng tôi có hơn hai con đường để lựa chọn, nhiều nếu / khác cặp có thể được "xích" lại với nhau. Dưới đây là một ví dụ:

```javascript
var num = Number(prompt("Pick a number", "0"));
      if (num < 10)
        alert("Small");
      else if (num < 100)
        alert("Medium");
      else
        alert("Large");
```
Chương trình đầu tiên sẽ kiểm tra xem num là ít hơn 10. Nếu có, nó chọn chi nhánh đó, cho thấy "Small", và được thực hiện. Nếu không, nó có khác chi nhánh, mà bản thân nó có chứa một giây nếu. Nếu điều kiện thứ hai (<100) nắm giữ, đó có nghĩa là số lượng là từ 10 đến 100, và "Medium" được hiển thị. Nếu không, thứ hai, và cuối cùng, khác chi nhánh được chọn.

### While and Do Loops
*Xem một chương trình in tất cả các số chẵn từ 0- 12. Một cách để viết chương trình là như sau.*
```javascript
console.log(0);
console.log(2);
console.log(4);
console.log(6);
console.log(8);
console.log(10);
console.log(12);
```
*Những dòng code ở trên hoạt động bình thường nhưng chúng t cần một chương trình đơn giản hơn cũng với những chức năng là in ra các số chẵn từ 0-12.*

Nếu như chúng tôi cần in ra các số chẵn từ 0-1000 thì sao ? Chắc chắn là khi áp dụng những dòng code ở trên vào đây thì nó sẽ không kả thi.
Những gì chúng ta cần ở đây là có thể lặp lại được những dòng code .Đây là một hình thức kiểm soát luồng `control flow` được gọi là vòng lặp `loop`.
![alt text][logoLoop]

[logoLoop]: ../img/controlflow_loop.png "Logo Title Text 2"

*Vòng lặp cho phép chúng ta quay lại một vài điểm trong chương trình trước và lặp lại nó nới chương trình hiện tại của chúng ta. Nếu chúng ta kết hợp một biến đếm , chúng ta có thể làm như sau:*
```javascript
var number = 0;
while(number <=12){
  console.log(number);
  number=number +2;
}
//-> 0
//->2
//....
```
Một tuyên bố bắt đầu với các từ khóa trong khi tạo ra một vòng lặp.`while` được theo sau bởi một biêủ thức trong ngoặc đơn và sau đó là một điều kiên, giống như `if`.Các vòng lặp thực hiện điều kiện rằng miền là biểu thức gặp một giá trị nào đó là `true` khi nó chuyển đổi qua `Boolean` type.

Trong vòng lặp, chúng ta muốn in cả số hiện tại và thêm vào 2 cho biến
của chúng ta.Tuy nhiên khi chúng ta thực thi nhiều  câu lệnh trong vòng lặp, chúng ta để chúng ở trong ngoặc nhọn `({and})`.Dấu ngoặc làm cho câu lệnh thực hiện những gì trong biểu thức: họ nhóm chúng lại với nhau, làm cho nó đếm chính xác tới từng câu lệnh một.Một chuỗi các câu lệnh được để trong dấu ngoặc được gọi là một `block`.

Nhiều lập trình viên javascipt để vòng lăj đơn hoặc `if` trong ngoặc.Họ làm điều này cả vì lợi ích của sự nhất quán và tránh việc phải thêm hoặc lại bỏ dấu ngoặc khi họ thay đổi số lượng câu lệnh .

Số biến chứng tỏ cách thức một biến có thể theo dõi sự tiến bộ của một chương trình. Mỗi lần vòng lặp được lặp lại con số đẵ được tăng lên 2. Sau đó , vào mỗi lần lặp lại, nó được so sánh với con số 12 để quyết định xem chương trình đã thực hiện tất cả các câu lệnh cần làm hay chưa.

Đó là một ví đã làm một vài điều thực sự hữu ích, bây giờ chúng ta có thể viết chương trình tính toán và hiển thị gái trị của 2^10 (2 mũ 10). Chúng ta sử dụng 2 biến : một để theo dõi kết quả và một để đếm bao nhiêu lần chúng ta đã nhân kết quả này với 2. Các thử nghiệm dù có biến thứ 2 đã đạt được 10 chưa và cập nhật cả 2 biến.

Ví dụ
```javascript
var result = 1;
var counter = 0;
while (counter < 10) {
  result = result * 2;
  counter = counter + 1;
}
console.log(result);
// → 1024
```

Biến đếm có thể cũng bắt đầu bằng 1 và kiểm tra tới <= 10, nhưng những lí do đó sẽ trở nên rõ ràng hơn trong chương 4, nó là một ý tưởng tốt để có thể sử dụng để đếm từ 0.

Vòng lặp `do` là một cấu trúc điều khiển tương tự như vòng lặp `while`. Nó khác biệt hơn ở một điểm : một vòng lặ `do` luôn luôn thực thi ít nhất một lần, và nó bắt đầu kiểm tra xem nó nên dừng lại ở đâu chỉ sau lần thực hiện đầu tiên. Để phản ánh điều này , các thử nghiệm xuất hiện sau nội dung của vòng lặp:

```javascript
do {
  var yourName = prompt("Who are you?");
} while (!yourName);
console.log(yourName);
```

Đây là chương trình sẽ yêu cầu nhập vào một tên `yourName`. Nó sẽ hỏi bạn một lần nữa cho đến khi nó nhận thông báo không phải là chuỗi rỗng `yourName != null`. Áp dụng với toán tử `!` nó sẽ chuyển đôỉ giá trị từ kiểu `Boolean` trước khi phủ định nó, và tât cả các chuỗi chấp nhận `" "` chuyển đổi qua `true`. Ở đây nghĩa là `loop` tiếp tục chạy mãi đến khi bạn cung cấp một cái tên `name` rằng không để `yourName` là trống. Trong thực tế, ngay cả ngắt dòng trong chương trình cũng là do mình tùy chọn.

### Thụt lề code (Indenting Code)
Bạn có thể nhận thấy những khoảng trống tôi đã đặt ở phía trước một vài câu lệnh. Trong JavaScript, chúng không có bắt buộc, máy tính sẽ chấp nhận các chương trình tốt mà không có nó.Bạn có thể viết một chương trihf như là một đường dài duy nhất nếu bạn cảm thấy thích nó. Vai trò của sự thụt vào bên trong khối là làm cho cấu trúc của mã nguồn nổi bật và dễ đọc. Trong mã phức tạp, nơi khối mới được mở ra bên trong các khối khác , nó có thể trở nên khó nhìn thấy nơi một khối kết thúc và một khối bắt đầu. Với thụt đầu dòng thích hợp ta sẽ có cái nhìn trực quan hơn về chương trình. Tôi thích sử dụng 2 khoảng trắng cho mỗi khối mở, và một số người sử dụng các kí tự `tab`.

### Breaking out of a loop

Trong phần này tôi sẽ giới thiệu tới các bạn một dạng khác của `loop`.

Có một tuyên bố đặc biệt được gọi là `break` rằng có tác dụng ngay lập tức nhảy ra khỏi vòng lặp đó.

Một chương trình đơn giản minh họa cho câu lệnh break. Nó tìm những số đầu tiên là cả 2 lớn hơn 20 và chia hết cho 7.

```javascript
for (var current = 20; ; current++) {
  if (current % 7 == 0)
    break;
}
console.log(current);
// → 21
```

Sử dụng toán tử `%` là một cách dễ dàng để kiểm tra xem một số chia hết cho số khác. Nếu có, phần còn lại của phép chia là `0`.

Cấu trúc của `for` xây dựng trong ví dụ không có một phần để kiểm tra kết thúc vòng lặp. Điều này làm cho vòng lặp của chúng ta sẽ không bao giờ dừng lại trừ khi các lệnh break được thực thi.

Nếu bạn đã rời câu lệnh khỏi câu lệnh `break` đó hoặc vô tình viết một điều kiênj là luôn luôn `true`, chương trình của bạn sẽ bị mắc kẹt trong một vòng lặp vô hạn. Một chương trình sẽ bị mắc kẹt trong vòng lặp mãi mà không bao giờ kết thúc , nó thường là những điều xấu.

Nếu bạn tạo ra một vòng lặp vô hạn trong một trong các ví dụ trên hay ở trong sách này, bạn sẽ thường được hỏi là có muốn dừng lại câu lệnh sau một vài giây. Nếu thất bại, bạn sẽ phải đóng các tab mà bạn đang làm việc hoặc trên một số trình duyệt của bạn để thu hồi.

Các từ khóa `continue` tương tự như `break`, trong đó nó ảnh hưởng tới xử lí của một vòng lặp. Khi tiếp tục được bắt gặp trong một vòng lặp , kiểm soát để nhảy ra khỏi vòng lặp và tới các câu lệnh tiếo theo trong vòng lặp.




TÂN
---

---
### Summary

Bây giờ bạn biết rằng chương trình xây dựng dựa trên các khối lệnh, có thể ngay cả chính bản thân nó chứa nhiều khối lệnh bên trong khác. Khi 1 lệnh đặt sau 1 lệnh khác, chương trình sẽ chạy từ trên xuống. Bạn có thể làm gián đoạn chương trình bằng các sử dụng các khối lệnh điều kiện (`if`, `else` hoặc `switch`) và vòng lặp (`while`, `do` hoặc `for`).

Các biến có thể được dùng để lưu trữ những mảnh dữ liệu bằng một định danh (name) và chúng sẽ hữu ích để theo dõi trạng thái trong chương trình của bạn.

Hàm (Function) là một giá trị đặc biệt có chức năng đóng gói thành các mảnh nhỏ của một chương trình. Bạn có thể gọi hàm bằng các viết `functionName(argument1, argument2), hàm có thể chạy một khối lệnh hoặc đơn giản là trả ra một giá trị.
