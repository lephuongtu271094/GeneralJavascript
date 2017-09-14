#  async await

 Promise nhằm giải quyết tình trạng callback hell. Với Promise, mã nguồn sẽ
 trông gần giống với phong cách đồng bộ, kết quả là trông dễ theo dõi và bảo trì hơn. Tuy nhiên sử dụng
 Promise lại làm phát sinh vấn đề "khá" tương tự là Promise hell

 ```javascript
     function wait(ms) {
        return new Promise(r => setTimeout(r, ms))
     }

     function main() {
        console.log('sắp rồi...')
        wait(2007).then(() => {
          console.log('chờ tí...')
          return wait(2007)
        }).then(() => {
          console.log('thêm chút nữa thôi...')
          return wait(2012)
        }).then(() => {
           console.log('thêm chút nữa thôi...')
          return wait(2016)
        }).then(() => {
          console.log('xong rồi đấy!')
        })
     }
 ```


 Để giải quyết vấn đề đó, ở phiên bản ES7 (ES 2017), 1 khái niệm với 2 từ khóa mới được đưa vào là hàm
 async (async / await). Hàm async cho phép ta viết các thao tác bất đồng bộ với phong cách của các mã
 đồng bộ. Bằng cách viết như vậy, mã nguồn của ta trông sẽ sáng sủa, dễ đọc hơn và "dễ hiểu hơn".


 ```javascript
    function wait(ms) {
       return new Promise(r => setTimeout(r, ms))
    }

    async function main() {
           console.log('sắp rồi...')
       await wait(2007)
           console.log('chờ tí...')
       await wait(2012)
           console.log('thêm chút nữa thôi...')
       await wait(2016)
           console.log('xong rồi đấy!')
    }
 ```

## Cách sử dụng

Để sử dụng hàm async, ta cần khai báo từ khóa async ngay trước từ khóa định nghĩa hàm tức là :

- Hàm định nghĩa với từ khóa function ta phải khai báo ngay trước function,

- Với arrow function ta phải khai báo trước tập tham số đầu vào,

- Với phương thức của Class thì ta phải khai báo ngay trước tên hàm.

```javascript
    // regular function
    async function functionName() {
       let ret = await new Google().search('JavaScript')
    }

    // arrow function
    let arr = ['JS', 'node.js'].map(async val => {
       return await new Google().search(val)
    })

    // Class
    class Google {
       constructor() {
         this.apiKey = '...'
       }

       async search(keyword) {
         return await this.searchApi(keyword)
       }
    }
```

Với từ khóa async này, ta có thể đợi các Promise xử
lý trong hàm đó mà không tạm dừng luồng chính bằng từ khóa await như ví dụ trên.

Kết quả trả ra của hàm async luôn là một Promise dù bạn có gọi await - có xử lý bất đồng bộ hay không.
Promise này sẽ ở trạng thái thành công với kết quả được trả ra với từ khóa return của hàm async,
hoặc trạng thái thất bại với kết quả được đẩy qua từ khóa throw trong hàm async.

Như vậy, bản chất của hàm async chính là Promise.

Với Promise, ta có thể xử lý lỗi với catch khá đơn giản. Tuy nhiên cũng không dễ dàng theo dõi và dễ
đọc. Nhưng với hàm async, việc này cực kì đơn giản bằng từ khóa try catch hệt như các thao tác đồng bộ.

```javascript
    function wait(ms) {
       return new Promise(r => setTimeout(r, ms))
    }

    async function runner() {
       console.log('sắp rồi...')
       await wait(2007)
       console.log('chờ tí...')
       await wait(2012)
       console.log('thêm chút nữa thôi...')
       await wait(2016)
       throw new Error(2016)
    }

    async function main() {
       try {
         await runner()
         console.log('xong rồi đấy!')
       } catch (e) {
         console.log(`có vấn đề tại ${ e }`)
       }
    }
```

Rõ ràng là mã nguồn sử dụng async/await trông đơn giản, dễ theo dõi,
"dễ hiểu" hơn và giải quyết được tình trạng callback - promise hell.

## Các lỗi có thể gặp

### Quên khai báo từ khóa async

Ví dụ như với trường hợp khai báo một hàm trong một hàm async. Hàm khai báo trong hàm async cũng bắt
buộc phải được khai báo với từ khóa async nếu như bạn muốn sử dụng như một hàm async.

```javascript
    async function main() {
       await wait(1000)
       let arr = [100, 300, 500].map(val => wait(val))
       arr.forEach(func => await func)
       // ??? error
    }
```

### Nhập nhằng từ khóa await

#### Có 2 tình huống điển hình cho trường hợp này là:

##### - Quên khai báo khi cần đợi một xử lý bất đồng bộ

Nếu không khai báo từ khóa này thì kết quả nhận được sẽ là một
Promise chứ không phải là kết quả thực thi của xử lý bất đồng bộ.

```javascript
     async function now() {
         return Date.now()
      }

      async function main() {
         let t = now()
         console.log(t)
          // ??? `t` is a `Promise` instance
      }
```

##### - Khai báo "thừa" trước một xử lý đồng bộ

Có 2 vấn đề là không biết cái nào là đồng bộ, cái nào là bất đồng bộ nữa, và hiệu quả đi xuống.
Mỗi khi khai báo await thì mặc nhiên sau từ khóa đó là một Promise,
nếu không phải là một Promise thì nó sẽ được gói lại vào Promise và được trả ra ngay
với phương thức Promise.resolve(value).

Ví dụ : muốn lấy 1 + 0 = 1 mà phải đi đường vòng là tính tổng,
rồi nhét vào Promise, rồi lại moi ra để sử dụng.

```javascript
     async function main() {
          // run with await
          console.log('run with await')
          let i = 1000000
          console.time('await')
          while(i-- > 0) {
            let t = await (1 + 0)
          }
          console.timeEnd('await')

          // run without await
          console.log('run without await')
          i = 1000000
          console.time('normal')
          while(i-- > 0) {
            let t = 1 + 0
          }
          console.timeEnd('normal')
       }
```

### Quên xử lý lỗi

Cũng như với việc quên catch lỗi khi sử dụng Promise, việc quên try catch để bắt lỗi với hàm async
cũng có thể xảy ra. Nếu quên không bắt lỗi, thì khi đoạn mã bất đồng xảy ra lỗi có thể làm
chương trình bị dừng lại.

```javascript
    function wait(ms) {
       if (ms > 2015) throw new Error(ms)
       return new Promise(r => setTimeout(r, ms))
    }

    async function main() {
       console.log('sắp rồi...')
       await wait(2007)
       console.log('chờ tí...')
       await wait(2012)
       console.log('thêm chút nữa thôi...')
       await wait(2016)
       console.log('xong rồi đấy!')
    }
```

### Mất tính song song

Nếu cứ khai báo await tuần tự thì chương trình sẽ bị chậm .
Vì mỗi lần khai báo await như vậy là cần phải chờ cho xử lý của await kết thúc. Kết
quả là có 1 ứng dụng chạy tuần tự qua hàm

```javascript
    function wait(ms) {
       return new Promise(r => setTimeout(r, ms))
    }

    async function main() {
       console.time('wait3s')
       await wait(1000)
       await wait(2000)
       console.timeEnd('wait3s')
    }
```

Với đoạn mã trên sẽ mất tổng cộng là 1 + 2 = 3s để thực thi

Để tránh tình trạng trên thì cho xử lý bất đồng bộ chạy trước rồi lấy kết quả sau
Vì Promise có thể cho phép lấy kết quả bất cứ khi nào mà nó ở trạng thái cuối cùng, nên có thể chạy nó trước rồi lấy sau.

```javascript
    function wait(ms) {
       return new Promise(r => setTimeout(r, ms))
    }

    async function main() {
       console.time('wait2s')
       let w1 = wait(1000)
       let w2 = wait(2000)
       await w1
       await w2
       console.timeEnd('wait2s')
    }
```

Chỉ mất 2s để thực hiện vì đoạn wait được thực thi song song. Ngoài cách await từng Promise như
trên, có thể sử dụng Promise.all để song song hóa các Promise.

```
    function wait(ms) {
       return new Promise(r => setTimeout(r, ms))
    }

    async function main() {
       console.time('wait2s')
       await Promise.all([wait(1000), wait(2000)])
       console.timeEnd('wait2s')
    }
```

Promise.all chỉ ở trạng thái thành công khi mà tất cả các Promise được truyền vào xử lý thành công,
còn nó sẽ ở trạng thái lỗi khi một trong các Promise truyền vào bị lỗi. Như vậy, nếu muốn bỏ qua các
Promise lỗi thì không thể sử dụng Promise.all. Lúc đó bắt buộc phải sử dụng await kèm
với try catch cho từng Promise.

bản Node.js v7.6 đã hỗ trợ async-await mặc định.
Nếu muốn chạy ở các nền tảng/ trình duyệt chưa hỗ trợ thì có thể dùng babel để chuyển đổi

## Kết luận

Bản chất của hàm async chính là Promise, vì vậy để sử dụng được nó cần phải sử dụng Promise cho việc xử lý các
thao tác bất đồng bộ. không thể nào sài await để đợi các hàm có sử dụng hàm callback được, mà bắt buộc phải gắn
nó với một Promise trước khi sử dụng await.


Mặc dù hàm async có cú pháp rất rõ ràng, nhưng cũng cần phải lưu ý tránh khai báo thừa thiếu các từ khóa gây lỗi, gây hiểu
lầm về lô-gíc chương trình. Và đặc biệt lưu ý tới khả năng làm mất đi tính song song của chương trình.


