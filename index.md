# 1) Giới thiệu webpack
**Wepback là gì?**
Webpack là một module bundler để quản lí code front-end của bạn (bao gồm HTML, CSS, JS,..). Webpack đơn giản hóa các workflow bằng       việc xây dựng một cách nhanh chóng một đồ thị tham chiếu (dependency graph) trong ứng dụng của bạn và sắp xếp nó một cách chính xác.

**Tại sao phải sử dụng webpakck**
+ Có rất nhiều lợi ích khi sử dụng webpack:
    -	Webpack giúp  bạn dễ dàng chia tách code của bạn thành nhiều phần cũng như là gộp chúng lại, điều này giúp bạn dễ quản lí  chúng 	 hơn.
    -	Khả năng tích hợp 3rd-party library như module, giúp bạn load những thứ bạn muốn khi bạn thật sự cần chúng.
    -	Giúp biên dịch các loại file khác nhau thành file .js.
    -   Có webpack-dev-server để chạy các gói bundle ngay lập tức.


# 2) Cài đặt
  Hãy chắc chắn rằng bạn có một vài thứ:
  + nodejs: 
    -	Bạn có thể download và cài đặt trực tiếp tại link sau tùy phiên bản hệ điều hành bạn đang dùng: https://nodejs.org/en/download/ 
    -	Khi bạn cài đặt node máy của bạn sẽ được cài luôn npm (viết tắt của node package manager). Đây là kho lưu trữ cho việc xuất bản         các dự án mã nguồn mở của nodejs, cũng là lệnh command-line giúp tương tác, quản lí, hỗ trợ trong việc cài đặt các package. Sau         này chúng ta sẽ dùng lệnh này để cài đặt webpack cũng như các package liên quan.
    -	Sau khi cài đặt, hãy thử lệnh sau trên command-line của bạn: node –v để kiểm tra phiên bản của node và npm –v để kiểm tra phiên         bản của npm. Nếu cả hai đều cho kết quả mà không báo lỗi nghĩa là bạn cài thành công.
  + webpack:
    -	Lúc này, khi đã cài đặt node và npm, bạn đã có thể cài đặt webpack trên command-line của mình bằng lệnh: npm install –g webpack.         Cờ lệnh –g giúp cho webpack có thể chạy global bất kì đâu trên máy của bạn. Thử lệnh webpack trên command-line. Nếu hệ thống             trả về tên phiên bản thì bạn đã cài đặt thành công.
  + package.json:
    -	Đảm bảo máy bạn có file package.json để tiện cho việc cấu hình cho webpack sau này khi chúng ta cài đặt thêm các loader, pluggin         và những tiện ích khác. Phần này sẽ được giới thiệu bên dưới. Nếu máy bạn không có file package.json bạn có thể mở command-line và       gõ lệnh: npm init. Cứ tuân theo hướng dẫn trên command-line và tạo một file package.json.

  
# 3) Sử dụng
  **Webpack khi không có file config: **
  	Tạo một folder có cấu trúc như sau:
	
	hello.js 
	Thêm dòng lệnh sau vào file hello.js của bạn: 
	setTimeout(()=> alert("Hello there from HELLO.js"),3000);
	Dòng lệnh trên có tác dụng hiện một text box có dòng chữ “Hello there from HELLO.js” trên trình duyệt sau của bạn sau 3 giây.

  ## Webpack khi có file config
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
