# REST API

## Người thực hiện: Mai Thái Sơn

## Chức vụ: Thực tập sinh

## Người yêu cầu: Nguyễn An Hưng

------------

### Các công việc tìm hiểu:

1. API là gì?
   1. Định nghĩa
   2. Tại sao chúng ta lại sử dụng API?
2. RestFul API là gì?
   1. Định nghĩa
   2. Rest là gì?
3. Các công cụ để làm việc với API
4. Viết 1 API đơn giản?

-----------------------

### Chi tiết

1. **API là gì?**

   1. **Định nghĩa**

      API là viết tắt của từ "Application Programming interface" có nghĩa là giao diện lập trình ứng dụng. Nó là  một tập hợp các giao ước, quy tắc mà một ứng dụng hay là hệ thống phải tuân theo nếu như muốn giao tiếp với hệ thống hay ứng dụng khác. Hay nói cách khác, API là  giao diện dùng để giao tiếp giữa hai phần mềm khác nhau, phần mềm này có thể gửi các yêu cầu của mình tới các phần mềm khác để thực hiện trên chúng hoặc ngược lại.

   2. **Tại sao chúng ta lại sử dụng API?**

      Vì hiện nay, mọi phần mềm ứng dụng cần tận dụng các lợi thế của nhau.

      Ví dụ: Để một chương trình trò chơi hoạt động trên một chiếc máy tính, chúng sẽ phải thực hiện các công việc như "lưu trữ trên ổ cứng, khi người dùng mở thì phải ghi lên RAM, hiển thị lên màn hình, Khi người dùng tắt đi thì phải giải phóng bộ nhớ trên RAM, ghi lại trạng thái trò chơi hay SAVE lại vào ổ cứng để dùng cho lần sau chơi tiếp". Nếu một lập trình viên viết nên trò chơi đó, anh ta phải nghiên cứu toàn bộ những thứ trên. Và tất nhiên, công việc này hoàn toàn bất khả thi. Thay vì phải khổ công như vậy, anh ta chỉ cần tương tác hay là gọi tới các API của hệ điều hành và nhờ chúng thực thi các công việc còn lại, công việc của người coder đó chỉ đơn giản là dùng các ngôn ngữ lập trình khác để viết nên trò chơi đó thôi.

2. **Restful API là gì?**

    1. **Định nghĩa**

       Restful API là các API được viết theo cấu trúc REST

    2. **Rest là gì?**

       

3. **Các công cụ để làm việc với API**

   Trong bài viết lần này, chúng ta sẽ viết Restful API bằng ngôn ngữ lập trình PHP trên **PHP storm** và sử dụng công cụ Test API **Postman.**

   [Link tải Postman](https://www.getpostman.com/downloads/)

4. **Viết 1 API đơn giản**

   Bước đầu tiên, tạo 1 cơ sở dữ liệu rest_api trên phpmyadmin và tạo một bảng user có chứa các trường sau:

   * id int primary key auto_increament
   * name varchar(30)
   * email varchar(30)
   * status bool (giới tính)

   Kế tiếp, ta sẽ tạo 1 folder REST trong htdocs và tổ chức cấu trúc thư mục như sau:

   ![](C:\Users\ADMIN\Pictures\Restful API\Structure.PNG)

   Trong thư mục config có chứa file **database.php** dùng để kết nối đến cơ sở dữ liệu

   Folder User có file **user.php** chứa các câu lệnh tương tác với csdl 

   tệp User_product dùng để kết nối tới người dùng

   Trong file **database.php** ta sẽ viết các câu lệnh sau:

   <pre>
       <?php
   class Database
   {
       private $host = "localhost";
       private $db_name = "rest_api";
       private $username = "root";
       private $password = "";
       private $conn;
       public function getConnection()
       {
           $this->conn = null;
           try
           {
               $this->conn = new PDO("mysql:host=".$this->host.";dbname=".$this->db_name,$this->username,$this->password);
               $this->conn->exec("set names utf8");
           }catch (PDOException $e)
           {
               echo "Error Connection: " . $e->getMessage();
           }
           return $this->conn;
       }
   }
   </pre>

   

   