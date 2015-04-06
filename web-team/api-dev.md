### [API Programming Guide](#)
***
##### RESTful API
Hầu hết các API hiện tại đều là RESTful API. Các API (web service) mà chúng ta lập trình trong tương lai cũng đều sẽ là RESTful API. Vậy RESTful API là gì?

RESTful API (hay RESTful web service) là 1 api được thiết kế dựa trên giao thức HTTP và các nguyên tắc của kiến trúc [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) (Có thể đọc kĩ thêm để hiểu về REST, mặc dù ko cần thiết lắm, chỉ cần hiểu rõ RESTful API hoạt động thế nào, và implement thế nào). RESTful API là 1 tập hợp của các tài nguyên với 4 đặc điểm sau

* Base URI của web API ví dụ *http://icts.vn/api/users*
* Internet mediatype của dữ liệu trả về được hỗ trợ bởi API (thường là JSON, đây cũng là format dữ liệu mà ta sẽ sử dụng chính yếu)
* Tập hợp các thao tác được hỗ trỡ bởi API sử dụng các HTTP methods (ta sẽ thưởng chỉ sử dụng GET, PUT, POST, DELETE)
* Hypertext driven, đại ý là các clients của API chỉ biết được access path (URI) của 1 resource và từ đó có thể lấy được URI (access path) của các thành phần của resource đó. Ví dụ: ta có resource User với URI là *http://dragon.vn/api/users*. Thì dữ liệu trả về từ URI này sẽ cho phép ta biết được URI để lấy dữ liệu cho User 100 là *http://dragon.vn/api/users/100*

Tham khảo thêm

* <http://rest.elkstein.org/2008/02/what-is-rest.html>
* <https://blog.apigee.com/detail/does_your_api_need_to_be_truly_restful/>


##### RESTful API HTTP methods
Các HTTP methods thông thường được sử dụng trong API bao gồm GET, PUT, POST, DELETE.

* **GET** Lấy thông tin của 1 resource từ API
* **POST** Tạo resource mới
* **PUT** Update thông tin của 1 resource đã có
* **DELETE** Xoá 1 resouce

Ví dụ: Nếu ta có 1 resouces là user thì ta có thể có 1 RESTful API cho User như sau

Base URI: *http://sample.icts.vn/api/users*

HTTP methods | URI | Ý nghĩa | Thông tin trả về 
-------------|-----|---------|--------
POST | http://dragon.vn/api/users | Tạo 1 user mới | Trả về id của user mới này
GET | http://dragon.vn/api/users | Lấy tất cả các user | Trả về thông tin của users (quan trọng là id)
GET | http://dragon.vn/api/users/:id | Lấy thông tin của 1 user | Trả về thông tin của 1 user
PUT | http://dragon.vn/api/users/:id | Update thông tin của 1 user | Trả về thông báo thành công cùng thông tin mới
DELETE | http://dragon.vn/api/users/:id | Xoá bỏ user này | Trả về thông báo thành công

Tham khảo thêm: <http://www.restapitutorial.com/lessons/httpmethods.html>

##### Dữ liệu trả về từ API
Thông thường tuỳ theo trạng thái xử lý request từ client mà API sẽ trả về các HTTP status code khác nhau (tham khảo: <http://www.restapitutorial.com/httpstatuscodes.html>). Tuy nhiên do chúng ta chủ yếu tạo API cho các mobile app, để cho người lập trình client dễ dàng xử lý dữ liệu trả về, sẽ chỉ có status code 200 được sử dụng (HTTP status code mặc định khi trả dữ liệu về, ko cần thêm thắt gì vào code).

JSON là định dịnh dữ liệu trả về chủ yếu mà chúng ta sẽ sử dụng. Các response json trả về cần ít nhất các trường như sau:

* **statusCode**: Khác với HTTP status code, đây là status code do chúng ta tự định tuỳ theo app mà để phù hợp. Ví dụ 0 là thất bại, 1 là thành công
* **message**: Thông báo kèm theo với dữ liệu trả về (cần rõ ràng, ngắn gọn)
* **data**: Dữ liệu trả về

##### Basic security for API

* Nếu API không có hệ thống login/logout chỉ đơn giản là access API thì mỗi request chỉ cần gửi kèm 1 ***apiKey*** (apiKey này chỉ có server và client biết)
* Nếu API có hệ thống login/logout
	* Vẫn cần có 1 ***apiKey*** cho những API mà không cần user phải login
	* Sau khi user đã login thì server cần phải tạo ra 1 unique ***authToken*** riêng cho user đó và trả về cho client. Tất cả các request sau khi user đã login cần phải gửi kèm ***authToken*** này
* Không phương pháp nào là bảo mật hoàn toàn nếu giao tiếp với API vẫn chỉ qua HTTP. Trong các trường hợp cần bảo mật cảo thì nên giao tiếp qua HTTPS (thường bên mình sẽ không tự quyết định được vì cái này cần phải mua certification cho domain và cài đặt lên server) 

