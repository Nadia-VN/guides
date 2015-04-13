# Git guide
***



1. ### Common git operations and commands
	* Tài liệu: [Backlog's Git Guide](http://backlogtool.com/git-guide/vn/intro/intro1_1.html)
	* Thời gian hoàn thành: 3 ngày
	* Output:
		* Nắm được cấu trúc và cách hoạt động của git
		* Nắm được các câu lệnh git cơ bản 	

2. ### Git style guide
	_Lấy từ [https://github.com/agis-/git-style-guide](https://github.com/agis-/git-style-guide)_
	#### General
	* Trước mỗi dự án cần tìm hiểu vào tạo file ```.gitignore``` phù hợp để ignore những file không cần thiết
	* Cần test kĩ trước khi push lên remote repo
	* Thỉnh thoảng nên optimize local repo dùng các câu lệnh sau
		* [git gc](http://git-scm.com/docs/git-gc)
		* [git prune](http://git-scm.com/docs/git-prune)
		* [git fsck](http://git-scm.com/docs/git-fsck)

	#### Branches
	* Tên của branch cần ngắn gọn nhưng vẫn thể hiện được nội dung cần thiết

		```sh
		# Good
		$ git checkout -b fix-facebook-login

		# Bad - ko rõ ràng nội dung
		$ git checkout -b login_fix
	```
	* Sử dụng ký tự ```-``` để phân cách giữa các từ
	* Nếu có nhiều người cùng làm việc trên 1 feature branch thì nên tạo 1 feature branch chung cho cả team và mỗi thành viên có 1 branch cá nhấn. Format: 
		* feature-name/master - branch chung
		* feature-name/linhtm - Working branch của Linh
		* feature-name/tuvd - Working branch của Tú


	#### Commits
	* Mỗi commit nên chỉ bao gồm 1 thay đổi về mặt logic trong code. Không nên để nhiều thay đổi trong 1 commit. Ví dụ: trong 1 lần code mà mình đồng thời sửa 1 bug và tối ưu hoá 1 tính năng thì nên để thành 2 commits.
	* Ngược lại, không nên chia 1 thay đổi về mặt logic ra nhiều commits.
	* Commit liên lục và thường xuyên. Các commit nhỏ và độc lập sẽ dễ hiểu và có thể dễ dàng revert lại hơn
	* Commit cần được sắp xếp 1 cách logic. Ví dụ nếu commit X phụ thuộc vào những thay đổi của commit Y, thì commit Y cần được đặt trước commit X

	#### Messages
	* Không nên sử dụng quick commit message ```-m``` khi commit (trừ trường hợp dự án cá nhân, ko quan trọng). Sử dụng quick commit message thường dẫn đến message quá ngắn gọn không rõ ràng.

		```sh
		# Good
		$ git commit
		
		# Bad
		$ git commit -m "Quick fix"
	```
	* Dòng tóm tắt message của commit (dòng đầu) cần ngắn gọn, xúc tích. Tốt nhất là không nên quá 50 ký tự. Cần viết hoa đầu dòng và không nên có dấu chấm kết thúc.
	
		```
		# good - imperative present tense, capitalized, less than 50 characters
		Mark huge records as obsolete when clearing hinting faults

		# bad
		fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
		```
	* Sau dòng tóm tắt, đối với những commit phức tạp cần giải thích thì cần cách 1 dòng và viết thêm 1 đoạn mô tả. Đoạn mô tả này nên được sao cho mỗi dòng < 80 ký tự và giải thích rõ vì sao cần phải có commit này, cách giải quyết vấn đề và các tác dụng phụ có thể có. Nếu commit này resolve 1 issue nào đó, thì issue ấy cũng cần được đề cập (#number, #link)

		```
		Short (50 chars or less) summary of changes

		More detailed explanatory text, if necessary. Wrap it to
		72 characters. In some contexts, the first
		line is treated as the subject of an email and the rest of
		the text as the body.  The blank line separating the
		summary from the body is critical (unless you omit the body
		entirely); tools like rebase can get confused if you run
		the two together.

		Further paragraphs come after blank lines.

		  - Bullet points are okay, too

		  - Typically a hyphen or asterisk is used for the bullet,
		    preceded by a single space, with blank lines in
		    between, but conventions vary here

		Taken from http://git-scm.com/book/ch5-2.html
		```
	* Nếu commit A phụ thuộc vào commit B thì sự phụ thuộc này nên được nêu trong commit message của commit A (sử dụng commit hash). Ngoài ra nếu commit A xử lý 1 bug mà do commit B gây nên thì điều này cũng nên được nêu.

	### Merging
	* Không nên thay đổi history của git repo. History của repo rất quan trọng trong việc xác định những gì đã xảy ra. Thay đổi history thường mang đến nhiều vấn đề trong quá trình phát triển.
	* Các trường hợp có thể thay đổi history
		* Chỉ có 1 người duy nhất làm việc trong branch và history của branch này không quan trọng (không cần review)
		* Branch cần được dọn dẹp (squash commit) và rebase lên branch chính để có thể merge vào branch chính
	* Tuy nhiên không bao giờ được thay đổi history của các branch chính (master, develop) hay bất kì branch nào dùng để deploy
	* Luôn có gắng để giữ history đơn giản và gọn. Trước khi merge 1 branch vào branch chính:
		* Cần đảm bảo các commit và history đúng theo style guide. Nếu không cần phải chỉnh sửa (squash/reorder, reword messages etc...)
		* Rebase branch này lên branch mà nó sắp được merge vào.
	* Nếu branch chứa nhiều hơn 1 commit thì khi merge branch này vào branch khác không sử dụng option fast-forward. Điều này sẽ giúp luôn luôn có 1 merge commit được tạo ra
	
	```sh
	# Good
	$ git merge --no-ff my-branch 
	# Bad
	$ git merge my-branch

	```
	
 ### Tag
 * Sử dụng annotated tags để đánh dấu các release hoặc các sự kiện, phiên bản quan trọng (alpha, beta)
 
	 ```sh
	 $ git tag -a v1.4 -m 'my version 1.4'
	 $ git tag
	  v0.1
	  v1.3
	  v1.4
	 ```

 * Sử dụng lightweight tags cho mục địch cá nhân, bookmark v..v..
 	
	 	```sh
	 	$ git tag v1.4-lw
		```
 
2. ### Recommended Git flow

* Sẽ có 3 hoặc 4 branch chính trên remote repo tuỳ theo dự án
	* __Master__ - Để deploy lên môi trường production
	* __Staging__ - Để deploy lên môi trường staging
	* (Optional) __Testing__ - Để deploy lên môi trường test hoặc build server
	* __Develop__ - Branch chính dành cho develpment, mọi hoạt động development sẽ diễn ra trên branch này
* __Workflow__
	* __Phát triển 1 tính năng mới - 1 người làm duy nhất feature này__
		* Tạo 1 branch mới
		
		```sh 
		$ git checkout -b new_feature
		```
		* Sau khi đã hoàn thành việc phát triển => commit các thay đổi
		
		```sh
		$ git commit -m 'Complete new feature'
		```
		* Pull những thay đổi mới nhất từ branch develop remote về local và rebase những thay đổi trên feature branch vào branch develop trên local

		```sh
		$ git checkout develop
		$ git pull
		$ git checkout new_feature
		$ git rebase -i develop
		```
		* Sử dụng rebase -i để có thể lựa chọn các commit muốn giữ sử dụng pick và squash
		
		```sh
		pick ae3a3dc Adding first part of new feature
 		squash 3c82ad8 Adding second part
 		```
 		* Merge branch feature này vào branch develop và (optional) delete branch feature

 		```sh
 		$ git checkout develop
 		$ get merge new_feature
 		$ git push origin develop
 		$ git branch -d new_feature
 		```
 	* __Phát triển tính năng mới, nhiều người cùng làm 1 tính năng__
 		* Tạo 1 branch feature chung có chức năng như base cho team làm feature này và push branch này lên remote

 		```sh 
		$ git checkout -b new_feature/master
		$ git push -u origin new_feature/master
		```
		* Mỗi người trong team sẽ tạo feature branch riêng của mình trên local từ branch new_feature/master và thực hiện công việc trên branch đó
		
		```sh
		$ git checkout -b new_feature/member_name
		```
		* Sau khi hoàn thành phát triển thì tương tự như với trường hợp 1 người làm 1 feature branch nhưng thay vì rebase vào branch develop thì sẽ rebase vào branch new_feature/master.
		
		```sh
		$ git checkout new_feature/master
		$ git pull
		$ git checkout new_feature/member_name
		$ git rebase -i new_feature/master
		$ git checkout new_feature/master
 		$ git merge new_feature/member_name
		```
		* Sau đó, team lead sẽ rebase branch feature này vào develop tương tự như flow 1 người
		* Kết thúc có thể delete feature branch dưới local và trên remote.

		```sh
		$ git branch -d new_feature/member_name
		$ git branch -d new_feature/master
		$ git push origin --delete new_feature/master
		```
	* __Release__ sản phẩm
		* Merge branch develop vào master (done by team leader)
		
		```sh
		$ git checkout master
		$ git merge develop
		```
		* Đánh dấu tag cho release 
		
		``` sh
		$ git tag -a v1.0 -m 'First release
		```
		* Push tất cả lên remote repo
		
		```sh
		$ git push
		$ git push --tags
		```
	* __Hotfix__ Trong trường hợp tìm thấy lỗi đang chạy trên production.
		* Tạo 1 branch hotfix trực tiếp từ master
		
		```sh
		$ git checkout -b hotfix-{ issue-number }
		```
		* Sau khi fix xong merge lại vào master và push lên remote repo. Trong trường hợp lỗi lớn có thể đánh dấu tag
		
		```sh
		$ git checkout master
		$ git merge hotfix-{ issue-number }
		$ git tag -a v1.0-patch1 -m 'Yo, fixed the bug'
		$ git push
		$ git push --tags
		$ git branch -d hotfix-{ issue-number }
		```
		* Merge back những thay đổi từ master vào develop
		
		```sh
		$ git checkout develop
		$ git merge master
		$ git push origin develop
		```