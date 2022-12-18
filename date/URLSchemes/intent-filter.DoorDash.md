# Giải quyết ý định web chung trên DoorDash

Để hướng dẫn Android sử dụng hoạt động cục bộ cho ý định này, hãy chèn bộ lọc ý định bên trong tệp kê khai Android như được hiển thị ở đây: 

> &lt;activity
    android:name="com.doordash.DeepLinkActivity"
    android:theme="@style/Theme.Consumer.DoorDash"&gt;
        &lt;intent-filter&gt;
            &lt;action android:name="android.intent.action.VIEW" /&gt;

            &lt;category android:name="android.intent.category.BROWSABLE" /&gt;
            &lt;category android:name="android.intent.category.DEFAULT" /&gt;

            &lt;data
                android:host="www.doordash.com"
                android:pathPrefix="/store"
                android:scheme="https" /&gt;

        &lt;/intent-filter&gt;
&lt;/activity&gt; 

Bằng cách này, Android có thể nhìn thấy và cố gắng sử dụng DeepLinkActivity vì Android có bộ lọc ý định với hành động của Intent.ACTION_VIEW và trường dữ liệu khớp với URL được yêu cầu. Điều này có thể hữu ích để thiết lập kết nối giữa liên kết HTTP và ứng dụng.

 Cho đến khi Android 12 ra đời, chúng tôi đã sử dụng kỹ thuật này tại DoorDash để điều hướng người dùng trực tiếp đến một cửa hàng cụ thể, giỏ hàng của người dùng, các tính năng tài khoản khác nhau và nhiều tính năng khác như được hiển thị.
