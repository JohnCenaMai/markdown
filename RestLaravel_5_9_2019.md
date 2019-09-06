# Restful API trên Laravel

## Người thực hiện: Mai Thái Sơn

## Chức vụ: Thực tập sinh

## Người yêu cầu: Nguyễn An Hưng

### Tìm hiểu

1. Laravel là gì?
   1. Cấu trúc thư mục
   2. Làm thế nào để download laravel?
   3. Tìm hiểu về Laravel Artisan
2. Viết Restful API trên laravel

----

### Chi tiết

1. **Laravel là gì?**

   Laravel là một open source, một framework dùng để xây dựn các ứng dụng, được thiết kế dựa trên mô hình MVC, đây là một mô hình được các lập trình viên ưu dùng nhất.

   1. **Cấu trúc thư mục**

      Sau đây ta sẽ giới thiệu 1 số thư mục chính trong laravel

      Các thư mục gốc

      | Directory | Description                                                  |
      | --------- | ------------------------------------------------------------ |
      | app       | chứa các code cơ nền tảng cho ứng dụng Laravel               |
      | bootstrap | chứa tất cả các kịch bản khởi động dành cho ứng dụng         |
      | config    | chứa tất cả files cấu hình dự án của bạn                     |
      | database  | chứa các file cơ sở dữ liệu như bảng,...                     |
      | public    | là nơi ứng dụng của chúng ta bắt đầu, chứa các file ảnh, css, javascripts |
      | resources | chứa tất cả files Sass, files ngôn ngữ, templates            |
      | routes    | chứa tất cả các tệp định nghĩa dành cho việc định tuyến như console.php, api.php, channels.php |
      | storage   | chứa files session, cache                                    |
      | test      | chứa các test cases dành cho chương trình                    |
      | vendor    | chứa các files độc lập composer                              |

      cấu trúc thư mục app

      | Directory  | Description                                                  |
      | ---------- | ------------------------------------------------------------ |
      | Console    | chứa các dòng lệnh artisan                                   |
      | Exceptions | chứa các xử lý ngoại lệ dành cho chương trình                |
      | Http       | nắm giữ các bộ lọc, yêu cầu, controllers khác nhau           |
      | Rules      | chứa các đối tượng khác nhau liên quan tới quy tắc điều chỉnh |

   2. **Làm thế nào để download laravel**

      Để download laravel, ngoài việc tìm các nguồn trên mạng nhưng tốt hết là nên cài đặt chúng với composer.

      Chúng ta nên tạo 1 thư mục trong folder htdocs của xampp. Bật cmd và đúng đường dẫn trong đó, chỉ cần đúng 2 câu lệnh để cài đặt:

      > composer global require "laravel/installer=~1.1"

      > composer create-project laravel/laravel <ten-thu-muc> <ten-phien-ban>

      Ở đây chúng ta sẽ cài bản với version mới nhât

      > composer create-project laravel/laravel cuoi 

      Nếu không điền tên phiên bản thì nó sẽ mặc định lấy phiên bản mới nhất.

      ![](C:\Users\ADMIN\Pictures\RestLaravel\structre.PNG)

      Kết quả sau khi tải xong, ta sẽ có được như thế này

   3. **Tìm hiểu về Laravel Artisan**

      Artisan là một giao diện dòng lệnh, được tích hợp cùng với laravel dùng để viết các câu lệnh nhằm hỗ trợ cho ứng dụng của mình. Nó có thể tự động một số các thao tác nhằm giúp đỡ các lập trình viên trong việc viết code. Để xem danh sách các lệnh sẵn có, chúng ta nháy chuột phải vào dòng màu xám rồi tìm đến **Open in terminal**.

      ![](C:\Users\ADMIN\Pictures\RestLaravel\right.PNG)

      Sau đó rồi gõ câu lệnh

      > php artisan list

      

2. **Viết Restful API trên laravel**

   Ở đây chúng ta sẽ dùng 1 bảng "Truyencuoi" có sẵn trong cơ sở dữ liệu

   ![](C:\Users\ADMIN\Pictures\RestLaravel\TruyenCuoiStructure.PNG)

   Mở thư mục .env, cấu hình để kết nối tới database

   ![](C:\Users\ADMIN\Pictures\RestLaravel\ConnectDatabase.PNG)
   
   Tạo model trong laravel, mở termial và viết câu lệnh artisan:
   
   > php artisan make:model Truyencuoi
   
   Mở folder App sẽ có 1 file Truyencuoi.php:
   
   ```php
   <?php
   
   namespace App;
   
   use Illuminate\Database\Eloquent\Model;
   
   class Truyencuoi extends Model
   {
       //
       
   }
   ```
   
   Ở trong Laravel mỗi model ứng với một bảng dữ liệu trong cơ sở dữ liệu và để khai báo model sử dụng bảng dữ liệu nào ta chỉ cần dòng lệnh:
   
   ```php
   public $table = 'truyencuoi';
   ```
   
   Khi ta chỉ muốn làm việc với một số cột cụ thể nào đó, ta dùng biến $filltable
   
   ```php
   protected $fillable = ['mt','service','is_sent','timeCreated'];
   ```
   
   Laravel cũng cung cấp cho chúng ta biến $timestamps, nếu không muốn sử dụng ta hoàn toàn có thể viết câu lệnh sau:
   
   ```php
   public $timestamps = false;
   ```
   
   Bây giờ sẽ tiếp tục tạo 1 controller
   
   > php artisan make:controller ApiController
   
   trong thư mục App/Http/Controllers sẽ xuất hiện tập tin ApiController.php
   
   Ở đây ta sẽ viết các hàm nhằm tương tác với cơ sở dữ liệu
   
   Các hàm dưới đây sẽ bao gồm thêm, đọc, sửa xóa.
   
   ```php
   <?php
   
   namespace App\Http\Controllers;
   
   use Illuminate\Http\Request;
   use App\Truyencuoi;
   
   class ApiController extends Controller
   {
       //insert into truyencuoi table
       public function create(Request $request)
       {
           $students = new Truyencuoi();
           $students->mt = $request->input('mt');
           $students->service = $request->input('service');
           $students->is_sent = $request->input('is_sent');
           $students->timeCreated = $request->input('timeCreated');
           $students->save();//save truyencuoi table
           return response()->json($students); //return json type
       }
       //select all from truyencuoi table
       public function show()
       {
           $students = Truyencuoi::all();
           return response()->json($students);
       }
       //select by id from truyencuoi table
       public function showbyid($id)
       {
           $students = Truyencuoi::find($id);
           return response()->json($students);
       }
       //update by id
       public function updatebyid(Request $request, $id)
       {
           $students = Truyencuoi::find($id);
           $students->mt = $request->input('mt');
           $students->service = $request->input('service');
           $students->is_sent = $request->input('is_sent');
           $students->timeCreated = $request->input('timeCreated');
   
           $students->save();
           return response()->json($students);
       }
       //delete by id
       public function deletebyid(Request $request,$id)
       {
           $students = Truyencuoi::find($id);
           $students->delete();
           return response()->json($students);
       }
   }
   ```
   
   Trong file routes/api.php ta sẽ viết các hàm nhằm điều hướng.
   
   ```php
   <?php
   
   use Illuminate\Http\Request;
   
   /*
   |--------------------------------------------------------------------------
   | API Routes
   |--------------------------------------------------------------------------
   |
   | Here is where you can register API routes for your application. These
   | routes are loaded by the RouteServiceProvider within a group which
   | is assigned the "api" middleware group. Enjoy building your API!
   |
   */
   
   Route::middleware('auth:api')->get('/user', function (Request $request) {
       return $request->user();
   });
   
   //create function in ApiController
   Route::post('/truyencuoi','ApiController@create');
   //show function in ApiController
   Route::get('/truyencuoi','ApiController@show');
   //get data by id 
   Route::get('/truyencuoi/{id}','ApiController@showbyid');
   //update by id
   Route::put('/truyencuoiupdate/{id}','ApiController@updatebyid');
   //delete by id
   Route::delete('/truyencuoidelete/{id}','ApiController@deletebyid');
   ```
   
   Đến đây tiếp tục mở terminal ra và gõ nốt câu lệnh còn lại
   
   > php artisan serve
   
   Bây giờ chúng ta sẽ dùng Postman để kiểm tra API
   
   ![](C:\Users\ADMIN\Pictures\RestLaravel\Get.PNG)
   
   Với phương thức GET sẽ lấy toàn bộ dữ liệu từ bảng
   
   ![](C:\Users\ADMIN\Pictures\RestLaravel\GetId.PNG)
   
   Get theo id
   
   ![](C:\Users\ADMIN\Pictures\RestLaravel\POST.PNG)
   
   Chèn dữ liệu vào bảng và thành công
   
   ![](C:\Users\ADMIN\Pictures\RestLaravel\UpdateByid.PNG)
   
   Update theo id = 25
   
   ![](C:\Users\ADMIN\Pictures\RestLaravel\Deletebyid.PNG)
   
   Delete theo id = 577