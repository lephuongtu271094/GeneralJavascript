# ASYNC & SYNC

## Synchronous - SYNC

Synchronous viêt tắt là sync có nghĩa là xử lý đồng bộ, chương trình sẽ chạy theo từng bước và chỉ khi nào bước 1 thực hiện xong thì mới nhảy sang bước 2,
khi nào chương trình này chạy xong mới nhảy qua chương trình khác. Đây là nguyên tắc cơ bản trong lập trình mà bạn đã được học đó là khi biên
dịch các đoạn mã thì trình biên dịch sẽ biên dịch theo thứ tự từ trên xuống dưới, từ trái qua phải và chỉ khi nào biên dịch xong dòng thứ nhât
mới nhảy sang dòng thứ hai, điều này sẽ sinh ra một trạng thái ta hay gọi là trạng thái chờ. Ví dụ trong quy trình sản xuất dây chuyền công
nghiệp được coi là một hệ thống xử lý đồng bộ.

## Asynchronous - ASYNC

Ngược lại với Synchronous thì Asynchronous là xử lý bất động bộ, nghĩa là chương trình có thể nhảy qua bỏ đi một bước nào đó, vì vậy Asynchronous
được ví như một chương trình hoạt động không chặt chẽ và không có quy trình nên việc quản lý rất khó khăn. Nếu một hàm A phải bắt buộc chạy trước
hàm B thì với Asynchronous sẽ không thể đảm bảo nguyên tắc này luôn đúng.

## Mặt tốt của ASYNC & SYNC

#### Synchronous - SYNC

Chương trình sẽ chạy theo đúng thứ tự và có nguyên tắc nên sẽ không mắc phải các lỗi về tiến trình không cần thiết. Không chỉ trong
lập trình mà trong thực tế cũng vậy, một công ty đưa ra quy trình đồng bộ sẽ đảm bảo được chất lượng của sản phẩm,
nếu bị lỗi thì sẽ biết ngay là lỗi tại quy trình nào và từ đó sẽ dễ dàng khắc phục.

#### Asynchronous - ASYNC

Có thể xử lý nhiều công việc một lúc mà không cần phải chờ đợi Ví dụ bạn đi ký một
văn bản ở Xã, Phường thì nếu bạn có tiền bạn sẽ bỏ qua được một vài công đoạn

## Mặt xấu của ASYNC & SYNC

#### Synchronous - SYNC

Chương trình chạy theo thứ tự đồng bộ nên sẽ sinh ra trạng thái chờ và là không cần thiết trong một số trường hợp,
lúc này bộ nhớ sẽ dễ bị tràn vì phải lưu trữ các trạng thái chờ đó.

#### Asynchronous - ASYNC

Nếu một chuong trình đòi hỏi phải có quy trình thì bạn không thể sử dụng Asynchronous được, điển hình là trong quy trình sản
xuât một sản phẩm của các nhà máy công nghiệp không thể áp dụng kỹ thuật làm nhiều công việc một lúc thế này được. Còn về
chương trình trong lập trình thì sao? Một thao tác thêm dữ liệu phải thông qua hai công đoạn là validate dữ liệu và thêm dữ
liệu, nếu thao tác validate xảy ra sau thao tác thêm thì còn gì tệ hại hơn nữa.

## AJAX

Ajax là một kỹ thuật viết tắt của chữ Asynchronous JavaScript and XML

Đây là một công nghệ giúp chung ta tạo ra những Web động mà hoàn toàn không reload lại trang nên rất mượt và đẹp. Đối với công nghệ web
hiện nay thì ajax không thể thiếu, nó là một phần làm nên sự sinh động cho website.

Ajax được viết bằng ngôn ngữ Javascript nó chạy trên client, tức là mỗi máy (user) sẽ chạy độc lập không hoàn toàn ảnh hưởng lẫn nhau.

## setTimeout

Bản chất setTimeout là một Async, nghĩa là các đoạn code bên dưới sẽ hoạt động trước nội dung bên trong hàm setTimeout()

```javascript
    setTimeout(function(){
        console.log('hello')
    }, 0);

    console.log('xin chào')

    // kết quả :

    // xin chào
    // hello
```




