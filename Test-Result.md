**Câu 1**. Cho 3 URI tương ứng với 3 controller và method sau

    - `/admin/product` - ProductController@index
    - `/admin/user` - UserController@index
    - `/admin/category` - CategoryController@index
​
Hãy định nghĩa các route cho các URI trên với các yêu cầu sau
- Sử dụng prefix chung là `admin`
- Cả 3 route đều là `GET`
- User phải login mới đc access vào 3 route trên
- Sau khi tạo xong, chỉ duy nhất 3 route đc tạo ra, ko đc phép hơn

## Trả lời

    Route::prefix('admin')->middleware('auth')->group(function() {

        Route::get('product', [ProductController::class, 'index']);
        
        Route::get('user', [UserController::class, 'index']);

        Route::get('category', [CategoryController::class, 'index']);
    });
​

**Câu 2**. Hãy cho biết sự khác nhau giữa post và get (nêu rõ sự giống nhau và khác nhau). Trong thực tế POST hay get được dùng nhiều hơn

Trả lời

Giống nhau: 

- GET và POST đều là hai phương thức của giao thức HTTP
- Đều gửi dư liệu về server xủ lí, sau khi người dùng nhập thông tin vào form và thực hiện submit
- Trước khi gửi thông tin, sẽ được mã hóa bắng giản đồ gọi là url encoding. Về cơ bản nó là các cặp name/value được kết hợp với các kí hiệu '=' và các kí hiệu khác được ngăn cách nhau bởi '&'

Khác nhau:

| GET | POST | 
|:-------|:-------|
|  Phương thức GET truyền thông tin thông qua url.  |  Phương thức POST truyền thông tin thông qua HTTP header  |  
|  Dữ liệu của METHOD GET gửi đi thì hiện trên thanh địa chỉ (URL) của trình duyệt.  |  Dữ liệu được gửi đi với METHOD POST thì không hiển thị trên thanh URL  |  
| HTTP GET có thể duy trì bởi lịch sử đó cũng là lý do mà người dùng có thê đánh dấu được. | HTTP POST không thể duy trì bởi lịch sử, đó cũng là lý do mà người dùng không thể đánh dấu HTTP POST được. | 
| Không bảo mật | Bảo mật | 
| Thực thi nhanh hơn POST vì những dữ liệu gửi đi luôn được webbrowser lưu ở bộ nhớ đêm | Thực thi chậm hơn GET |
| Không sử dụng Phương thức GET để gửi password hoặc thông tin nhạy cảm lên server | Dữ liệu gửi bởi phương thức POST thông qua Http header, vì vậy việc bảo mật phụ thuộc vào giap thức Http. Sử dụng Secure Http để chắc chắn thông tin đã an toàn. |
| Gửi form với form gửi đi bằng phương thức GET có thể gửi lại bằng cách bấm F5 | Gửi lại dữ liệu của form thì trình duyệt sẽ hiển thị một hộp thoại cảnh báo |
| Dữ liệu gửi đi được lưu lại trong lịch sử web, có thể xem lại | Không lưu lại trong lịch sử |

GET hay POST thường được sử dụng hơn?

- Đối với dữ liệu ít thay đổi, sử dụng GET để truy xuất và xử lí nhanh hơn 
- Dữ liệu bảo mật thì dùng POST

**Câu 3** Kể tên các loại Route bạn thường sử dụng trong Laravel

​
Trả lời

| Verb | Uri | Action  |
|:-------|:------|-------|
|  GET  |  /users  |   index  |
|  GET  |  /users/create  |   create  |
| POST | /users | store |
| GET | /users/{photo} | show |
| GET | /photos/{photo}/edit | edit |
| PUT/PATCH | /photos/{photo} | update |
| DELETE | /photos/{photo} | destroy |

    //Các thuộc tính chung được quy định trong một mảng định dạng là tham số đầu tiên của phương thức Route::group

    //nhóm nhiều route lại với nhau thành một nhóm
    Route::prefix

    // Chuyển hướng (mặc định status code là 302):
    Route::redirect('/here', '/there');

    // Tạo ra các route của đầy đủ các HTTP method, tương ứng với các action trong controller tương ứng, với đầy đủ các thao tác lên một loại dữ liệu (đọc, thêm, sửa, xóa,...).
    Route::resource('photos', 'PhotoController');


**Câu 4**. Nếu trong thư mục `database/migrations` của bạn đang có 3 file migration lần lượt là 1,2,3. Bạn đã chạy `php artisan migrate` cho 3 file đó rồi.
Sau đó bạn tạo thêm 2 file migration lần lượt là 4,5. Lúc này bạn tiến hành chạy lệnh `php artisan migrate`. Những file nào sẽ được thực thi, vì sao lại là những file đó?
​

## Trả lời

2 file 4,5 sẽ được chạy do các file 1,2,3 đã được migrate thì được lưu vào database rồi nên khi chạy `php artisan migrate` chỉ những file chưa được migrate sẽ được tạo

**Câu 5**. Nếu trong thư mục `database/migrations` của bạn đang có 3 file migration lần lượt là 1,2,3. Bạn đã chạy `php artisan migrate` cho 3 file đó rồi.
Sau đó bạn tạo thêm 2 file migration lần lượt là 4,5. Lúc này bạn tiến hành chạy lệnh `php artisan migrate:rollback`. Những file nào sẽ được thực thi, vì sao lại là những file đó?
​
## Trả lời

`php artisan migrate:rollback`: Database sẽ lưu danh sách version migrate. Khi rollback, nó sẽ tìm version mới nhất trong Database => file 1, 2, 3

**Câu 6**. Hãy cho biết sự khác nhau giữa migrate:refresh và migrate:reset trong Laravel
​

Trả lời

- migrate:refresh: xóa dữ liệu nhưng không xóa bảng
- migrate:reset: xóa dữ liệu và xóa cả bảng

**Câu 7**. Hãy lấy một ví dụ về 1 trường hợp Query N+1 và giải thích nó bằng code demo

##### Model:
    class Course extends Model
    {
        public function lessons()
        {
            return $this->hasMany(Lesson::class);
        }
    }
##### Controller:
    public function index(Request $request)
    {
        return view('courses.index', [
            'courses' => $this->model->getAll(),
        ]);
    }
##### View:
    @foreach($courses as $course)
        <li>{{ $course->lessons->name }}</li>
    @endforeach
##### Giải thích:
Nếu database có 10 lessons thì nó sẽ truy vấn tới database tổng cộng là 11 lần.

Trong đó có một truy vấn là lấy ra tất cả courses, còn lại là name tương ứng của lesson.
​

**Câu 8**. Hãy kể tên một số ORM Relationship trong Laravel mà bạn đã sử dụng (tối thiểu 5) kèm giải thích phía sau

## 1. One to One

Cái này chỉ phụ thuộc vào cái kia và ngược lại

Ví dụ: Có bảng Users và bảng Avatar thì ở đây một người dùng thì chỉ có một cái avatar và chiếc avatar này chỉ đại diện cho user đó.

Từ một user để gọi tới avatar tương ứng của user đó

    public function avatar()
    {
        return $this->hasOne('App\Avatar');
    }

Ngược lại, từ avatar này để truy vấn ra nó thuộc user nào:

    public function user()
    {
        $this->belongsTo('App\User');
    }
## 2. One to Many

Mối quan hệ này để biểu thị một mối quan hệ cha-con. Ví dụ một user thì sẽ có nhiều bài posts. 

Một user có thể có nhiểu bài posts:

    public function posts()
    {
        return $this->hasMany('App\Post');
    }

Ngược lại, một bài post chỉ thuộc về 1 user:

    public function user()
    {
        return $this->belongsTo('App\User');
    }
## 3. Many to Many

Ví dụ một product sẽ thuộc nhiều orders mà một order lại có nhiều products.

Để biểu diễn được quan hệ này cần sử dụng đến một bảng thế 3, tên là order_product, đồng thời sẽ chứa 2 cột là order_id và product_id

Biểu diễn method Product với bảng order:

    public function orders()
    {
        return $this->belongsToMany('App\Order');
    }

Ngược lại, đối với bảng Order định nghĩa như sau:

    public function product()
    {
        return $this->belongsToMany('App\Product');
    }

***Eloquent sẽ tự động tìm đến bảng trung gian đặt tên theo thứ tự alphabet, trong trường hợp này bảng sẽ tên là order_product.***

## 4. Has One Through

Đây là một mối quan hệ liên kết các bảng với nhau thông qua một bảng trung gian

Ví dụ có 3 bảng:

    users
        id - integer
        supplier_id - integer

    suppliers
        id - integer

    history
        id - integer
        user_id - integer

Mặc dù bảng history không chứa supplier_id nhưng vẫn có thể truy cập đến user's history bởi mối quan hệ hasOneThrough như sau:

    class Supplier extends Model
    {
        public function userHistory()
        {
            return $this->hasOneThrough('App\History', 'App\User');
        }
    }

Trong đó:
- tham số thứ nhất: tên của model muốn truy cập
- tham số thứ 2 là model trung gian

Hai bảng user và history định nghia như bình thường

## 5. Has Many Through
Truy cập bảng liên kết dễ dàng hơn thông qua bảng trung gian. 

Ví dụ một Team có nhiều bài Post thông qua bảng trung gian là User.

    teams
        id - integer
        name - string

    users
        id - integer
        team_id - integer
        name - string

    posts
        id - integer
        user_id - integer
        title - string

Mặc dù bảng posts không chứa khóa ngoại team_id, nhưng với quan hệ hasManyThrough sẽ lấy tất cả posts của một teams bằng cách $team->posts. 

Để thực hiện việc này thì Eloquent sẽ kiểm tra team_id thông qua bảng users. 

    class Team extends Model
    {
        public function posts()
        {
            return $this->hasManyThrough('App\Post', 'App\User');
        }
    }

Trong đó:

- Tham số đầu tiên: tên model muốn truy cập
- Tham số thứ hai: model trung gian.


**Câu 9**. Hãy cho biết sự khác nhau giữa Session và Cookie trong PHP

- Cookie: được tạo khi người dùng truy cập 1 website, cookie sẽ ghi nhớ những thông tin như tên đăng nhập, mật khẩu,.... Các thông tin này được lưu để nhận biết người dùng khi truy cập vào một trang web.

- Session: Lưu lại dữ liệu của người dùng sử dụng website. Giá trị của session được lưu trong một tập tin trên máy chủ. Ví dụ khi đăng nhập vào một trang web và đăng nhập với tài khoản đã đăng ký trước đó. Máy chủ sau khi xác thực được thông tin người dùng cung cấp là đúng nó sẽ sinh ra một tập tin (hay chính là session của trình duyệt của người dùng) chứa dữ liệu cần lưu trữ của người dùng.

| Cookie | Session | 
|:-------|:------|
|  Cookie được lưu trữ trên trình duyệt của người dùng  | Session không được lưu trữ trong trình duyệt của người dùng  |  
|  Dữ liệu cookie được lưu trữ ở phía máy khách  |  Dữ liệu session được lưu trữ ở phía máy chủ  |   
| Dữ liệu cookie dễ dàng sửa đổi khi chúng được lưu trữ ở phía khách | Dữ liệu session không dễ sửa đổi vì chúng được lưu trữ ở phía máy chủ |
| Dữ liệu cookie có sẵn trong trình duyệt đến khi hết hạn | Dữ liệu session có sẵn cho trình duyệt chạy. Sau khi đóng trình duyệt sẽ mất thông tin session | 
​

**Câu 10**. Để kiểm tra một `column name` là email có phải là column của table `users` hay không, bạn kiểm tra như thế nào trong Laravel. Cho ví dụ

    if (Schema::hasColumn('users', 'email')) {
        // The "users" table exists and has an "email" column...
    }
​

**Câu 11**. Để tạo một Rule trong Laravel bạn sử dụng câu lệnh nào?
    Để truyền một giá trị từ Request vào trong Rule bạn truyền thông qua method nào
    Cho ví dụ về cách truyền

Trả lời

command:

    php artisan make:rule CheckPassword --invokable

Để truyền một giá trị từ Request vào trong Rule bạn truyền thông qua method:

    public function __invoke($attribute, $value, $fail)
        {
            if (!Hash::check($value, auth()->user()->password)) {
                $fail("The old password doesn't match");
            }
        }

Rule CheckPassword sẽ được khai báo trong PasswordRequest như sau:

    class PasswordRequest extends FormRequest
    {
        public function rules()
        {
            return [
                'old_password' => [
                    'required',
                    'min:6',
                    new CheckPassword
                ],
                'new_password' => [
                    'required',
                    'confirmed',
                    'min:6'
                ],
            ];
        }
    }

​

**Câu 12**. Hãy cho biết cách tạo một đối tượng (object) từ một class trong PHP. cho ví dụ 
​
- Lớp (class) là một mẫu cho các đối tượng cùng kiểu. 
- Đối tượng (object) là một thực thể cụ thể của lớp (class).

Có thể tạo nhiều đối tượng từ một lớp. Mỗi đối tượng có tất cả các thuộc tính và phương thức được định nghĩa trong lớp nhưng chúng sẽ có các giá trị thuộc tính khác nhau.

Các đối tượng của một lớp được tạo bằng cách sử dụng từ khóa `new`.

        <?php
            class Cat {
                public $name;
                public $color;
                
                function set_name($name) {
                    $this->name = $name;
                }
                function get_name() {
                    return $this->name;
                }
                function set_color($color) {
                    $this->color = $color;
                }
                function get_color() {
                    return $this->color;
                }
                # Methods of Cat class
                function info(){
                    return $this->name." cat has ".$this->color." color";
                }
                function sleep(){
                    return $this->name." cat takes a nap.";
                }
            }
            $tom = new Cat();
            $tom->set_name("Tom");
            $tom->set_color("grey and white");

            $kitty = new Cat();
            $kitty->set_name("Kitty");
            $kitty->set_color("white and pink");
    

**Câu 13**. Hãy cho biết ý nghĩa của abstract class, khi nào nên sử dụng abstract class

- `abstract class` là một lớp trừu tượng. Một lớp được gọi là abstract nếu nó chứa ít nhất 1 method abstract.

- Các class khi kế thừa một abstract class sẽ phải định nghĩa lại các phương thức trừu tượng của abstract class

- Một class chỉ có thể kế thừa 1 lớp trừu tượng
​

=> Khi một nhóm đối tượng có cùng bản chất kế thừa từ một class thì sử dụng abstract class.

**Câu 14**. Hãy cho biết ý nghĩa của interface, khi nào nên sử dụng interface

- Là cấu trúc trong OOP cho phép các class khác có thể implements.
- Interface là một Template (khuôn mẫu), nó không phải là một lớp đối tượng.
- Một đối tượng implement một interface thì nó phải khai báo và định nghĩa tất cả các hàm trong Interface.
- Interface không thể khởi tạo.
- Interface có thể được extends với nhau.
- 1 class có thể implements nhiều Interface

=> Khi một nhóm đối tượng không có cùng bản chất nhưng chúng có hành động giống nhau thì sử dụng interface.
​

**Câu 15**. Hãy cho biết sự giống và khác nhau giữa where và whereIn trong Laravel
​
- whereIn: whereIn(column, array())

Kiểm tra xem cột 'age' có giá trị nào thuộc mảng [18, 19, 20, 21] không, có nếu thì lấy 

    $get = DB::table('users')
		->whereIn('age', [18, 19, 20, 21])
		->get();

- where:
  
​Kiểm tra 1 đối tượng nào đó có thỏa mãn điều kiện cụ thể không

    $get = DB::table('users')
		->where('name', 'mai')

**Câu 16**. Hãy cho biết ý nghĩa của việc đặt tên route trong laravel. Cho ví dụ về cách đặt tên route trong Laravel
​

## Trả lời:

- Việc đặt tên cho các route rất có ý nghĩa và hữu dụng khi  muốn thay đổi URI mà không phải thay đổi quá nhiều code.

        Route::get('user/profile', 'UserController@showProfile')->name('profile');


- Để đặt tên một route sử dụng phương thức name

Khi route đã được đặt tên, có thể sử dụng tên này qua phương thức route


**Câu 17**. Một object user có attribute là first_name và last_name. Giá trị của first_name là `Mr.` giá trị của `last_name` là Laravel. Định nghĩa trong model để có thể tạo ra một attribute mới `fullname`. Fullname là giá trị của first_name + last_name

    class User extends Model
    {
        protected $appends = ['full_name'];
        
        public function getFullName()
        {
            return $this->first_name.' '.$this->last_name;
        }
    }
​

**Câu 18**. Một product có thể thuộc nhiều category và một category có thể có nhiều product
Hãy viết Relationship thể hiện điều này (viết nó trong model Product, User)

## Trả lời

Relationship: Many to many

    class Product extends Model {

        ...

        public function categories()
        {
            return $this->belongsToMany(Product::class);
        }
    }


    class Category extends Model {

        ...

        public function products()
        {
            return $this->belongsToMany(Category::class);
        }
    }
​
Ngoài ra, cần 1 bảng trung gian CategoryProduct chứa `category_id` và `product_id`

**Câu 19**. Điều gì xảy ra khi bạn submit một form không có input name='_token'
​

## Trả lời:

***Lỗi 419, page expired***

Vì name="_token" này để chứng thực xem có phải người dùng gửi request lên không. Vậy nếu không có thì sẽ bị tấn công csrf

**Câu 20**. Làm thế nào để kiểm tra một table đã tồn tại trong database (trong Laravel)
​  

    if (Schema::hasTable('users')) {
        // The "users" table exists...
    }