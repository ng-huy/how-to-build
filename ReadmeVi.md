# 
Đầu tiên cần khai báo thông tin dev trên thiết bị
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
Change.txt
```
- File chứa đựng các thay đổi phục vụ quá trình build của Gradle hoặc CI, hiện tại hỗ trợ tiếng Việt và English
- File không phân biệt CRLF hay LF và đều chuyển về LF
- File phải chứa 3 \n\n\n phân cách 2 ngôn ngữ, bắt đầu bằng tiếng Việt và /n/n/n Tiếng Anh thì hệ thống mới xử lý, Ngoài ra thông tin tiếng Việt phải khác với lần build gần nhất
 + Quá trình build Bundle
  > pwsh ./tools/bundle.ps1
  > app.gradle.kts sẽ build Bundle và xử lý changelog.txt(English) và changelogvi.txt(Tiếng Việt) chứa tất cả thay đổi bằng cách ghép thêm vào, cùng với release.xml chứa đựng cùng thư mục để phục vụ việc phát hành
  > trong quá trình trên, change.json cũng được tạo ở assets(./app/main/assets) để phục vụ lưu trữ thông tin thay đổi hiện tại
 + Quá trình build apk
  > pwsh ./tools/build.ps1
  > Tương tự bundle, apk sẽ xử lý thêm tệp manifest, ghi thông tin thay đổi vào tệp để phục vụ báo hiệu cập nhật và xây dựng repo.json
  > Đồng bộ files từ máy chủ CI sang máy chủ Public (vnapps.com/apps)
- Chú ý, nếu Change.txt xóa trắng hoặc giữ nguyên, việc xử lý change logs sẽ bỏ qua phiên bản build hiện tại.
Ứng dụng cần xử lý assets và manifest để lấy các thông tin (trước hoặc sau build) để hiển thị nếu cần.
Để phát hành bundle, khuyến cáo copy nội dung có sẵn từ release.xml để giúp người dùng hiểu rõ hơn thay đổi của ứng dụng
```
```
Thay đổi từ build script 3.6, changelog phải khai báo trước khi muốn nâng cấp phiên bản, để đảm bảo tính đồng bộ, hoặc có thể bỏ qua nếu không muốn cung cấp
```
push.ps1
```
Phần lớn các commit không cần hoặc không muốn công bố thay đổi, push.ps1 phục vụ việc sao lưu code nhanh hoặc đẩy nhanh cho CI
Change.txt cung cấp thay dổi lớn, các thay đổi trong quá trình commit có thể không cần thiết.
sử dụng cmd.exe /c "start pwsh ./push.ps1" cho phím vật lý (F12) hoặc cho toolbar của IDE
```


