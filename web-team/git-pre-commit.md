# Sử dụng Git commit hook để  check code error and style

### Table of contents
***

1. [PHP](#php)
 
***

### PHP
* Cài đặt phpcs (PHP Code Sniffer)
	
	```sh
	$ composer require --dev squizlabs/php_codesniffer
	```
* Tạo mới file ```.git/hooks/pre-commit``` với nội dung như sau

	```sh
	#!/bin/sh
	 
	STAGED_FILES=`git diff --cached --name-only --diff-filter=ACMR HEAD | grep \\\\.php`
	 
	echo "Checking PHP Lint..."
	for FILE in $STAGED_FILES
	do
		php -l -d display_errors=0 $FILE
		if [ $? != 0 ]
		then
			echo "Fix the error before commit."
			exit 1
		fi
		FILES="$FILES $FILE"
	done
	 
	if [ "$FILES" != "" ]
	then
		echo "Running Code Sniffer..."
		./vendor/bin/phpcs --standard=PSR1 --encoding=utf-8 -n -p $FILES
		if [ $? != 0 ]
		then
			echo "Fix the error before commit."
			exit 1
		fi
	fi
	 
	exit $?
	``` 
* Thay đổi quyền của file để git có thể gọi file này

	```
	$ chmod +x .git/hooks/pre-commit
	```
* Với setup như vậy, mỗi lần chạy câu lệnh ```git commit``` thì pre-commit hook sẽ được chạy và check các file được stage trong commit. Nếu có lỗi thì commit sẽ không được chấp nhận.