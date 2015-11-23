### Growing functions
Thông thường có 2 cách để giới thiệu function trong chương trình.
Đầu tiên, bạn thấy mình viết những đoạn code giống nhau rất nhiều lần. Chúng ta muốn tránh những điều đó vì càng nhiều code thì đồng nghĩa với việc có nhiều không gian hơn cho các lỗi xuất hiện và người đọc code phải cố gắng nhiều hơn để hiểu được chương trình. Vì vậy khi có các chức năng lặp đi lặp lại ta gom chúng lại, đặt tên cho nó và đặt nó vào một function.
Thứ hai, bạn thấy bạn cần một số chức năng mà bạn chưa từng viết. Bạn sẽ bắt đầu bằng cách đặt tên các chức năng và sau đó bạn viết phần thân của nó. Bạn thậm chí có thể phải viết code sử dụng function đó trước khi xác định các chức năng chính của function đó.
Việc tìm một cái tên mô tả rõ ràng, ngắn gọn cho function là một việc không dễ dàng.Hãy cùng xem xét ví dụ sau.
Chúng ta muốn viết một chương trình in ra 2 số, số bò và số gà trong 1 trang trại, với từ *Cows* và *Chickens* sau các số đó và các số 0 đệm trước để các số này đều luôn là 3 chữ số.

`007 Cows`

`011 Chickens`

Rõ ràng chúng ta cần 1 function có 2 đối số.
```javascript
function printFarmInventory(cows, chickens) {
  var cowString = String(cows);
  while (cowString.length < 3)
    cowString = "0" + cowString;
  console.log(cowString + " Cows");
  var chickenString = String(chickens);
  while (chickenString.length < 3)
    chickenString = "0" + chickenString;
  console.log(chickenString + " Chickens");
}
printFarmInventory(7, 11);
```

Thêm `.length` vào sau chuỗi sẽ cho ta chiều dài của chuỗi đó. Vòng lặp while thêm các con số 0 trước các số cho đến khi có ít nhất 3 ký tự.
Nhiệm vụ hoàn thành. Nhưng nếu người nông dân ở trang trại nuôi thêm heo và muốn chúng ta mở rộng phần mềm để đếm cả số lợn. Chúng ta chắc chắn có thể làm điều đó.Thay vì copy và dán đoạn code xuống, chúng ta sẽ có 1 cách tốt hơn.
```javascript
function printZeroPaddedWithLabel(number, label) {
  var numberString = String(number);
  while (numberString.length < 3)
    numberString = "0" + numberString;
  console.log(numberString + " " + label);
}

function printFarmInventory(cows, chickens, pigs) {
  printZeroPaddedWithLabel(cows, "Cows");
  printZeroPaddedWithLabel(chickens, "Chickens");
  printZeroPaddedWithLabel(pigs, "Pigs");
}

printFarmInventory(7, 11, 3);
```
Nó hoạt động tốt. Nhưng cái tên `printZeroPaddedWithLabel` là cách đặt khá vụng về. Nó đề cập đến ba hàm, thêm số 0, và thêm một nhãn vào một chức năng duy nhất. Chúng ta nên chọn ra 1 khái niệm duy nhất.
```javascript
function zeroPad(number, width) {
  var string = String(number);
  while (string.length < width)
    string = "0" + string;
  return string;
}

function printFarmInventory(cows, chickens, pigs) {
  console.log(zeroPad(cows, 3) + " Cows");
  console.log(zeroPad(chickens, 3) + " Chickens");
  console.log(zeroPad(pigs, 3) + " Pigs");
}

printFarmInventory(7, 16, 3);
```
Một function với một tên đẹp và rõ ràng như zeroPad giúp người đọc dễ tìm ra và hiểu được chức năng của nó.
