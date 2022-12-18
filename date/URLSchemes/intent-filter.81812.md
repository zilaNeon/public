# Xác định URL tùy chỉnh

Để cho phép liên kết sâu tới nội dung trong Android, chúng tôi cần thêm các bộ lọc ý định để phản hồi các yêu cầu hành động từ các ứng dụng khác. Bộ lọc ý định được chỉ định trong bảng kê khai app]/AndroidManifest.xml. Đây là bảng kê khai đã sửa đổi với bộ lọc ý định được thêm vào hoạt động chính:

> Lưu ý nội dung nhằm một để JavaScript chuyển khai 

`&lt;activity android:name=".MainActivity" android:label="@string/app_name" android:configChanges="keyboard|keyboardHidden|orientation|screenSize"&gt;
  &lt;intent-filter&gt;
    &lt;action android:name="android.intent.action.MAIN" /&gt;
    &lt;category android:name="android.intent.category.LAUNCHER" /&gt;
  &lt;/intent-filter&gt;
  &lt;intent-filter android:label="filter_react_native"&gt;
    &lt;action android:name="android.intent.action.VIEW" /&gt;
    &lt;category android:name="android.intent.category.DEFAULT" /&gt;
    &lt;category android:name="android.intent.category.BROWSABLE" /&gt;
    &lt;data android:scheme="deeplink" android:host="home" /&gt;
  &lt;/intent-filter&gt;
/activity&gt;`

Thẻ &lt;data&gt; chỉ định lược đồ URL giải quyết hoạt động mà bộ lọc ý định đã được thêm vào. Trong ví dụ này, bộ lọc ý định chấp nhận các URI bắt đầu bằng deeplink://home. Có thể chỉ định nhiều lược đồ URI bằng cách sử dụng các thẻ <data> bổ sung. Đó là phần gốc của mọi thứ, tất cả những gì còn lại phải làm là triển khai ở phía JavaScript.
