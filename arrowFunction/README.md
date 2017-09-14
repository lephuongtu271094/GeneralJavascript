# Arrow function

### syntax
```javascript
   let functionName = (var1, var2) => {
       // Nội dung function
   };
```

### Nội dung là một câu lệnh đơn:

```javascript
    let hello = (name, message) => console.log("Chào " + name + ", bạn là " + message)

    hello(tu,laptrinhvien)
```

có thể bỏ đi cặp dấu {},
điều này tuân thủ theo nguyên tắc "nếu bên thân cặp {} chỉ là một câu lệnh thì bạn có thể bỏ cặp {}".

### Trường hợp một tham số:

```
    let hello = message => console.log(message);

    hello('My name is tu')
```

Trường hợp truyền vào chỉ một tham số thì có thể bỏ cặp ()

## Lỗi có thể gặp với Arrow function

### Đóng arrow function

Trường hợp sử dụng arrow function bên trong một hàm
hoặc sử dụng dạng một biến thì ban phải dùng cặp đóng mở để bao quanh lại

```javascript
    console.log(typeof () => {}); // Cú pháp sai
    console.log(typeof (() => {})); // Cú pháp đúng
```

Trong ví dụ trên thì ví dụ đầu tiên sai vì arrow function được sử dụng này như một tham số,
vì vậy bạn phải đặt nó bên trong cặp đóng mở

Trường hợp không muốn đặt nó bên trong cặp đóng mở thì ban phải khai báo arrow function thành một biến như ví dụ dưới đây.

```javascript
    let x = () => {}
    console.log(typeof x);
```

### Ràng buộc mũi tên

Đúng với cái tên của nó là hàm mũi tên và mũi tên này rất khó chịu về cú pháp sử dụng,
phải đặt mũi tên cùng hàng với tên hàm.

```javascript
    const func1 = (x, y) // Sai
    => {
        return x + y;
    };
    const func2 = (x, y) => // Đúng
    {
        return x + y;
    };
    const func3 = (x, y) => { // OK
        return x + y;
    };

    const func4 = (x, y) // Sai
    => x + y;
    const func5 = (x, y) => // Đúng
    x + y;
```

Nếu muốn xuống hàng mà không bị lỗi thì phải sử dụng cú pháp sau:

```javascript
    const func6 = (
        x,
        y
    ) => {
        return x + y;
    };
```


## Khắc phục nhược điểm với this trong closure function

Từ version ES5 trở về trước sẽ có nhược điểm với đối tượng this đó là phạm vi hoạt động, và trong ES5
có sử dụng hàm bind để khắc phục. Vấn đề này được khắc phục hoàn toàn trong ES6 bằng cách sử dụng hàm
arrow function.


##### ví dụ sử dụng trong ES5 trở về trước.

```
    var blog = {
        domain : "lephuongtu.com",
        showWebsite : function (callbackFunction){
            callbackFunction();
        },
        render : function(){
            this.showWebsite(function (){
               console.log(this.domain); // this chính là blog
            }.bind(this)); // phải sử dụng hàm bind thì đối tượng this mới chính là blog
        }
    };
```

##### Với ES6 thì viết như sau:

```
    var blog = {
        domain : "lephuongtu.com",
        showWebsite : function (callbackFunction){
            callbackFunction();
        },
        render : function(){
            this.showWebsite((() => {
               console.log(this.domain); // this chính là blog
            }));
        }
    };

    blog.render();
```



