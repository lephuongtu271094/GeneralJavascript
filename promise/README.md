# Promise

promise sinh ra để xử lý kết quả của một hành động cụ thể,
kết quả của mỗi hành động sẽ là thành công hoặc thất bại và Promise sẽ giúp chúng ta giải quyết câu hỏi
"Nếu thành công thì làm gì? Nếu thất bại thì làm gì?". Cả hai câu hỏi này ta gọi là một hành động gọi lại (callback action).

### Khi một Promise được khởi tạo thì nó có một trong ba trạng thái sau :

    Fulfilled Hành động xử lý xong và thành công

    Rejected Hành động xử lý xong và thất bại

    Pending Hành động đang chờ xử lý hoặc bị từ chối

Trong đó hai trạng thái Rejected và Fulfilled ta gọi là Settled, tức là đã xử lý xong.

Pending : là trạng thái khi bạn khởi tạo một Promise nhưng chưa thiết lập kết quả cho nó, tức là chưa sử dụng resolve và reject.

Rejected :  là trạng thái thao tác thất bại, trạng thái này xảy ra khi bạn sử dụng reject. Khi bạn sử dụng reject thì bắt buộc phải khai báo hành động
xử lý cho nó (tức sử dụng then hoặc catch).

Fulfilled : còn được gọi là resolved, đây là trạng thái của Promise đã thành công, trạng thái này xảy ra khi bạn sử dụng resolve.


### Syntax :

```javascript

    let promise = new Promise(function(resolve, reject){

    });

```
##### Trong đó:

    resolve là một hàm callback xử lý cho hành động thành công.

    reject là một hàm callback xử lý cho hành động thất bại.


## Thenable ( .then() ) trong Promise :

Thenable là một phương thức ghi nhận kết quả của trạng thái (thành công hoặc thất bại)
mà ta khai báo ở Reject và Resolve. Nó có hai tham số truyền vào là 2 callback function.
Tham số thứ nhất xử lý cho Resolve và tham số thứ 2 xử lý cho Reject

```javascript
    let promise = new Promise(function(resolve, reject){
        resolve('Success');
        // OR
        reject('Error');
    });


    promise.then(
            function(success){
                // Success
            },
            function(error){
                // Error
            }
    );
```

 Hai hàm callback trong .then() chỉ xảy ra một trong hai mà thôi, điều này tương ứng ở Promise sẽ khai báo một là Resolve
 và hai là Reject, nếu khai báo cả hai thì nó chỉ có tác dụng với khai báo đầu tiên.

#### Thenable liên tiếp :

Phương thức then() có nhiệm vụ tiếp nhận kết quả trả về của promise và nó cũng return về một promise
nên bạn có thể dùng nhiều lần liên tiếp với nhau.

```javascript
    var promise = new Promise(function(resolve, reject){
        resolve();
    });

    promise.then(function(){
                console.log(1);
            })
            .then(function(){
                console.log(2);
            })
            .then(function(){
                console.log(3);
            });

     // kêt quả :
     // 1
     // 2
     // 3
```

Khi sử dụng thenable liên tiếp thì kết quả return của phương thức then() hiện tại sẽ quyết định trạng thái
của phương thức  then() tiếp theo. Ví dụ then() phía trên return về một Promise Rejected thì then() phía
dưới sẽ nhận một trang thái Rejected.

```javascript
    var promise = new Promise(function(resolve, reject){
        resolve();
    });

    promise
        .then(function(){
            return new Promise(function(resolve, reject){
                reject();
            });
        })
        .then(function(){
            console.log('Success!');
        })
        .catch(function(){
            console.log('Error!');
        });

    // kết quả
    // Error
```

Vì then() thứ nhất return về một Reject Promise nên then() thứ hai không chạy, và trạng thái bây giờ là Rejected nên catch sẽ
được chạy => in ra chữ Error!.

## Catch ( .catch() ) trong Promise :
.then() có hai tham số callbacks đó là success và error. Tuy nhiên bạn cũng có thể sử dụng phương thức catch để bắt lỗi.

```javascript
    promise.then().catch()
```

Nếu ta vừa truyền callback error và vừa sử dụng catch thì nó sẽ chạy hàm callback error và catch sẽ không chạy.
