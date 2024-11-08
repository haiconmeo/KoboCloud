# KoboCloud
Bộ script để đồng bộ hóa thiết bị đọc Kobo với các dịch vụ đám mây phổ biến. Có sẵn các font tiếng việt ở file cài đặt : 
nguồn từ repo https://github.com/lelinhtinh/kobo-tieng-viet

Các dịch vụ đám mây được hỗ trợ:

- Dropbox
- Google Drive
- NextCloud/OwnCloud
- pCloud
- Box

## <a name="installation"></a>Cài đặt

Tải xuống file `KoboRoot.tgz` mới nhất từ trang Phát hành (hoặc [liên kết trực tiếp này](https://github.com/fsantini/KoboCloud/releases/download/latest/KoboRoot.tgz)).

Chép nó vào thiết bị Kobo:

- Kết nối thiết bị Kobo và gắn kết nó (bạn sẽ có thể truy cập vào hệ thống file của Kobo)
- Sao chép file .tgz vào thư mục .kobo(1) trên thiết bị của bạn
- Ngắt kết nối và khởi động lại thiết bị Kobo

(1) Đây là thư mục ẩn, bạn cần bật chế độ hiển thị file ẩn

**Lưu ý cho người dùng Mac/Safari:** Safari tự động giải nén `KoboRoot.tgz` thành `KoboRoot.tar` sau khi tải xuống. Hãy chắc chắn rằng bạn chuyển file `.tgz` vào Kobo, **không phải** file `.tar`. Sử dụng trình duyệt khác để tải gói về hoặc đóng gói lại (sử dụng `gzip`) trước khi chuyển.

## Cấu hình

Sau khi cài đặt:

- Cắm Kobo lại vào máy tính
- Mở file cấu hình nằm trong `.add/kobocloud/kobocloudrc`
- Thêm các liên kết đến dịch vụ đám mây (mỗi dòng một liên kết)

Ví dụ cấu hình:

```
# Các dòng bắt đầu bằng '#' sẽ bị bỏ qua
# Google Drive:
https://drive.google.com/drive/folders/<ID>?usp=sharing
# Dropbox:
https://www.dropbox.com/sh/pgSHORTENED
REMOVE_DELETED
```

Một số lưu ý quan trọng:
- Đảm bảo không có **khoảng trắng** trước hoặc sau liên kết trên dòng
- **Không hỗ trợ thư mục con** tại thời điểm này, các sách của bạn phải nằm trong cùng một thư mục mà bạn chia sẻ
- **Khởi động lại Kobo** sau khi thay đổi bất kỳ thiết lập nào trong kobocloudrc để áp dụng

### Thư mục công khai Dropbox

Do thay đổi trên trang web Dropbox, phương pháp dùng thư mục công khai không còn hoạt động.

### Thư mục riêng tư Dropbox

Phương pháp này sẽ tạo một thư mục `/Applications/Kobo Cloud Sync` trong Dropbox của bạn và đồng bộ với nó.

- Mở [liên kết này](https://www.dropbox.com/oauth2/authorize?response_type=code&token_access_type=offline&client_id=5oyw72cfwcp352f&code_challenge_method=plain&code_challenge=0000000000000000000000000000000000000000000&redirect_uri=https://louisabraham.github.io/KoboCloud/)
- Dán lệnh vào terminal
- Sao chép dòng bắt đầu với `DropboxApp:` từ terminal của bạn
- Thêm nó vào file `kobocloudrc`

### Google Drive

- Sử dụng tùy chọn "chia sẻ liên kết" trên thư mục Google Drive
- Chọn tùy chọn "ai có liên kết đều có thể xem."
- Sao chép và dán liên kết vào file kobocloudrc

Hỗ trợ thư mục con cho Google Drive.
**Lưu ý**: Các thư mục có nhiều file có thể không hoạt động.

### NextCloud (OwnCloud)

Để thêm một liên kết NextCloud (OwnCloud):

- Mở trang NextCloud trong trình duyệt
- Chọn thư mục bạn muốn chia sẻ
- Nhấp vào "Chia sẻ" và chọn "Chia sẻ bằng liên kết"
- Sao chép liên kết vào file kobocloudrc

Lưu ý rằng bạn cần phiên bản NextCloud (OwnCloud) mới. 
Hỗ trợ thư mục con cho NextCloud (OwnCloud).

**Lưu ý**: Webdav cho thư mục công khai cần được bật, xem thêm tại: https://docs.nextcloud.com/server/20/user_manual/en/files/access_webdav.html#accessing-public-shares-over-webdav. Bạn cũng cần đảm bảo rằng 'dav.propfind.depth_infinity' được đặt thành 'true'. Xem thêm tại: https://doc.owncloud.com/server/next/admin_manual/configuration/server/config_sample_php_parameters.html#enable-propfind-depth-infinity-requests.

### pCloud

- Thêm liên kết công khai đến thư mục chứa vào file kobocloudrc.

~~Các file được thêm vào thư mục con trong thư mục *công khai* của pCloud cũng được hỗ trợ.~~
Do phương pháp tải xuống khác nhau cho pCloud (các liên kết chia sẻ mới có định dạng khác), chỉ hỗ trợ thư mục con trên các thư mục chia sẻ cũ. Không áp dụng cho các thư mục chia sẻ mới.

### Box

- Trên thư mục Box, nhấp "Tạo liên kết" trong thanh bên và bật "Chia sẻ liên kết"
- Chọn các tùy chọn "Người có liên kết" và "có thể xem và tải xuống"
- Sao chép và dán liên kết vào file kobocloudrc

Lưu ý rằng, mặc dù script hỗ trợ thư mục có danh sách file có nhiều trang, danh sách nhiều trang có thể không hoạt động.

### Đồng bộ với máy chủ từ xa
Để xóa file khỏi thư viện khi chúng không còn trên máy chủ từ xa:

- Chỉnh sửa file kobocloudrc để chứa cụm từ `REMOVE_DELETED` trên một dòng riêng biệt (viết hoa hoàn toàn, không có khoảng trống trước hoặc sau).
- Khởi động lại Kobo của bạn.

Lần tiếp theo khi Kobo kết nối Internet, nó sẽ xóa bất kỳ file nào (không bao gồm thư mục) không có trên máy chủ từ xa.

## Sử dụng

Các file mới sẽ được tải xuống khi Kobo kết nối Internet để đồng bộ. Đôi khi cần vài phút sau quá trình đồng bộ để thiết bị nhận dạng và nhập nội dung mới tải xuống.

## Gỡ cài đặt

Để gỡ cài đặt KoboCloud đúng cách:

- Chỉnh sửa file kobocloudrc để chứa từ `UNINSTALL` trên một dòng riêng biệt (viết hoa hoàn toàn, không có khoảng trống trước hoặc sau).
- Khởi động lại Kobo của bạn.

Lần tiếp theo khi Kobo kết nối Internet, chương trình sẽ tự xóa.

Lưu ý: Thư mục .add/kobocloud sẽ không bị xóa. Sau khi kết nối thiết bị với máy tính, bạn nên chuyển các file từ thư mục Library để không mất nội dung, và xóa thư mục kobocloud theo cách thủ công.

## Cài đặt từ mã nguồn

Để cài đặt KoboCloud từ mã nguồn:

- Tải xuống kho lưu trữ này
- Biên dịch mã thành định dạng nén (hướng dẫn dưới đây)
- Thực hiện theo hướng dẫn [cài đặt](#installation)

### Biên dịch

- Di chuyển đến thư mục gốc của dự án
- Mở file cấu hình nằm trong `src/usr/local/kobocloud/kobocloudrc.tmpl`
- Thêm các liên kết đến dịch vụ đám mây (xem ví dụ cấu hình bên trên)
- Chạy `sh ./makeKoboRoot.sh`

Lệnh cuối cùng sẽ tạo ra file `KoboRoot.tgz`.

Giờ bạn có thể làm theo hướng dẫn [cài đặt](#installation).

## Khắc phục sự cố

KoboCloud lưu nhật ký của mỗi phiên trong file .add/kobocloud/get.log. Nếu có sự cố, thông tin hữu ích có thể tìm thấy ở đó. Vui lòng gửi bản sao file này khi báo cáo lỗi.

