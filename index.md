# 1) Giới thiệu webpack
## Wepback là gì?
+ Webpack là một module bundler để quản lí code front-end của bạn (bao gồm HTML, CSS, JS,..). Webpack đơn giản hóa các workflow 	 bằng việc xây dựng một cách nhanh chóng một đồ thị tham chiếu (dependency graph) trong ứng dụng của bạn và sắp xếp nó một các   	 chính xác.
	
**Tại sao phải sử dụng webpakck**


# 2) Cài đặt
  Hãy chắc chắn rằng bạn có một vài thứ:
  + nodejs: 
    -	Bạn có thể download và cài đặt trực tiếp tại link sau tùy phiên bản hệ điều hành bạn đang dùng: https://nodejs.org/en/download/ 
    -	Khi bạn cài đặt node máy của bạn sẽ được cài luôn npm (viết tắt của node package manager). Đây là kho lưu trữ cho việc xuất bản         các dự án mã nguồn mở của nodejs, cũng là lệnh command-line giúp tương tác, quản lí, hỗ trợ trong việc cài đặt các package. Sau         này chúng ta sẽ dùng lệnh này để cài đặt webpack cũng như các package liên quan.
    -	Sau khi cài đặt, hãy thử lệnh sau trên command-line của bạn: node –v để kiểm tra phiên bản của node và npm –v để kiểm tra phiên         bản của npm. Nếu cả hai đều cho kết quả mà không báo lỗi nghĩa là bạn cài thành công.
  + webpack:
    -	Lúc này, khi đã cài đặt node và npm, bạn đã có thể cài đặt webpack trên command-line của mình bằng lệnh: npm install –g webpack.         Cờ lệnh –g giúp cho webpack có thể chạy global bất kì đâu trên máy của bạn. Thử lệnh webpack trên command-line. Nếu hệ thống             trả về tên phiên bản thì bạn đã cài đặt thành công.
  + package.json:
    -	Đảm bảo máy bạn có file package.json để tiện cho việc cấu hình cho webpack sau này khi chúng ta cài đặt thêm các loader, pluggin         và những tiện ích khác. Phần này sẽ được giới thiệu bên dưới. Nếu máy bạn không có file package.json bạn có thể mở command-line 	 và gõ lệnh: npm init. Cứ tuân theo hướng dẫn trên command-line và tạo một file package.json.

  
# 3) Sử dụng
  **Webpack khi không có file config: **
  Tạo một folder có cấu trúc như sau:
	
_hello.js_
Thêm dòng lệnh sau vào file hello.js của bạn: 
`setTimeout(()=> alert("Hello there from HELLO.js"),3000);`
Dòng lệnh trên có tác dụng hiện một text box có dòng chữ “Hello there from HELLO.js” trên trình duyệt sau của bạn sau 3 giây.

_main.js_
Thêm 2 dòng lệnh sau vào file main.js của bạn:
`var sub = require('./hello.js');
setTimeout(()=> alert("Hello there from MAIN.js"),300);`
Dòng đầu tiên sẽ gọi đến file hello.js và dòng thứ hai sẽ có tác dụng hiện một text box có dòng chữ “Hello there from MAIN.js” trên trình duyệt của bạn sau 0.3 giây. 
Về cơ bản, bạn không thể gọi một file .js này từ một file .js khác, tuy nhiên webpack cho phép bạn làm điều này. Điều này giúp bạn có thể tùy biến gọi đến nhiều file .js khác phục vụ nhu cầu chức năng mà không phải là gom tất cả các file .js kể cả các file .js không cần thiết vào. Điều này cũng giúp bạn dễ dàng quản lí các file .js nếu bạn muốn gom chúng lại. 
Tuy nhiên, nếu không thực hiện require thì vẫn có cách khác để bạn gộp các file .js này thành một. Cách này sẽ được hướng dẫn bên dưới.

_index.html_
Chúng ta cần một view để xem những gì chúng ta làm bên dưới. Bạn thêm vào file index.html của mình các dòng lệnh sau:
`<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack</title>
    <script type="text/javascript" src="./bundle.js">
    </script>
</head>
<body>
    <h1>Hi, my name is Hien</h1>
</body>
</html>`
Ở dòng thứ 6 của đoạn code trên, trong thẻ <script> bạn thấy có một lời gọi đến file bundle.js. Vậy file này ở đâu ra? Mở command-line của bạn lên (bạn cần nhớ là đứng ở thư mục gốc chứa các file này) và gõ lệnh: 
webpack main.js bundle.js

Quay lại trường hợp bạn không thực hiện require file hello.js trong file main.js thì bạn có thể thực hiện theo lệnh sau, kết quả sẽ không thay đổi.
webpack hello.js main.js bundle.js
Nếu bạn có nhiều hơn một file hello.js, ví dụ như hello1.js, hello2.js, hello3.js,… bạn có thể require chúng trong file main.js rồi thực hiện chạy lệnh command-line thứ nhất hoặc liệt kê chúng như lệnh command-line thứ hai.
Sau khi thực hiện lệnh trên command-line. Nó sẽ trả về cho bạn một số thứ trông gần giống như thế này.

Sau đó, kiểm tra trong thư mục webpack-without-file-config, một file có tên bundle.js sẽ được tạo ra, mở file này lên kiểm tra, bạn sẽ thấy có một số đoạn code khác bao quanh code ban đầu của bạn và bạn sẽ có cảm giác giống như hai file main.js và hello.js được nhập lại thành một file.
Sau đó mở trình duyệt của bạn lên và kiểm tra. Hai text box sẽ hiện lên lần lượt. 
Đây là cách sử dụng webpack khi không sử dụng file webpack.config.js. Tuy nhiên chúng có một số bất tiện. Thứ nhất, mỗi lần có một sự thay đổi nào, dù là nhỏ nhất, bạn cũng phải chạy lại lệnh trên command-line. Thứ hai, việc này sẽ trở nên cực kì phức tạp khi bạn tích hợp các module khác của JS hay CSS,… do đó chúng ta cần một cách dùng khác giúp giải quyết vấn đề này, đó là dùng file webpack.config.js để giúp ta chạy các lệnh đơn giản hơn. 

  ## Webpack khi có file config
  Tạo một folder có cấu trúc như sau (có thêm file webpack.config.js và file style.css)
  Tác dụng của file webpack.config.js:
Như đã nói ở trên, file webpack.config.js giúp chúng ta dễ dàng quản lí các module, pluggin,… mà không phải gõ lại những lệnh quá dài dòng trên command-line, đồng thời có một số chế độ giúp tự compile và cập nhật lại các file khi có thay đổi.
Cấu trúc của một file webpack.config.js:
Trước khi tạo file cấu hình, bạn cần hiểu rằng, tùy chọn dòng lệnh của wepack lấy theo hai tham số:
+ entry: được hiểu là đầu vào.
+ output: được hiểu là đầu ra.
module.exports = {
    entry: './main.js',
    output: {
        filename: './bundle.js'
    }
  }
Vì bạn cài đặt webpack bằng lệnh trên command-line nên câu lệnh ở đây để thực hiện khai báo các cấu hình bên trong là module.exports. Trong ví dụ trên, file entry là main.js và sẽ cho ra một file output là bundle.js ở cùng thư mục. Bạn có thể tùy chỉnh thư mục lưu trữ bằng các tùy chọn khác như tùy chỉnh output.path và rất nhiều tùy chọn khác ở trang này: https://webpack.github.io/docs/configuration.html
Tiếp đến chúng ta thực hiện lệnh trên command-line, thay vì liệt kê các file như câu lệnh phía trên, bây giờ chỉ cần gõ webpack thì chúng ta sẽ có kết quả tương  tự. 

  ## Watch mode
  ## Tối ưu hóa kết quả đầu ra
  ## Loader
  ## Webpack dev server
  ## Pluggin




### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
      
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/UDPT-2017/seminar-webpack-1412193-1412169.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
