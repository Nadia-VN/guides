# Environment for PHP developer
***


### 1.  Install GIT

- Download file "git-osx-installer" tại [trang chủ của git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git) và install.
- Sau khi cài đặt xong vào terminal đánh lệnh *git --version*  kiểm tra xem git có được cài trên máy thành công chưa.

### 2.  Setup environment for develop (Apache, MySQL, PHP)

Để cài đặt Apache, MySQL, PHP trên MacOS thì cài MAMP và Homestead (Cài 1 trong 2 cái là đã ok!)
#### 2.1. Cài đặt [MAMP](https://www.mamp.info/en/)
#### 2.2. Cài đặt Homestead

- Note: Trước khi cài đặt homestead bạn phải cài đặt virtual box và vargrant.
- Tham khảo tại [Homestead installed](http://laravel.com/docs/5.0/homestead)

### 3. Terminal

- Sử dụng [Iterm2](https://www.iterm2.com/) thay cho terminal mặc định trong MacOS
- Cài đặt plugin [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) để hỗ trợ cho terminal.
    - install using curl. Copy đoan text dưới đây vào terminal.
    
       `curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh`

### 4. [Composer](https://getcomposer.org/download/).

- Install Local
`curl -sS https://getcomposer.org/installer | php`

- Install Global
`mv composer.phar /usr/local/bin/composer`

Tham khảo thêm tại [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx)

### 5. Cài đặt Laravel
- Sử dụng composer để cài đặt
- Cài đặt laravel hiện tại (Laravel 5).

    cd vào thư mục project của bạn rồi chạy lệnh.
    
    `composer create-project laravel/laravel --prefer-dist`
    
- Cài đặt laravel 4.2 (Phiên bản mà công ty đang sử dụng cho các dự án)

    cd vào thư mục project của bạn rồi chạy lệnh.
    
    `composer create-project laravel/laravel {directory} 4.2 --prefer-dist`

### 6.  Editor

- Công ty sử dụng sublime text 3 để phát triển các dự án web

- Link down [sublime text 3](http://www.sublimetext.com/3)
- Ngoài ra bạn có thể cài thêm các plugin support cho sublime text. [Link](http://wasil.org/sublime-text-3-perfect-php-development-set-up).
  Ngoài ra cài đặt thêm: SublimeLinter-phpcs, AlignTab, CodeFormatter, DocBlockr, Emmet"
  
  
### 7. [Virtual box](https://www.virtualbox.org/) + [Vagrant](https://www.vagrantup.com/) : Support việc cài đặt homestead.

### 8. [Filezilla](https://filezilla-project.org/) : Dùng để FTP và SFTP vào server.

### 9. [Sequel Pro](http://www.sequelpro.com/) : Database management.



