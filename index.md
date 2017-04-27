# 1) Giới thiệu webpack
## a)Wepback là gì?
Webpack là một module bundler để quản lí code front-end của bạn (bao gồm HTML, CSS, JS,..). Webpack đơn giản hóa các workflow 	 bằng việc xây dựng một cách nhanh chóng một đồ thị tham chiếu (dependency graph) trong ứng dụng của bạn và sắp xếp nó một các   	 chính xác.
	
## b)Tại sao phải sử dụng webpakck
Có rất nhiều lợi ích khi bạn sử dụng webpack:
  -	Webpack giúp  bạn dễ dàng chia tách code của bạn thành nhiều phần cũng như là gộp chúng lại, điều này giúp bạn dễ quản lí  chúng hơn.
  -	Khả năng tích hợp 3rd-party library như module, giúp bạn load những thứ bạn muốn khi bạn thật sự cần chúng.
  -	Giúp biên dịch các loại file khác nhau thành file .js.
  -	Có webpack-dev-server để chạy các gói bundle ngay lập tức.
  -	Phù hợp với các dự án lớn về web.
Bên cạnh những lợi ích trên, thì còn nhiều lợi ích khác mà khi sử dụng bạn sẽ cảm nhận rõ hơn về chúng. 


# 2) Cài đặt
  Hãy chắc chắn rằng bạn có một vài thứ:
  + nodejs: 
    -	Bạn có thể download và cài đặt trực tiếp tại link sau tùy phiên bản hệ điều hành bạn đang dùng: https://nodejs.org/en/download/
    -	Khi bạn cài đặt node máy của bạn sẽ được cài luôn `npm` (viết tắt của node package manager). Đây là kho lưu trữ cho việc xuất bản         các dự án mã nguồn mở của nodejs, cũng là lệnh command-line giúp tương tác, quản lí, hỗ trợ trong việc cài đặt các package. Sau         này chúng ta sẽ dùng lệnh này để cài đặt webpack cũng như các package liên quan.
    -	Sau khi cài đặt, hãy thử lệnh sau trên command-line của bạn: `node –v` để kiểm tra phiên bản của node và `npm –v` để kiểm tra 		phiên bản của npm. Nếu cả hai đều cho kết quả mà không báo lỗi nghĩa là bạn cài thành công.
  + webpack:
    -	Lúc này, khi đã cài đặt node và npm, bạn đã có thể cài đặt webpack trên command-line của mình bằng lệnh: `npm install –g 		webpack`. Cờ lệnh `–g` giúp cho webpack có thể chạy global bất kì đâu trên máy của bạn. Thử lệnh `webpack` trên command-line. 		Nếu hệ thống trả về tên phiên bản thì bạn đã cài đặt thành công.
  + package.json:
    -	Đảm bảo máy bạn có file package.json để tiện cho việc cấu hình cho webpack sau này khi chúng ta cài đặt thêm các loader, pluggin         và những tiện ích khác. Phần này sẽ được giới thiệu bên dưới. Nếu máy bạn không có file package.json bạn có thể mở command-line 	 và gõ lệnh: `npm init`. Cứ tuân theo hướng dẫn trên command-line và tạo một file package.json.

  
# 3) Sử dụng
## a) Webpack khi không có file config:
  Tạo một folder `webpack-without-file-config` gồm các file (`hello.js`, `main.js`, `index.js`)
  + _hello.js_
     - Thêm dòng lệnh sau vào file hello.js của bạn: 
    ```
    setTimeout(()=> alert("Hello there from HELLO.js"),3000);
    ```
     -  Dòng lệnh trên có tác dụng hiện một text box có dòng chữ “Hello there from HELLO.js” trên trình duyệt sau của bạn sau 3 giây.


  + _main.js_
    - Thêm 2 dòng lệnh sau vào file main.js của bạn:
    ```
    var sub = require('./hello.js');
    setTimeout(()=> alert("Hello there from MAIN.js"),300);
    ```
    - Dòng đầu tiên sẽ gọi đến file `hello.js` và dòng thứ hai sẽ có tác dụng hiện một text box có dòng chữ “Hello there from MAIN.js” 	  	trên trình duyệt của bạn sau 0.3 giây. 
    - Về cơ bản, bạn không thể gọi một file .js này từ một file .js khác, tuy nhiên webpack cho phép bạn làm điều này. Điều này giúp 	       bạn có thể tùy biến gọi đến nhiều file .js khác phục vụ nhu cầu chức năng mà không phải là gom tất cả các file .js kể cả các 	       file .js không cần thiết vào. Điều này cũng giúp bạn dễ dàng quản lí các file .js nếu bạn muốn gom chúng lại. 
    - Tuy nhiên, nếu không thực hiện require thì vẫn có cách khác để bạn gộp các file .js này thành một. Cách này sẽ được hướng dẫn 	 	bên dưới.


  + _index.html_
    - Chúng ta cần một view để xem những gì chúng ta làm bên dưới. Bạn thêm vào file index.html của mình các dòng lệnh sau:
```
<!DOCTYPE html>
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
</html>
```
   - Ở dòng thứ 6 của đoạn code trên, trong thẻ `<script>` bạn thấy có một lời gọi đến file `bundle.js`. Vậy file này ở đâu ra? Mở             command-line của bạn lên (bạn cần nhớ là đứng ở thư mục gốc chứa các file này) và gõ lệnh: 
     `webpack main.js bundle.js`
     
Quay lại trường hợp bạn không thực hiện require file `hello.js` trong file `main.js` thì bạn có thể thực hiện theo lệnh `webpack 	  hello.js main.js bundle.js`, kết quả sẽ không thay đổi.
 
Nếu bạn có nhiều hơn một file `hello.js`, ví dụ như `hello1.js`, `hello2.js`, `hello3.js`,… bạn có thể require chúng trong file         `main.js`rồi thực hiện chạy lệnh command-line thứ nhất hoặc liệt kê chúng như lệnh command-line thứ hai.

Sau khi thực hiện lệnh trên command-line. Nó sẽ trả về cho bạn một số thứ trông gần giống như thế này.
![https://github.com/UDPT-2017/seminar-webpack-1412193-1412169.github.io/blob/master/image/result.png]
    
Sau đó, kiểm tra trong thư mục `webpack-without-file-config`, một file có tên `bundle.js` sẽ được tạo ra, mở file này lên kiểm tra, bạn sẽ thấy có một số đoạn code khác bao quanh code ban đầu của bạn và bạn sẽ có cảm giác giống như hai file `main.js` và `hello.js` được nhập lại thành một file.

Sau đó mở trình duyệt của bạn lên và kiểm tra. Hai text box sẽ hiện lên lần lượt. 

Đây là cách sử dụng webpack khi không sử dụng file `webpack.config.js`. Tuy nhiên chúng có một số bất tiện. Thứ nhất, mỗi lần có một sự thay đổi nào, dù là nhỏ nhất, bạn cũng phải chạy lại lệnh trên command-line. Thứ hai, việc này sẽ trở nên cực kì phức tạp khi bạn tích hợp các module khác của JS hay CSS,… do đó chúng ta cần một cách dùng khác giúp giải quyết vấn đề này, đó là dùng file `webpack.config.js` để giúp ta chạy các lệnh đơn giản hơn. 

##  b) Webpack khi có file config:
Tạo một folder `webpack-with-file-config` gồm các file sau (webpack.config.js, hello.js, main.js, index.html, style.css) (có thêm 	 file webpack.config.js và file style.css)
    
**Tác dụng của file webpack.config.js:** 
Như đã nói ở trên, file `webpack.config.js` giúp chúng ta dễ dàng quản lí các module, pluggin,… mà không phải gõ lại những lệnh quá      dài dòng trên command-line, đồng thời có một số chế độ giúp tự compile và cập nhật lại các file khi có thay đổi.

**Cấu trúc của một file webpack.config.js:**
Trước khi tạo file cấu hình, bạn cần hiểu rằng, tùy chọn dòng lệnh của wepack lấy theo hai tham số:
+ `entry` được hiểu là đầu vào.
+ `output`: được hiểu là đầu ra.
```
module.exports = {
    entry: './main.js',
    output: {
        filename: './bundle.js'
    }
  }
  ```
- Vì bạn cài đặt webpack bằng lệnh trên command-line nên câu lệnh ở đây để thực hiện khai báo các cấu hình bên trong là `module.exports`. Trong ví dụ trên, file entry là `main.js` và sẽ cho ra một file output là `bundle.js` ở cùng thư mục. Bạn có thể tùy chỉnh thư mục lưu trữ bằng các tùy chọn khác như tùy chỉnh `output.path` và rất nhiều tùy chọn khác ở trang này: https://webpack.github.io/docs/configuration.html

Tiếp đến chúng ta thực hiện lệnh trên command-line, thay vì liệt kê các file như câu lệnh phía trên, bây giờ chỉ cần gõ `webpack` thì chúng ta sẽ có kết quả tương  tự. 

## c) Watch mode
Để tiện hơn, webpack cung cấp cho chúng ta một chế độ, giúp tự động compile lại khi chúng ta thực hiện các thay  đổi. Có 2 cách để bạn làm điều này:
* _Cách 1:_ chạy lệnh `webpack –watch` hoặc lệnh `webpack –w` trên command-line, bạn chạy lênh này càng sớm càng tốt, bạn sẽ đỡ tốn công gõ đi gõ lại lệnh webpack nhiều lần.

* _Cách 2:_ cấu hình trong file webpack.config.js, bật `watch` lên thành `true`.
```
module.exports = {
    entry: './main.js',
    output: {
        filename: './bundle.js'
    },
    watch: true,
  }
  ```
Bây giờ, bạn chỉ cần gõ lệnh `webpack` một lần duy nhất, cho tới khi bạn nhấn `Ctr+C` để thoát thì webpack sẽ tự compile mỗi lần bạn thực hiện thay đổi trên các file liên quan.

## d)Tối ưu hóa kết quả đầu ra
Webpack cung cấp một chế độ giúp tối ưu hóa code đầu ra của bạn. Nó sẽ xóa bỏ các khoảng trắng, dấu xuống dòng, các lệnh comment trên code,… để giúp file đầu ra nhẹ hơn.
Bạn có thể thực hiện bằng lệnh `webpack –p` trên command-line.

## e)Loader
Đây được xem là phần rất quan trọng. 

Vì webpack chỉ hiểu các file .js nên để có thể làm việc được với các file như .html hay .css chúng ta cần phải cài một số loader. Các loader này sẽ dạy cho webpack cách làm việc với các file không phải là file .js. 

Bản thân webpack không có sẵn các loader nhằm giúp cho webpack trở nên linh hoạt và ít cồng kềnh hơn. Vì vậy khi cần bất cứ loader nào chúng ta chỉ việc cài đặt chúng.

Quá trình tích hợp một loader vào webpack diễn ra theo 2 bước:

+ _Bước 1:_ Tải loader đó về máy theo lệnh `npm install –save-dev <tên_loader>` . Cờ lệnh `–save-dev` giúp lưu các module được tải về dưới dạng các dependencies trong file `package.json` một cách tự động. 

+ _Bước 2:_ Thực hiện cấu hình trong file `webpack.config.js`

_Lưu ý:_ các loader được thực thi theo thứ  tự trừ phải sáng trái trong câu lệnh.

**Loading Javascript:**

Để load được file Javascript, bạn cần một loader có tên là babel-loader. 
- Cài đặt: `npm install –save-dev babel-core babel-loader babel-preset-es2015`

Babel là một trình biên dịch code Javascript. Về cơ bản bạn có thể dùng webpack và `babel-loader` để giúp chuyển code ES2015 thành 	ES5. Để cài đặt được `babel-loader`, bạn cần cài `babel-core`, sau đó là cài `babel-preset-es2015` (preset cho toàn bộ pluggin của ES2015) để nói cho webpack biết, những preset nào sẽ được sử dụng. 

- Thực hiện cấu hình trong file `webpack.config.js`

```
module.exports = {
    entry: './main.js',
    output: {
        filename: './bundle.js'
    },
    watch: true,

    module: {
        loaders: [
            {
                test: /\.js6$/,
                exclude: /node_modules/,
                loader: 'babel-loader',
                query: {
                    presets: ['es2015']
                }
            },
        ],
      }
}
```
Giải thích đoạn code trong file webpack.config.js:
+ `test`: một đoạn regular expression được viết để kiểm tra loại file nào được chạy qua loader này. Trong trường hợp này, nó cho phép tất cả các file có đuôi .js6 chạy qua. 
+ `exclude`: cho biết file nào nên được bỏ qua. Trong trường hợp này, loader sẽ bỏ qua các file js6 nằm trong thư mục node_modules.
+ `loader`: tên loader của bạn. Trong trường hợp này đó là babel-loader.
+ `query`: danh sách các tùy chọn của bạn. Trong trường hợp này, đó là thông báo bộ preset es2015 sẽ được sử dụng.

Sau khi đã cài đặt babel và các loader liên quan, giờ thì thử viết một ít code bằng ES6 sau đó thực hiện biên dịch nó bằng babel loader

**Loading CSS:**
- Cài đặt: `npm install –save-dev css-loader style-loader`

Để load được file CSS, webpack cần 2 loader:  `css-loader` và `style-loader`, `css-loader` giúp load file CSS và `style-loader` giúp đưa 	các định dạng CSS vào trình duyệt. 

- Cấu hình trong file `webpack.config.js`
```
module.exports = {
    entry: './main.js',
    output: {
        filename: './bundle.js'
    },
    watch: true,

    module: {
        loaders: [
            {
                test: /\.js6$/,
                exclude: /node_modules/,
                loader: 'babel-loader',
                query: {
                    presets: ['es2015']
                }
            },
        ],

        loaders: [
            {
                test: /\.css$/,
                exclude: /node_modules/,
                loader: 'style-loader!css-loader'
            }
        ],
    }
};
```

Như lúc nãy đã đề cập, loader sẽ thực thi theo thứ tự từ phải sang trái. Trong trường hợp này, css-loader sẽ thực hiện trước style-loader.

+ _style.css_
- Hãy thêm vào file style.css của bạn dòng lệnh sau:
```
h1 {	
    color: green;
}
```
Dòng lệnh này giúp dòng chữ trong tag `<h1>` chuyển sang màu xanh lá. 

+ _main.js_

Thêm vào file main.js của bạn dòng lệnh require file `style.css`
```
var sub = require('./hello.js');
var sub = require('./style.css');
setTimeout(() => alert(`Hello there from MAIN`), 300);
```
Sau đó chuyển sang command-line và gõ lệnh `webpack`, mở trình duyệt và theo dõi sự thay đổi.

## Webpack dev server
Webpack có một server được gọi là `webpack-dev-server`

Từ command-line bạn có thể cài đặt `webpack-dev-server` thông qua lệnh sau: `npm install –g  webpack-dev-server`

Khi bạn dùng watch-mode của webpack, webpack sẽ tự động compile, tuy nhiên bạn phải tự refresh lại trình duyệt của mình để hiển 	thị kết quả. Còn với `webpack-dev-server`, tất cả mọi thứ sẽ được diễn ra một cách tự động, nghĩa là bạn không cần phải refresh 	trình duyệt nữa. Trình duyệt sẽ hiển thị những thay đổi nếu bạn thay đổi những thứ liên quan đến hiển thị.

Mở command-line lên và chạy lệnh `webpack-dev-server`. Sau đó đi đến trình duyệt và mở: http://localhost:8080/webpack-dev-		server/. Hiển nhiên bạn cũng có thể cấu hình để webpack-dev-server có thể mở trên port khác.

+ _style.css_
Vào file style.css của bạn đổi như sau:
```
h1 {
    color: red;
}
```
Giờ thì xem trên trình duyệt của bạn, dòng chữ sẽ chuyển sang màu đỏ.

## Pluggin
Phần cấu hình mở rộng được hỗ trợ cho tool webpack, hỗ trợ và bổ sung việc ánh xạ code mà các bạn vừa tạo ra ghép thành trang hoành chỉnh. Một số Plugin tiêu biểu: 
+ HTML webpack plugin 
+ Extract text wepack plugin 
**HTML webpack pluggin**
HTML webpack plugin dùng để làm gì? Mục đích của module này dùng để generate ra một file cuối của bạn mà file đó được xác định bằng cách cài đặt cấu hình. Nói cách đơn giản là nó generate ra 1 file trong bao gồm phần layout(chúng ta định nghĩa) và tích hợp sẵn thêm file .js mà webpack tạo ra HTML webpack plugin hỗ trợ việc truyền qua lại theo định dạng cú pháp (EJS).
+ Cài đặt: `npm install --save-dev html-webpack-pluggin`
```
new HtmlWebpackPluggin({
	title: "Form Dang Ki By Webpack",
	filename: "admin.html",
	template: "./source/hello.html",
	minify: false,
	hash: true
})
```
**Extract text wepack plugin**
Extract text webpack plugin dùng để làm gì? Nó giúp ách JS thành 2 phần JS riêng và CSS.
+ Cài đặt:
```
new ExtractTextPluggin({
	filename: "bundle.css",
	disable: false,
	allChunks: true,
})
```
**Webpack for NodeJS**
Tạo file `index.js` là file chứa cấu hình webpack. 
Khai báo webpack: `var webpack = require("webpack");`
Cách cấu hình webpack
```
webpack ({
	entry: "./source/js/JavaScript_1.js",
	output: {
		path: __dirname + "/public",
		filename: "js/bundle.js
		},
	module: {
		loaders: [{
			test: /\.css$/,
			exclude: /(node_modules)/,
			use: ExtractTextPluggin.extract({
				fallback: "style-loader",
				use: "css-loader",
			})
		}]
	},
	
	pluggins: [{
		new HtmlWebpackPluggin({
			title: "Form Dang Ki By Webpack",
			filename: "admin.html",
			template: "./source/hello.html",
			minify: false,
			hash: true
		})
		
		new ExtractTextPluggin({
			filename: "bundle.css",
			disable: false,
			allChunks: true,
		})
	}]
})
```



# Tài liệu tham khảo:
https://webpack.github.io/docs/configuration.html
https://scotch.io/tutorials/getting-started-with-webpack-module-bundling-magic
https://medium.com/@dabit3/beginner-s-guide-to-webpack-b1f1a3638460
https://webpack.github.io/docs/what-is-webpack.html


