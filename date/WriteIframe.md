Đoạn mã JavaScript giúp tôi viết trên đối tượng ifrane, dựa trên phương pháp write của document.

Đầu tiên tôi khởi tạo một iframe bằng phương pháp createElement của document mà bạn có thể thấy, kế tiếp tôi dùng đối tượng body với phương pháp appendChild để chèn đối tượng iframe trên body của html và kế tiếp tôi nhập đối tượng contentDocument của iframe và dùng phương pháp write của đối tượng document để viết, nhưng niếu bạn không mở một đối tượng contentWindo từ phương pháp open nó có ném lỗi. Đây là đoạn mã rất tuyệt để viết các trang tạm và thêm các đoạn mã.

&lt;script&gt;

var doc = document; 
var iframe = doc.createElement("iframe");
iframe.width="320";
iframe.height="480"; 

/* add an iframe element to the document */ 
doc.body.appendChild(iframe); 
    
/* Add object in iframe elements */    
var iwin = iframe.contentWindow;
var idoc = iframe.contentDocument; 
  
idoc.open();
idoc.close();    

/* Write method in iframe document */     
idoc.write("Game Play"); // uotput

&lt;/script&gt;
