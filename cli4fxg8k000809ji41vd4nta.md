---
title: "Tìm hiểu Facades và cách tạo mới trong Laravel"
datePublished: Fri May 26 2023 10:49:07 GMT+0000 (Coordinated Universal Time)
cuid: cli4fxg8k000809ji41vd4nta
slug: tim-hieu-facades-va-cach-tao-moi-trong-laravel
canonical: https://hau.xyz/tim-hieu-facades-va-cach-tao-moi-trong-laravel/
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1685098122438/dc9d55e7-c2e7-4634-a1a2-0a3cb55cbec9.jpeg

---

[Facades](https://hau.xyz/tim-hieu-facades-va-cach-tao-moi-trong-laravel/) là một tính năng quan trọng trong Laravel, cho phép truy cập các đối tượng trong container của ứng dụng một cách dễ dàng thông qua một cách gọi tĩnh đơn giản. Laravel cung cấp cho chúng ta một số Facades sẵn có như `Route`, `DB`, `View`, `Auth`, `Cache` và nhiều hơn nữa. Ngoài ra, chúng ta cũng có thể tạo ra các Facades tùy chỉnh của riêng mình.

Ví dụ, chúng ta sẽ tạo ra một Facade tùy chỉnh để lấy ra thông tin về một user bằng ID của user đó. Đầu tiên, chúng ta sẽ tạo ra một class để xử lý logic lấy thông tin user:

```php
namespace App\Services;

use App\Models\User;

class UserService
{
    public function getUserById($userId)
    {
        return User::find($userId);
    }
}
```

Tiếp theo, chúng ta sẽ tạo ra một class Facade để truy cập vào đối tượng UserService của chúng ta:

```php
namespace App\Facades;

use Illuminate\Support\Facades\Facade;

class UserFacade extends Facade
{
    protected static function getFacadeAccessor()
    {
        return 'user-service';
    }
}
```

Trong lớp Facade trên, chúng ta kế thừa từ lớp `Facade` của Laravel và định nghĩa phương thức `getFacadeAccessor()` để trả về tên của service mà chúng ta muốn truy cập thông qua Facade. Trong trường hợp này, service của chúng ta là `user-service`.

Tiếp theo, chúng ta sẽ đăng ký service của chúng ta trong container của ứng dụng bằng cách thêm đoạn mã sau vào file `AppServiceProvider.php`:

```php
namespace App\Providers;

use App\Services\UserService;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    public function register()
    {
        $this->app->bind('user-service', function () {
            return new UserService();
        });
    }
}
```

Trong đoạn mã trên, chúng ta đăng ký service của chúng ta với tên là `user-service` và trả về một instance của class `UserService`.

Sau khi đăng ký service và tạo Facade, chúng ta có thể sử dụng Facade `UserFacade` để truy cập vào đối tượng `UserService` một cách dễ dàng:

PHP

```php
use App\Facades\UserFacade;

$user = UserFacade::getUserById(1);
```

Trong đoạn mã trên, `UserFacade` là Facade tùy chỉnh của chúng ta và `getUserById()` là phương thức của đối tượng `UserService`. Khi chúng ta gọi phương thức `getUserById()` thông qua Facade `UserFacade`, Laravel sẽ tự động tạo ra một instance của class `UserService` và gọi phương thức `getUserById()` trên đối tượng đó.

Điều này giúp đơn giản hóa cú pháp và giảm độ phức tạp khi truy cập các đối tượng phụ thuộc trong ứng dụng của chúng ta.

Qua ví dụ trên, chúng ta đã tạo ra một Facade tùy chỉnh và sử dụng nó để truy cập vào một service trong Laravel. Tuy nhiên, để sử dụng Facade tùy chỉnh, chúng ta cần đăng ký service của chúng ta trong container của ứng dụng. Việc này có thể được thực hiện trong một ServiceProvider của Laravel, như `AppServiceProvider`. Sau khi đăng ký service, chúng ta có thể tạo ra một Facade tùy chỉnh bằng cách tạo một class Facade và định nghĩa phương thức `getFacadeAccessor()` để trả về tên của service mà chúng ta muốn truy cập thông qua Facade.

Ví dụ trên chỉ là một ví dụ đơn giản về [cách tạo một Facade tùy](https://hau.xyz/tim-hieu-facades-va-cach-tao-moi-trong-laravel/) chỉnh. Khi tạo Facade, chúng ta cần đảm bảo rằng các phương thức trong Facade đều được định nghĩa và hoạt động đúng cách. Ngoài ra, chúng ta cũng cần đảm bảo rằng các service được đăng ký trong container của ứng dụng và được sử dụng một cách hợp lý trong Facade của chúng ta.

cả nhà xem thêm: [https://hau.xyz/tim-hieu-facades-va-cach-tao-moi-trong-laravel/](https://hau.xyz/tim-hieu-facades-va-cach-tao-moi-trong-laravel/)