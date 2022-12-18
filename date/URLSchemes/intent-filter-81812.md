Làm cách nào để mở một loại tệp nhất định trong hoạt động của Android?

> Lưu ý loại tài liệu này để xem bộ lọc ý định 

### Điều này sẽ ném lỗi mã

Cần sử dụng mimeType, host và pathPattern.

> &lt;activity
    android:name=".JsonActivity"
    android:label="Json"&gt;
    &lt;intent-filter&gt;
        &lt;action android:name="android.intent.action.VIEW" /&gt;
        &lt;category android:name="android.intent.category.DEFAULT" /&gt;
        &lt;category android:name="android.intent.category.BROWSABLE" /&gt;
        &lt;data android:scheme="http" /&gt;
        &lt;data android:scheme="https" /&gt;
        &lt;data android:scheme="content" /&gt;
        &lt;data android:scheme="file" /&gt;
        &lt;data android:host="*" /&gt;
        &lt;data android:pathPattern=".*\\.json" /&gt;
    &lt;/intent-filter&gt;
&lt;/activity&gt; 

**Xử lý với mimetypes, trong đó hậu tố không liên quan:**

> &lt;intent-filter&gt;
    &lt;action android:name="android.intent.action.VIEW" /&gt;
    &lt;category android:name="android.intent.category.BROWSABLE" /&gt;
    &lt;category android:name="android.intent.category.DEFAULT" /&gt;
    &lt;data android:scheme="http" /&gt;
    &lt;data android:host="*" /&gt;
    &lt;data android:mimeType="application/json" /&gt;
  &lt;/intent-filter&gt;

**Xử lý ý định từ ứng dụng trình duyệt tệp:**

> &lt;intent-filter&gt;
    &lt;action android:name="android.intent.action.VIEW" /&gt;
    &lt;category android:name="android.intent.category.DEFAULT" /&gt;
    &lt;data android:scheme="file" /&gt; 
    &lt;data android:host="*" /&gt;
    &lt;data android:pathPattern=".*\\.json" /&gt;
  &lt;/intent-filter&gt;

