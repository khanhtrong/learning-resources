# Học Git

## Chuẩn bị

1. Cấu hình ban đầu
	* `git config --global user.name "Username"`
	* `git config --global user.email emailaddress@test.com`

2. Tạo dự án mới (Windows)
	* Tạo thư mục cho dự án

3. Dùng Git cho dự án
	* Nhấp chuột phải vào thư mục dụ án
	* Chọn Git Bash here
	* Gõ `git init`
	* Git đã được áp dụng vào thư mục

4. Tạo kho chứa (repositories) mới trên Github
	* Đăng ký tài khoản Github
	* Đăng nhập vào tài khoản
	* Tạo kho chứa, VD: `testgit`
	* Đường dẫn đến kho chứa sẽ là: `https://github.com/username/testgit` hoặc `git://github.com/username/testgit`

5. Đẩy dữ liệu lên kho chứa trên github
	* Gõ (tên máy chủ là origin)
		* Github: `git remote add origin https://github.com/username/testgit.git`
		* BitBucket: `git remote add origin https://username@bitbucket.org/username/testgit.git`
	* Gõ `git push -u [tên-máy-chủ] [tên-nhánh]`, VD: `git push -u origin master`
	* Lần đầu thực hiện Git sẽ yêu cầu nhập thông tin đăng nhập Github

6. Tải kho chứa về máy cục bộ (local)
	* Nhấp chuột phải vào thư mục dụ án
	* Chọn Git Bash here
	* Gõ `git clone git://github.com/username/testgit`: lấy toàn bộ kho chứa
	* `git pull [tên-máy-chủ] [tên-nhánh]`: Lấy những dữ liệu thay đổi
	* `git pull --rebase [tên-máy-chủ] [tên-nhánh]`

7. Một số lệnh remote
	* `git remote`: Xem cấu hình máy chủ từ xa
	* `git remote -v`: Xem chi tiết cấu hình máy chủ từ xa
	* `git remote add [tên-máy-chủ] https://github.com/username/ten-kho-chu.git`: Thêm kho chứa từ xa
	* `git push [tên-máy-chủ] [tên-nhánh]`: Đẩy dữ liệu lên máy chủ từ xa
	* `git remote show [tên-máy-chủ]`: Kiểm tra tên máy chủ trung tâm
	* `git remote rename ten-a ten-b`: Đổi tên máy chủ ten-a thành ten-b từ xa
	* `git remote rm tên-máy-chủ`: Xóa tên-máy-chủ từ xa

8. Một số lênh khách trong branch
	* `git branch ten_nhanh`: Tạo nhánh
	* `git branch -d ten_nhanh`: Xóa nhánh
	* `git branch -D ten_nhanh`: Ép xóa tên nhánh
	* `git branch`: Xem danh sách nhánh (Sẽ thấy HEAD đang ở nhánh nào)
	* `git checkout -b [tên-nhánh]`: Tạo vào chuyển vào nhánh (không cần qua 2 bước)

9. Chuyển đổi giữa các nhánh: `git checkout branch_name`

10. Trộn (merge) nhánh: `git merge branch_name`
	* VD: Nếu muốn trộn nhánh B vào nhánh A, ta chuyển về nhánh A sau đó gõ `git merge B`

## Lệnh Git

1. Theo dõi file mới: `git add filename`
	* `git add *.txt`: Thêm tất cả các file có đuôi `.txt`
	* `git add *`: Thêm tất cả file
	* Ghi chú: Nếu ta chạy `git add filename` sau đó thay đổi nội dung file, ta phải chạy lại `git add` lần nữa để cập nhật lần thay đổi mới nhất.

2. Xóa file: `rm filename`
	* `rm filename`: File sẽ được xóa khỏi khu vực stage, và không được commit trong lần tới
		* Nếu muốn lấy lại file sau lệnh này, ta gõ `git checkout -- filename`
	* `git rm filename`: Tập tin sẽ được gỡ bỏ trong lần commit tiếp theo
	* `git rm filename -f`: Nếu file đã được sửa và thêm vào khu vực stage, ta phải ép Git xóa bằng `-f`  

		Nếu muốn lấy lại file sau 2 lệnh `git rm filename` và `git rm filename -f` ta làm như dưới đây
		* `git reset HEAD filename`: Đưa file về trạng thái như lệnh `rm filename`
		* `git checkout -- filename`: Lấy lại file

	* `git rm --cached filename`: Gỡ bỏ file khỏi khu vực stage và đưa về trạng thái untrack, đây là cách an toàn.

3. Xem thay đổi Stage và Unstage: `git status`
4. Xem chi tiết thay đổi Stage và Unstage: `git diff`
	* `git diff --cached`
	* `git diff --staged` (V1.6.1 and higher)

5. Commit thay đổi: `git commit`
	* `git commit -m "Ghi chú thay cho lần thay đổi này"`
	* `git commit -a -m "Ghi chú thay cho lần thay đổi này"`: Commit bỏ qua thao tác `git add`

6. Di chuyển file: `git mv file_from file_to`
	* `git mv README.md NEWNAME.txt`: Di chuyển và đổi tên file từ README.md thành NEWNAME.txt trong cùng thư mục
	* Câu lệnh trên thực hiện các bước tương tụ như bên dưới:
		* `git rm README.md`
		* `git add NEWNAME.txt`

7. Liệt kê danh sách file trong Staged: `git ls`
	* `git ls-files`: Liệt kê tất cả tên file
	* `git ls-tree --full-tree -r HEAD`: Liệt kê tất cả file đã commit với thông tin đầy đủ

8. Xem lịch sử commit: `git log`
	* `git log -p` : hiển thị nội dung thay đổi trong log
	* `git log -p -2` : hiện thị nội dung thay đổi 2 lần gần nhất
	* `git log --stat` : Xem một số thống kê tóm tắt cho mỗi commit
	* `git log --pretty=oneline` : in mỗi commit trên một dòng
		+ `--pretty=short`
		+ `--pretty=full`
		+ `--pretty=fuller`

	* git log `--pretty=format:"%h - %an, %ar : %s"` : cho ra kết quả dạng như bên dưới
		```
		ca82a6d - Scott Chacon, 11 months ago : changed the version number
		085bb3b - Scott Chacon, 11 months ago : removed unnecessary test code
		a11bef0 - Scott Chacon, 11 months ago : first commit
		```

		Một số các lựa chọn của format

		+ `%H`	Mã băm của commit
		+ `%h`	Mã băm của commit ngắn gọn hơn
		+ `%T`	Băm hiển thị dạng cây
		+ `%t`	Băm hiển thị dạng cây ngắn gọn hơn
		+ `%P`	Các mã băm gốc
		+ `%p`	Mã băm gốc ngắn gọn
		+ `%an`	Tên tác giả
		+ `%ae`	E-mail tác giả
		+ `%ad`	Ngày "tác giả" (định dạng tương tự như lựa chọn --date= )
		+ `%ar`	Ngày tác giả, tương đối
		+ `%cn`	Tên người commit
		+ `%ce`	Email người commit
		+ `%cd`	Ngày commit
		+ `%cr`	Ngày commit, tương đối
		+ `%s`	Chủ để

	* `git log --pretty=format:"%h %s" --graph` : hiển thị dạng biểu đồ nhánh

	* `git log --since=2.weeks`: Giới hạn thông tin đầu ra
		* `-(n)`				Chỉ hiển thị n commit mới nhất
		* `--since`, `--after`	Giới hạn các commit được thực hiện sau ngày nhất định.
		* `--until`, `--before`	Giới hạn các commit được thực hiện trước ngày nhất định.
		* `--author`			Chỉ hiện thị các commit mà tên tác giả thoả mãn điều kiện nhất định.
		* `--committer`			Chỉ hiện thị các commit mà tên người commit thoả mãn điều kiện nhất định.

		* VD: `git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
		--before="2008-11-01" --no-merges -- t/`
