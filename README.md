# Hắc Thoại Lạc Hồng

Chào mừng bạn đến với kho mã nguồn (repository) của dự án! Tài liệu này cung cấp đầy đủ hướng dẫn để thiết lập môi trường làm việc, tuân thủ quy trình Git của nhóm và gửi công việc một cách hiệu quả.

---

# 🛠️ 1. Thiết Lập Môi Trường & Repository

## Cài Đặt Git & Git LFS

Các dự án Unreal Engine sử dụng rất nhiều tài nguyên dạng nhị phân (binary) như `.uasset`, `.umap`, mô hình 3D, texture và âm thanh. Git thông thường không phù hợp để quản lý các tệp lớn này nếu không sử dụng **Git LFS (Large File Storage)**.

### Bước 1: Cài đặt Git

Tải và cài đặt Git tại:

https://git-scm.com/

### Bước 2: Khởi tạo Git LFS

Mở Command Prompt hoặc Terminal và chạy lệnh sau:

```bash id="gitlfs01"
git lfs install
```

---

## Cấu Hình Chuẩn Cho `.gitignore`

Đảm bảo thư mục gốc của dự án có tệp `.gitignore` với nội dung sau để tránh đưa các tệp tạm thời hoặc được sinh tự động vào repository:

```gitignore id="gitignore01"
# Thư mục tạm và dữ liệu được Unreal Engine sinh tự động

/Binaries/
/Intermediate/
/DerivedDataCache/
/Saved/
/Build/

# Thư mục tạm của Plugin

/Plugins/*/Binaries/*
*/Plugins/*/Intermediate/

# File của IDE & Solution

/*.sln*
*.vs/*
*.idea/*
*.vscode/*
*/*.xcodeproj
/*.xcworkspace

# File biên dịch

*.dll
*.exe
*.o
*.obj

# File hệ thống

.DS_Store
Thumbs.db
$RECYCLE.BIN/
```

---

## ⚠️ Quy Tắc Quan Trọng Đối Với Tệp Nhị Phân Của Unreal Engine

### Không Tự Động Merge Tệp Binary

Các tệp Blueprint (`.uasset`) và Level (`.umap`) là tệp nhị phân.

Nếu hai người cùng chỉnh sửa một tệp `.uasset` hoặc `.umap` tại cùng thời điểm, Git không thể tự động gộp thay đổi và rất dễ dẫn đến mất dữ liệu.

### Phối Hợp Khi Làm Việc Với Asset

Luôn trao đổi với các thành viên khác trước khi chỉnh sửa:

* Các level dùng chung.
* Các Blueprint cốt lõi.
* Các asset quan trọng của dự án.

---

# 📜 2. Các Quy Tắc Git Workflow Bắt Buộc

Vui lòng tuân thủ nghiêm ngặt 5 quy tắc sau để đảm bảo tính ổn định của dự án và lịch sử commit rõ ràng.

## 1. Mỗi Tính Năng Sử Dụng Một Branch Riêng

* Luôn tạo một branch mới từ `main` cho mỗi task.
* Không tái sử dụng branch cũ cho nhiều task khác nhau.

❌ Sai:

```text id="wrongbranch01"
john-dev
feature-character
```

✅ Đúng:

```text id="rightbranch01"
TSK-101
GAME-42
BUG-08
```

---

## 2. Quy Tắc Đặt Tên Branch

Tên branch **bắt buộc** phải là mã Task ID được giao.

Ví dụ:

* `TSK-101`
* `GAME-42`
* `BUG-08`

🚨 Bất kỳ branch nào sử dụng tên tùy ý hoặc không đúng quy chuẩn sẽ bị xóa khỏi remote repository mà không cần thông báo trước.

---

## 3. Gửi Công Việc (Merge Request Vào `develop`)

Khi hoàn thành tính năng và đã kiểm thử trên Unreal Engine:

1. Push branch của bạn lên remote.
2. Tạo Merge Request (MR) hoặc Pull Request (PR).
3. Chọn nhánh đích là `develop` (**không phải** `main`).
4. Sao chép đầy đủ mẫu checklist MR vào phần mô tả.
5. Tự xác nhận toàn bộ checklist trước khi gửi review.

---

## 4. Review Code & Asset

Chỉ các Lead Developer hoặc thành viên được cấp quyền merge mới được phép:

* Review MR.
* Approve MR.
* Merge vào `develop`.

Người review sẽ:

* Kiểm tra checklist.
* Xác minh Blueprint và code.
* Kiểm tra asset thay đổi.
* Thực hiện merge.

---

## 5. Đồng Bộ Theo Milestone

Khi hoàn thành một milestone hoặc khi Game Designer (GD) yêu cầu:

* Các branch đã được approve sẽ được merge vào `main`.
* Sau khi `main` được cập nhật, tất cả thành viên đang làm việc trên branch riêng phải đồng bộ ngay lập tức.

### Hành Động Bắt Buộc

Mỗi khi `main` có thay đổi:

```text id="syncwarning01"
Pull và cập nhật branch của bạn ngay lập tức
để tránh xung đột merge nghiêm trọng về sau.
```

---

# 📖 3. Hướng Dẫn Sử Dụng Git Qua Command Line

## Bắt Đầu Một Task Mới

```bash id="newtask01"
# 1. Chuyển sang nhánh main và lấy dữ liệu mới nhất

git checkout main
git pull origin main

# 2. Tạo branch mới theo Task ID

git checkout -b TSK-123
```

---

## Lưu Và Đẩy Công Việc Lên Remote

```bash id="pushwork01"
# 1. Kiểm tra file đã thay đổi

git status

# 2. Đưa file vào staging

git add .

# 3. Commit với nội dung rõ ràng

git commit -m "TSK-123: Implement player double jump logic"

# 4. Push branch lên remote

git push -u origin TSK-123
```

---

## Đồng Bộ Branch Với `main`

```bash id="syncmain01"
# Cập nhật branch hiện tại với nội dung mới nhất từ main

git checkout main
git pull origin main

git checkout TSK-123
git merge main
```

---

# 📋 4. Mẫu Merge Request (MR) Checklist

Khi tạo Merge Request vào nhánh `develop`, chọn template checklist-review-merge-request và hoàn thành checklist. Nếu có điểm nào chưa hoàn thành, hãy đảm bảo đã hoàn thành mục đó trước khi check.
```

---

# ❓ Cần Hỗ Trợ?

Nếu gặp phải các vấn đề như:

* Merge conflict.
* Thiếu plugin.
* Blueprint bị lỗi liên kết (Broken Reference).
* Asset bị mất hoặc không đồng bộ.

### KHÔNG ĐƯỢC

```text id="forbidden01"
git push -f
```

* Không force push.
* Không tự ý xóa thư mục dự án.
* Không tự xử lý các xung đột nghiêm trọng khi chưa trao đổi với nhóm.

### Hãy Làm

Liên hệ ngay với:

* Lead Developer.
* Technical Lead.
* Team Lead.

để được hỗ trợ và tránh làm ảnh hưởng đến repository của toàn dự án.

---

**Mục tiêu của quy trình này là đảm bảo:**

* Repository luôn ổn định.
* Giảm thiểu xung đột merge.
* Bảo vệ asset Unreal Engine.
* Dễ dàng truy vết lịch sử phát triển.
* Hỗ trợ phát hành milestone một cách an toàn và hiệu quả.
