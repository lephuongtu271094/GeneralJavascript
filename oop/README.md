Lập trình hướng đối tượng là một kỹ thuật lập trình cho phép lập trình viên tạo ra các đối tượng trong code trừu tượng
hóa các đối tượng thực tế trong cuộc sống. Hướng tiếp cận này hiện đang rất thành công và đã trở thành một trong những
khuôn mẫu phát triển phần mềm, đặc biệt là các phần mềm cho doanh nghiệp

Khi phát triển ứng dụng sử dụng OOP, chúng ta sẽ định nghĩa các lớp (class) để mô hình các đối tượng thực tế. Trong ứng
dụng các lớp này sẽ được khởi tạo thành các đối tượng và trong suốt thời gian ứng dụng chạy, các phương thức (method) của
 những đối tượng này sẽ được gọi.

 Lớp định nghĩa đối tượng sẽ gồm những phương thức(method) và thuộc tính (property) . Một đối tượng chỉ là một thể hiện của
 lớp. Các lớp tương tác với nhau bởi các public API: là tập các phương thức, thuộc tính public của các lớp.

## OOP có những nguyên lý cơ bản sau

### Tính đóng gói (Encapsulation)

Tính đóng gói là quy tắc yêu cầu trạng thái bên trong của một đối tượng được bảo vệ và tránh truy cập được từ các code bên ngoài
(tức là các code bên ngoài không thể trực tiếp nhìn thấy và thay đổi trạng thái của một đối tượng). Bất cứ truy cập nào tới trạng thái
bên trong này bắt buộc phải thông qua một public API để đảm bảo trạng thái của đối tượng luôn hợp lệ bởi vì các public API
đảm bảo tất cả các quy tắc kiểm tra tính hợp lệ cũng như trình tự thực hiện được áp dụng mỗi khi thay đổi trạng thái đó.

Vì trạng thái đối tượng không hợp lệ thường do: chưa được kiểm tra tính hợp lệ, các bước thực hiện không đúng trình tự hoặc bị bỏ qua nên trong


OOP có một quy tắc quan trọng cần nhớ đó là phải luôn khai báo các trạng thái bên trong của đối tượng là private và chỉ cho truy cập qua các public,
protected method/property. Khi sử dụng các đối tượng ta không cần biết bên trong nó làm việc như thế nào, ta chỉ cần biết các
public API là gì và điều này đảm bảo những gì thay đổi đối tượng sẽ được kiểm tra bởi các quy tắc logic bên trong, tránh đối
tượng bị sử dụng không chính xác.

### Tính kế thừa (Inheritance)

Khi bắt đầu xây dựng ứng dụng bởi các lớp, chúng ta thường thấy trường hợp một số lớp dường như có quan hệ với những lớp khác, chúng khá tương đồng.

Mỗi lớp đều đại diện cho một đối tượng khác nhau nhưng lại có những thuộc tính giống nhau. Thay vì sao chép những thuộc tính này, sẽ hay hơn nếu ta
đặt chúng ở một nơi có thể dùng bởi những lớp khác. Điều này được thực hiện bởi tính kế thừa trong OOP: chúng ta có thể định nghĩa lớp cha – base class
 và có những lớp con kế thừa từ nó (derived class), tạo ra một mối quan hệ cha/con

Nếu các chức năng của lớp cha đã được định nghĩa đầy đủ thì lập trình viên sẽ không phải làm bất cứ việc gì với lớp con. Còn nếu một lớp con muốn chức
 năng khác so với định nghĩa ở lớp cha thì nó có thể dễ dàng ghi đè (override)

### Tính đa hình (Polymorphism)

Tính Đa hình là khái niệm mà hai hoặc nhiều lớp có những phương thức giống nhau nhưng có thể thực thi theo những cách thức
khác nhau.

Nếu các lớp con không định nghĩa lại (overrides) phương thức CloudStore() thì phương thức CloudStore() trên lớp cha
sẽ được gọi. Còn nếu lớp con override lại phương thức CloudStore() của lớp cha thì phương thức CloudStore() trên
lớp con sẽ được gọi mặc dù code trong hàm đang thao tác với đối tượng

Tính Đa hình là một tính chất hết sức mạnh mẽ bởi vì nó mang lại cho code khả năng tổng quát hóa. không cần tạo ra phương thức cho mỗi kiểu kế
thừa từ lớp cha mà chỉ cần nhận một biến kiểu và có thể làm việc với bất cứ lớp nào kế thừa từ nó. Điều duy nhất không làm được ở đây là sử dụng những
phương thức mà chỉ được khai báo trên các lớp con.

VD: nếu ta có một phương thức trên lớp IPhone gọi là OpenSiri() nhưng không được khai báo trên lớp Smartphone, khi đó muốn gọi
nó sẽ bắt buộc phải ép kiểu từ Smartphone sang IPhone trước khi gọi.

### Interface

Đa hình dựa trên Kế thừa không phải bao giờ cũng là lựa chọn tốt nhất

Thay vì sử dụng Kế thừa ở đây, ta có thể sử dụng một kỹ thuật khác đó là Interface. Interface đơn giản là một giao kèo chỉ ra rằng code sẽ thực thi và
hỗ trợ một public API cụ thể nào đó. Tuy nhiên các public API này được thực hiện như thế nào thì không được chỉ ra trên Interface mà sẽ được chỉ ra trên lớp thực
thi interface này. Về cơ bản giao kèo là một danh sách các public method/property mà chắc chắn sẽ được thực thi trong lớp

