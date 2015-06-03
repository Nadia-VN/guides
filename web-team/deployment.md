# PHP deployment guide (Mac OS)

## 1. Thực thi trên môi trường Local
* Khởi tạo dự án.
	* Clone project từ remote (git clone remote) 
* Hoàn thiện chức năng 
* Test trên local
* Push các file mới hoặc đã thay đổi lên remote (git push)
Tham khảo thêm về git
* <https://www.atlassian.com/git/tutorials/>
* <http://git-scm.com/docs/gittutorial>

## 2. Thực thi trên các môi trường dev, stg, production
### 1 Kết nối đến server
* Kết nối sử dụng ssh
    - ssh sử dung username and password
    ssh username@host và điền password.
    - ssh sử dụng username and file .pem
    ssh -i path_to_file_pem username@host
* Lưu ý cần chmod 400 cho file .pem.
* Kết nối sử dụng sftp
    - Sử dụng filezilla để connect to server
### 2. Thao tác deployment trên server
* Việc deployment phải tuần tự trên server từ các môi trường : dev, stg và production.
#### Bước 1 : cần phải up dữ liệu từ local lên server:
    - Sử dụng git :
        + Sử dụng git để lấy code mới nhất trên remote về (git pull).
    - Sử dụng sftp :
        + Upload những file đã thay đổi lên server.
        + Chú ý những file, folder cần chmod permission.
    - Sử dụng ssh :
        + Đối với việc up các file lên ta sử dụng lện sau
    Trong trường hợp server không cài đặt git chúng ta cần thực thi up các file, folder đã thay đổi lên server:
        + Đối với việc up các file lên ta sử dụng lện sau
            * scp file_local username@host:~path_to_file_host
        + Đối với việc up các folder:
            * Nén folder đó lại 
                - tar pzcf {folder_name}.tgz {folder_name}
            * Copy lên server
                - scp path_to_{forder_name}.tgz 
                - username@host:~path_to_{forder_name}
            * Giải nén trên server
                - tar pzxf {folder_name}.tgz.
#### Bước 2 : Config để dự án có thể chạy được trên server
    * Config database
    * Config Base_url
    * Symlink domain tới folder project
### 3. Thao tao tác với database trên server
* Đối với môi trường dev :
    - Có thể dump dữ liệu để test, thao tác với dữ liệu
* Đối với môi trường stg
    - Chỉ được thao tác với các dữ liệu chính xác.
* Đối với môi trường production
    - Không được có một thao tác nào đối với db, cần confirm với khách hàng trước khi có 1 hành động nào đó.
### 4. Test
* Đối với thao tác deployment trên tất cả các môi trường đều phải test lại đối với các chức năng mới được update.
* Nếu trong trường hợp xảy ra lỗi trên production cần phải revert về version đang được chạy tốt trước đó.  
