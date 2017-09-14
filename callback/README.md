# Callback


Callback là một đoạn code được truyền như một tham số của một hàm(function)
và chờ để được gọi vào thực thi. Javascript là một ngôn ngữ lập trình hướng sự kiện
và bất đồng bộ nên callback function đóng vai trò rất quan trọng, bạn sẽ truyền một
callback function vào các sự kiện và xử lý bất đồng bộ đó.

Callback chỉ là một hàm của javascript tuy nhiên khác với các hàm thông
thường khác hàm callback không được gọi một cách trực tiếp mà chỉ khi có một sự kiện nào
đó diễn ra thì chúng mới được thực thi.

### Callback phải là một function
Callback là một function nên bạn nhất định phải truyền vào là một function,
nếu bạn truyền một type khác thì bạn sẽ nhận được error notice:
"Callback is function" trong console.

## Callback hell

là mô tả các trường hợp mà có nhiều tác vụ bất đồng bộ được gọi liên tiếp nhau trong đó tác vụ sau
là kết quả của tác vụ trước trong trường hợp đó thì đoạn code nhìn sẽ phức tạp hơn rất nhiều
và gây khó khăn trong quá trình đọc hiểu và bảo trì code