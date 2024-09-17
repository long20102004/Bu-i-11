## Buổi 11: Nhập môn: các nguyên tắc thiết kế phần mềm và lập trình giao diện

- SOLID là gì? (3 phần đầu)
- KISS, DRY, YAGNI
- Mô hình MVC 
- Các thành phần chính trong lập trình giao diện: 
   - Window
   - View
   - ViewGroup
   - Layout
   - Event Handling
   - Widgets

----


# 1. SOLID là gì? (3 phần đầu)

SOLID là một nguyên lý thiết kế phần mềm, bao gồm 5 nguyên lý cơ bản:
    - Single Responsibility Principle: Quy tắc trách nhiệm đơn lẻ
    - Open/Closed Principle: Quy tắc mở đóng
    - Liskov Substitution Principle: Quy tắc thay thế Liskov
    - Interface Segregation Principle: Quy tắc phân chia giao diện
    - Dependency Inversion Principle: Quy tắc đảo ngược phụ thuộc

Tại bài này, ta chỉ tập trung vào 3 nguyên lý đầu tiên để phù hợp với đối tượng người đọc.

![alt text](image.png)

## Lí do nên áp dụng các nguyên tắc SOLID

- **Clean**: Nguyên tắc SOLID giúp code clean, dễ nhìn hơn và chuẩn hoá format của code để nhiều người hiểu hơn.
- **Dễ bảo trì**: Code dễ bảo trì, sửa lỗi hơn.
- **Tính co giãn**: Dễ dàng refactor, tái cấu trúc lại code. Dễ dàng phát triển các tính năng mới sau này.
- **Tối ưu**: Giảm bớt các code dư thừa.
- **Kiểm nghiệm**: Viết unit test dễ hơn.
- **Dễ đọc**: Giúp code đọc dễ hiểu hơn.
- **Độc lập**: Code hoạt động độc lập, ít phụ thuộc các phần khác, giảm thiểu lỗi.
- **Tái sử dụng**: Code được chia nhỏ và độc lập như các module, dễ dàng sử dụng lại.

## 1.1. Single Responsibility Principle: Quy tắc trách nhiệm đơn lẻ

![alt text](image-1.png)

## Quy tắc trách nhiệm đơn lẻ (SRP)

**Quy tắc trách nhiệm đơn lẻ (SRP)** khẳng định rằng một lớp chỉ nên có một lý do để thay đổi. Nói cách khác, một lớp chỉ nên có một trách nhiệm hoặc công việc duy nhất. Nguyên tắc này giúp giữ cho các lớp tập trung và dễ bảo trì.

- Theo nguyên lí này, mỗi class chỉ nên có một vai trò duy nhất. Tức là bạn có thể để 1 class có rất nhiều chức năng, làm đủ thứ, với nhiều method khác nhau. Tuy nhiên việc nhét toàn bộ chức năng vào 1 class khiến code khó bảo trì, khó hiểu hơn, và xử lí một phần nhỏ của cả một class chứa rất nhiều chức năng này có thể làm lỗi toàn bộ các chức năng khác.

Hãy thử xem một class sau:

![alt text](image-2.png)

- Việc cho toàn bộ các phương thức gộp vào 1 class NguoiChoi như này đã vi phạm quy tắc, thực hiện rất nhiều thay đổi chỉ trong 1 class như lấy dữ liệu từ database, chuyển sang json để trả về, di chuyển nhân vật, …. `Sau này khi nâng cấp thêm chức năng, class này ngày càng phình to ra.` Khiến cho việc bảo trì, nâng cấp, test, …. trở lên khó khăn hơn sau này.

`Thay vì vậy, ta có thể chuyển thành như sau`

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

- Lúc này mỗi class sẽ độc lập hơn và các luồng hoạt động cũng sẽ rõ ràng hơn, khi có lỗi xảy ra hay cần nâng cấp chức năng, bạn có thể dễ dàng sửa đổi vào các class trong 1 luồng chứ không phải thay đổi hay thêm mọi thứ vào 1 class và khiến chúng phình to hơn nữa.
`Tuy số lượng class nhiều hơn những việc sửa chữa sẽ đơn giản hơn, dễ dàng tái sử dụng hơn, class ngắn hơn nên cũng ít bug hơn.`
Một số ví dụ về nguyên tắc SRP cần xem xét có thể cần được tách riêng bao gồm: `Persistence, Validation, Notification, Error Handling, Logging, Class Instantiation, Formatting, Parsing, Mapping, …`


## 1.2. Open/Closed Principle: Quy tắc mở đóng

![alt text](image-7.png)

Nguyên tắc này được phát biểu như sau:

- Có thể thoải mái mở rộng 1 class, nhưng không được sửa đổi bên trong class đó.
`"Objects or entities should be open for extension, but closed for modification."`

- Điều này có nghĩa là một class nên mở rộng được, nhưng không nên sửa đổi bên trong class đó. Điều này giúp cho việc mở rộng chức năng, thêm tính năng mới, mở rộng class, module, … mà không cần phải sửa đổi code cũ, giúp cho việc bảo trì, nâng cấp, test, … dễ dàng hơn.

- Theo nguyên tắc này, sau khi thiết kế một class với một số chức năng nhất định, cần đảm bảo các chức năng này hoạt động trơn tru trong tương lai, tránh sửa đổi thêm sau này. Như vậy, class luôn “đóng – closed” cho các sửa đổi vào các chức năng đã được thiết kế trước, nhưng lại phải “mở – open” để mở rộng tính năng hơn, để mở thì có 1 số cách phổ biến như:

    - Sử dụng kế thừa
    - Sử dụng interface
    - Sử dụng một số design pattern như Strategy, Decorator, …

Ví dụ:

![alt text](image-8.png)

- Với cách thiết kế như trên, khi ta có các class con kế thừa từ class cha NguoiChoi, và cần kiểm tra xem class con có hệ là gì, hay ví dụ ta cần tạo thêm nhiều class con khác tương tự, `ta lại phải thêm nhiều if else vào class gốc`. 


- `Thay vào đó, ta có thể thiết kế như sau:`

![alt text](image-9.png)

- Lúc này, khi cần nâng cấp thêm nhiều hệ mới cho hệ thống, ta chỉ cần tạo các class con và sử dụng chức năng của class chính, không cần thực hiện trực tiếp vào class chính nữa.

- `Lợi ích` của nguyên lý này là đôi khi chúng ta cần sử dụng các class từ các nguồn thư viện thứ 3, hoặc từ chính các thư viện có sẵn trong Java. `Chúng ta có thể dễ dàng extend và tạo các class con mới kế thừa từ class cha để phục vụ cho một mục đích, chức năng mới của dự án, mà không cần quá lo lắng về class cha sẽ bị lỗi do ta đã không sửa đổi chúng.` -> Chỉ kế thừa và thay đổi những phần cần thiết.

## 1.3. Liskov Substitution Principle: Quy tắc thay thế Liskov

![alt text](image-10.png)

- Barbara Liskov đã đưa ra nguyên tắc `Liskov Substitution Principle (LSP)` này. Nguyên tắc này cho rằng: trong kế thừa, các class con, `class kế thừa phải luôn có thể thay thế được class cha.` Tức là, nếu `class A kế thừa từ class B, thì mình luôn có thể sử dụng class A thay cho class B mà các chức năng không bị thay đổi.`

Lấy ví dụ về hình vuông và hình chữ nhật

![alt text](image-11.png)
![alt text](image-12.png)


- Như trong toán học được dạy ở các cấp dưới, ta hay được nghe là `“hình vuông cũng là hình chữ nhật”`, `Nhìn ví dụ` trên ta thấy mọi tính toán đều rất hợp lý. Do hình vuông có 2 cạnh bằng nhau, mỗi khi set độ dài 1 cạnh thì ta set luôn độ dài của cạnh còn lại bằng cách viết đè phương thức set chiều cao và set chiều rộng.

- Tuy nhiên, class HinhVuong sau khi kế thừa class HinhChuNhat đã `làm thay đổi các đặc tính vốn có của HinhChuNhat`, dẫn đến `vi phạm LSP`. 

### Những vi phạm về nguyên lý LSP

- Các lớp dẫn xuất có các phương thức ghi đè phương thức của lớp cha nhưng với chức năng hoàn toàn khác.
- Các lớp dẫn xuất có phương thức ghi đè phương thức của lớp cha là một phương thức rỗng.
- Các phương thức bắt buộc kế thừa từ lớp cha ở lớp dẫn xuất nhưng không được sử dụng.
- Phát sinh ngoại lệ trong phương thức của lớp dẫn xuất.

![alt text](image-13.png)

- Câu chuyện về con vịt nhựa: Nếu bạn có một con vịt nhựa, nó là 1 con `vịt`, có thể kêu như vịt, nhưng mà lại cần pin, thì nó không thể thay thế cho con vịt thật được.

- Đây là nguyên lý… `dễ bị vi phạm nhất`, nguyên nhân chủ yếu là do sự thiếu kinh nghiệm khi thiết kế class. Thông thường, design các class dựa theo đời thật: hình vuông là hình chữ nhật, file nào cũng là file. Tuy nhiên, không thể bê nguyên văn mối quan hệ này vào code. Hãy nhớ 1 điều:

- Nguyên lý này ẩn giấu trong hầu hết mọi đoạn code, giúp cho code linh hoạt và ổn định mà ta không hề hay biết. Ví dụ như trong Java, `ta có thể chạy hàm foreach với List, ArrayList, LinkedList bởi vì chúng cùng kế thừa interface Iterable`. Các class List, ArrayList, … đã được thiết kế đúng LSP, chúng có thể thay thế cho Iterable mà không làm hỏng tính đúng đắn của chương trình.

### Sửa vấn đề hình vuông - hình chữ nhật

- Theo đó, để sửa vấn đề hình vuông – hình chữ nhật trên, ta `có thể` để chúng cùng kế thừa một class Shape như sau

![alt text](image-14.png)


Lúc này việc set các chiều cao và chiều rộng thì chỉ class con mới có, và không vi phạm nguyên tắc LSP.

`Việc thiết kế áp dụng theo nguyên tắc LSP giúp chúng ta giảm bớt quá lạm dụng việc kế thừa trong class. Ý nghĩa của các chức năng không được thay đổi để có thể sử dụng ở nhiều phạm vi khác nhau hơn.`

- Ngoài ra có thể sử dụng Design Pattern như Builder, Factory, ... để giải quyết vấn đề này.

# 2. KISS, DRY, YAGNI

## 2.1. KISS

![alt text](image-15.png)
- `KISS` là viết tắt của `Keep It Simple, Stupid`. Nguyên tắc này khuyến khích việc thiết kế và viết code đơn giản, dễ hiểu, dễ bảo trì. `KISS` không có nghĩa là viết code ngắn gọn, mà là viết code dễ hiểu, dễ bảo trì, dễ mở rộng.

- Đôi lúc, ta nghĩ quá phức tạp vấn đề, ví dụ dự án nhỏ, nhưng ta lại áp dụng một số công nghệ quá phức tạp, như dùng những thư viện lớn cho chức năng nhỏ, làm dự án nặng hơn. Dùng thuật toán quá cao cho những vấn đề nhỏ, dần dà code trở nên phức tạp, khó bảo trì, khó mở rộng.

## 2.2. DRY

![alt text](image-16.png)

- `DRY` là viết tắt của `Don’t Repeat Yourself`. Nguyên tắc này khuyến khích việc viết code không lặp lại, không viết lại những chức năng đã có sẵn. `DRY` giúp giảm thiểu lỗi, giảm thiểu thời gian viết code, giảm thiểu thời gian bảo trì.

- Khi viết code, nếu có một chức năng nào đó mà ta cần sử dụng nhiều lần, ta nên viết thành một hàm, một class, một module

## 2.3. YAGNI

![alt text](image-17.png)

- `YAGNI` là viết tắt của `You Ain’t Gonna Need It`. Nguyên tắc này khuyến khích việc viết code dựa trên những yêu cầu thực tế, không viết những chức năng không cần thiết, không viết những chức năng dựa trên giả định.

- Dự án chỉ cho một trường học sử dụng bởi khoảng 100 cán bộ nhân viên. Ta có cần làm nó có cân bằng tải, có hệ thống database phân tán xịn MongoDB, có hệ thống cache Redis, có hệ thống tìm kiếm Elasticsearch, có hệ thống gửi mail, có hệ thống chat, … không? `YAGNI` khuyến khích việc viết code dựa trên những yêu cầu thực tế, không viết những chức năng không cần thiết, không viết những chức năng dựa trên giả định.


# 3. Mô hình MVC

![alt text](image-18.png)

- `MVC` là viết tắt của `Model – View – Controller`. Đây là một mô hình thiết kế phần mềm, mô hình này chia ứng dụng thành 3 phần chính: `Model`, `View`, `Controller`.

    - `Model`: Là phần dữ liệu, nơi chứa dữ liệu, nơi thực hiện các thao tác với dữ liệu.
    - `View`: Là phần hiển thị, nơi hiển thị dữ liệu, nơi tương tác với người dùng.
    - `Controller`: Là phần điều khiển, nơi điều khiển dữ liệu, nơi điều khiển hiển thị.

- Mô hình `MVC` giúp cho việc phân chia ứng dụng trở nên rõ ràng, dễ bảo trì, dễ mở rộng. Mỗi phần có một nhiệm vụ riêng, không phụ thuộc vào nhau.

- Ví dụ mô hình MVC

![alt text](image-19.png)

- Giả sử bạn đi vào 1 nhà hàng. Bạn sẽ không vào thẳng nhà bếp và tương tác với đồ ăn, thay vì đó, bạn sẽ xem các món ăn qua `thực đơn menu` - `View`
- Sau khi bạn chọn món ăn, `nhân viên` sẽ lấy thực đơn và đưa vào bếp - `Controller`
- Ở bếp, `đầu bếp` sẽ thực hiện các công việc như nấu ăn, chế biến thức ăn - `Model`. Trong bếp ta cần chứa các thông tin như số đồ ăn còn lại, số đồ ăn đã bán, số đồ ăn đã chế biến, … - `Model`.

- Ta không biết ứng dụng bên dưới được lưu như thế nào ở tầng Model, ở View, ta chỉ xem những gì hiển thị ra màn hình, và tương tác với nó.
- Model, các đồ ăn ở bếp có thể đang cất tủ đá, có thể được nhớ bằng giấy note, có thể được lưu trong máy tính, … Controller sẽ quyết định cách thức lấy dữ liệu từ Model và hiển thị ra View.

Ta có thể thấy rằng, mỗi phần có một nhiệm vụ riêng, không phụ thuộc vào nhau, giúp cho việc phân chia ứng dụng trở nên rõ ràng, dễ bảo trì, dễ mở rộng.


Ví dụ: Một chiếc xe

![alt text](image-20.png)

- Ta tương tác với `View` là vô lăng, cần số, cần ga, cần phanh, …
- Vô lăng, cần số, ... sẽ yêu cầu `Controller` là động cơ, các cấu phần bên trong xe, … phải đốt nhiên liệu đi, phải chuyển động, phải phanh, …
- Động cơ, các cấu phần bên trong xe lúc này sẽ yêu cầu các tài nguyên từ `Model` như xăng, dầu, .. để thực hiện các công việc.
# 4. Các thành phần chính trong lập trình giao diện
## 4.1. Window
- Window là cửa sổ chính của ứng dụng, nơi chứa tất cả các thành phần giao diện khác. Mỗi ứng dụng thường có ít nhất 1 Window.
- Window chứa các View và ViewGroup bên trong nó, đồng thời xử lý các sự kiện từ hệ điều hành và người dùng.

![alt text](image-21.png)
## 4.2. View
- View là các thành phần hiển thị giao diện trên màn hình mà người dùng có thể tương tác
- Mỗi View thường có một hình dạng và kích thước cụ thể, và có thể hiển thị nội dung như văn bản, hình ảnh, hoặc các thành phần đồ họa khác.
- Các loại View phổ biến
  - **Button**: Nút bấm mà người dùng có thể nhấp vào để thực hiện một hành động.
  - **Label**: Hiển thị văn bản tĩnh, không thể chỉnh sửa.
  - **TextBox**: Hộp nhập văn bản cho phép người dùng nhập và chỉnh sửa văn bản.
  - **ImageView**: Hiển thị hình ảnh.
  - **CheckBox**: Hộp kiểm cho phép người dùng chọn hoặc bỏ chọn một tùy chọn.
  - **RadioButton**: Nút chọn cho phép người dùng chọn một trong nhiều tùy chọn.

![alt text](image-22.png)
## 4.3. ViewGroup
- ViewGroup là container chứa các View và quản lý các View con nằm trong nó.
- ViewGroup cũng có thể chứa các ViewGroup khác

![alt text](image-23.png)
## 4.4. Layout
- Layout tổ chức, quản lý kích thước, vị trí, bố cục của các View, ViewGroup một cách hiệu quả và có hệ thống giúp đảm bảo giao diện trực quan và dễ sử dụng cho người dùng.
- Các loại Layout phổ biến:
  - **LinearLayout**: Sắp xếp các thành phần theo hàng ngang hoặc dọc.
  - **GridLayout**: Sắp xếp các thành phần theo dạng lưới, với các hàng và cột.
  - **FlowLayout**: Sắp xếp các thành phần theo dòng chảy, từ trái sang phải và từ trên xuống dưới.
  - **BorderLayout**: Sắp xếp các thành phần theo các vùng biên (Bắc, Nam, Đông, Tây, Trung tâm).


![alt text](image-24.png)

Trong thực tế, khi làm sản phẩm ta sẽ phải kết hợp rất nhiều Layout với các kiểu khác nhau để bố cục được hài hòa và thuận mắt với người dùng
## 4.5. Event Handling
- Event: Là một hành động hoặc sự kiện xảy ra, chẳng hạn như nhấp chuột hoặc gõ bàn phím, di chuyển chuột.
- Event Handling: Là quá trình lắng nghe và phản hồi lại các sự kiện này
- Các thành phần chính của Event Handling:
  - **Event Source**: Là nơi mà sự kiện được kích hoạt, chẳng hạn như một nút bấm hoặc một hộp văn bản.
  - **Event Object**: Là đối tượng chứa thông tin chi tiết về sự kiện, chẳng hạn như loại sự kiện, vị trí xảy ra sự kiện, và các thông tin liên quan khác.
   - **Event Listener**: Là một đối tượng hoặc phương thức được đăng ký để lắng nghe và xử lý sự kiện khi nó xảy ra.
- Quy trình xử lý sự kiện:
  - **Đăng ký Listener**: Đăng ký Listener với Event Source
  - **Kích hoạt sự kiện**: Khi sự kiện xảy ra, Event Source sẽ tạo ra một Event Object và gọi phương thức của listener tương ứng.
  - **Xử lý sự kiện**: Listener sẽ thực hiện các hành động cần thiết để phản hồi lại sự kiện.
  
![alt text](image-25.png)

![alt text](image-26.png)
