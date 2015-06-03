# Ruby on Rails Environment setup guide (Mac OS)

### 1. Setup Environment
* Để quản lý version ruby thì sử dụng 1 trong 2 phần mềm sau
	* [RVM](https://rvm.io/)
	* [Rbenv](https://github.com/sstephenson/rbenv). Nên cài thêm các plugin sau
		* [Rbenv-gem-rehash](https://github.com/sstephenson/rbenv-gem-rehash)
		* [Rbenv-bundler](https://github.com/carsomyr/rbenv-bundler)
* Sử dụng __RVM__
	* Cài đặt

		```
		$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
		$ \curl -sSL https://get.rvm.io | bash -s stable
		```
	* Cài Ruby
		
		```
		# List các phiên bản ruby có thể cài
		$ rvm list known
		# Cài đặt
		$ rvm install 2.2.1
		# Chuyển sang sử dụng 1 phiên bản ruby
		$ rvm use 2.2.1
		# Set 1 phiên bản ruby là phiên bản mặc định
		$ rvm --default use 2.2.1
		```
* Sử dụng __Rbenv__
	* Cài đặt
		
		```
		$ git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
		$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile (hoặc .zprofile nếu dùng zsh)
		$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile # (hoặc .zprofile nếu dùng zsh)
		# Cài đặt ruby-build
		$ git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
		# Sau đó restart terminal
		```
	* Cài Ruby

		```
		$ rbenv install 2.2.1
		# set default ruby version
		$ rbenv global 2.2.1
		# set default ruby version for a folder
		$ rbenv local 2.2.0
		```
		  

### 2. Tools
* Nếu sử dụng PostgreSQL thì nên dùng [Postgres.app](http://postgresapp.com/) để chạy PostgreSQL
* Terminal nên dùng [iTerm 2](https://www.iterm2.com/)
	* Dùng __zsh__ và [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) sử dụng [theme](https://github.com/robbyrussell/oh-my-zsh/wiki/themes) thích hợp hỗ trợ hiển thị ruby version
* Editor
	* Sublime Text
	* Macvim
	* Rubymine  
