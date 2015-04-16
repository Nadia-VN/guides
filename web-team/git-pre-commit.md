# Sử dụng Git commit hook để  check code error and style

### Table of contents
***

1. [PHP](#php)
2. [Javascript](#javascript)
 
***

### PHP
* Cài đặt phpcs (PHP Code Sniffer)
	
	```sh
	$ composer require --dev squizlabs/php_codesniffer
	```
* Tạo mới file ```.git/hooks/pre-commit``` với nội dung như sau. Có thể đổi PSR1 thành các chuẩn mà PHPCS hỗ trợ (PSR2, Zend, PEAR)

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


### Javascript
* Cài đặt eslint (cần phải cài nodejs hoặc iojs)

	```sh
	$ npm -g install eslint
	```
* Tạo mới file pre-commit (nếu file này chưa tồn tại) hoặc add thêm đoạn code sau vào file pre-commit đã có

	```sh
	#!/bin/sh
 
	STAGED_FILES=$(git diff --cached --name-only --diff-filter=ACM | grep ".jsx\{0,1\}$")
	 
	if [ "$STAGED_FILES" = "" ]; then
	  exit 0
	fi
	 
	PASS=true
	 
	echo "\nValidating Javascript:\n"
	 
	for FILE in $STAGED_FILES
	do
	  RES=$(eslint ${FILE} | grep "problem")
	  if [ "$RES" != "" ]; then
	    echo "\t\033[32mESLint Failed: ${FILE}\033[0m"
	    PASS=false
	  else
	    echo "\t\033[32mESLint Passed: ${FILE}\033[0m"
	  fi
	done
	 
	echo "\nJavascript validation completed\n"
	 
	if ! $PASS; then
	  echo "\033[41mCOMMIT FAILED:\033[0m Your commit contains files that should pass ESLint but do not. Please fix the ESLint errors and try again.\n"
	  exit 1
	else
	  echo "\033[42mCOMMIT SUCCEEDED\033[0m\n"
	fi
	 
	exit $?
	```
* Thay đổi quyền của file

	```
	$ chmod +x .git/hooks/pre-commit
	```
* Mỗi lần commit với git thì các file .js hoặc .jsx sẽ được check