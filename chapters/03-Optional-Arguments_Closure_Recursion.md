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

It is perfectly okay for a function to call itself, as long as it takes care not to overflow the stack. A function that calls itself is called recursive. Recursion allows some functions to be written in a different style. Take, for example, this alternative implementation of power:
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
This is rather close to the way mathematicians define exponentiation and arguably describes the concept in a more elegant way than the looping variant does. The function calls itself multiple times with different arguments to achieve the repeated multiplication.

But this implementation has one important problem: in typical JavaScript implementations, it’s about 10 times slower than the looping version. Running through a simple loop is a lot cheaper than calling a function multiple times.

The dilemma of speed versus elegance is an interesting one. You can see it as a kind of continuum between human-friendliness and machine-friendliness. Almost any program can be made faster by making it bigger and more convoluted. The programmer must decide on an appropriate balance.

In the case of the earlier power function, the inelegant (looping) version is still fairly simple and easy to read. It doesn’t make much sense to replace it with the recursive version. Often, though, a program deals with such complex concepts that giving up some efficiency in order to make the program more straightforward becomes an attractive choice.

The basic rule, which has been repeated by many programmers and with which I wholeheartedly agree, is to not worry about efficiency until you know for sure that the program is too slow. If it is, find out which parts are taking up the most time, and start exchanging elegance for efficiency in those parts.

Of course, this rule doesn’t mean one should start ignoring performance altogether. In many cases, like the power function, not much simplicity is gained from the “elegant” approach. And sometimes an experienced programmer can see right away that a simple approach is never going to be fast enough.

The reason I’m stressing this is that surprisingly many beginning programmers focus fanatically on efficiency, even in the smallest details. The result is bigger, more complicated, and often less correct programs, that take longer to write than their more straightforward equivalents and that usually run only marginally faster.

But recursion is not always just a less-efficient alternative to looping. Some problems are much easier to solve with recursion than with loops. Most often these are problems that require exploring or processing several “branches”, each of which might branch out again into more branches.

Consider this puzzle: by starting from the number 1 and repeatedly either adding 5 or multiplying by 3, an infinite amount of new numbers can be produced. How would you write a function that, given a number, tries to find a sequence of such additions and multiplications that produce that number? For example, the number 13 could be reached by first multiplying by 3 and then adding 5 twice, whereas the number 15 cannot be reached at all.

Here is a recursive solution:
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
Note that this program doesn’t necessarily find the shortest sequence of operations. It is satisfied when it finds any sequence at all.

I don’t necessarily expect you to see how it works right away. But let’s work through it, since it makes for a great exercise in recursive thinking.

The inner function find does the actual recursing. It takes two arguments—the current number and a string that records how we reached this number—and returns either a string that shows how to get to the target or null.

To do this, the function performs one of three actions. If the current number is the target number, the current history is a way to reach that target, so it is simply returned. If the current number is greater than the target, there’s no sense in further exploring this history since both adding and multiplying will only make the number bigger. And finally, if we’re still below the target, the function tries both possible paths that start from the current number, by calling itself twice, once for each of the allowed next steps. If the first call returns something that is not null, it is returned. Otherwise, the second call is returned—regardless of whether it produces a string or null.

To better understand how this function produces the effect we’re looking for, let’s look at all the calls to find that are made when searching for a solution for the number 13.
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
The indentation suggests the depth of the call stack. The first time find is called it calls itself twice to explore the solutions that start with (1 + 5) and (1 * 3). The first call tries to find a solution that starts with (1 + 5) and, using recursion, explores every solution that yields a number less than or equal to the target number. Since it doesn’t find a solution that hits the target, it returns null back to the first call. There the || operator causes the call that explores (1 * 3) to happen. This search has more luck because its first recursive call, through yet another recursive call, hits upon the target number, 13. This innermost recursive call returns a string, and each of the || operators in the intermediate calls pass that string along, ultimately returning our solution.
