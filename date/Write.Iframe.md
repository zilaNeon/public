Đoạn mã JavaScript giúp tôi viết trên đối tượng ifrane, dựa trên phương pháp write của document.

Đầu tiên tôi khởi tạo một iframe bằng phương pháp createElement của document mà bạn có thể thấy, kế tiếp tôi dùng đối tượng body với phương pháp appendChild để chèn đối tượng iframe trên body của html và kế tiếp tôi nhập đối tượng contentDocument của iframe và dùng phương pháp write của đối tượng document để viết, nhưng niếu bạn không mở một đối tượng contentWindo từ phương pháp open nó có ném lỗi. Đây là đoạn mã rất tuyệt để viết các trang tạm và thêm các đoạn mã.

&lt;script&gt;
<code>var doc = document; <br />
var iframe = doc.createElement("iframe"); <br /><br />
iframe.width="320";<br />
iframe.height="480"; <p/>

/* add an iframe element to the document */<br />
doc.body.appendChild(iframe); <br /><br />    
/* Add object in iframe elements */<p/>    

var iwin = iframe.contentWindow;<br />    
var idoc = iframe.contentDocument; <p/> 
  
idoc.open();<br />     
idoc.close(); <br />     

/* Write method in iframe document */<br />     
idoc.write("Game Play"); // uotput</code>
&lt;/script&gt;
