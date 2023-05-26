---
title: "So sánh giữa Eloquent ORM và QueryBuilder trong Laravel"
datePublished: Fri May 26 2023 11:00:22 GMT+0000 (Coordinated Universal Time)
cuid: cli4gbx7d001u0al79bj3f3m7
slug: so-sanh-giua-eloquent-orm-va-querybuilder-trong-laravel
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1685098818161/aaf1e46c-d024-4032-9063-c7307a87948b.jpeg
tags: programming-blogs

---

[Eloquent ORM](https://hau.xyz/so-sanh-giua-eloquent-orm-va-querybuilder-trong-laravel/) và [QueryBuilder](https://hau.xyz/so-sanh-giua-eloquent-orm-va-querybuilder-trong-laravel/) trong Laravel đều là các công cụ mạnh mẽ để tương tác với cơ sở dữ liệu. Dưới đây là một số sự khác biệt giữa chúng và một số ví dụ về hiệu năng của chúng:

1. Cú pháp: Eloquent ORM sử dụng các model để tương tác với cơ sở dữ liệu, trong khi QueryBuilder sử dụng các phương thức chuỗi để xây dựng câu truy vấn.
    

Ví dụ:

```php
// Sử dụng Eloquent ORM để lấy tất cả các bài viết
$posts = App\Models\Post::all();

// Sử dụng QueryBuilder để lấy tất cả các bài viết
$posts = DB::table('posts')->get();
```

1. Quản lý mối quan hệ: Eloquent ORM cung cấp các tính năng để quản lý mối quan hệ giữa các bảng trong cơ sở dữ liệu. Ví dụ: quan hệ một-nhiều, nhiều-nhiều. QueryBuilder không cung cấp các tính năng này.
    

Ví dụ:

```php
// Sử dụng Eloquent ORM để lấy tất cả các bài viết của một tác giả cụ thể
$author = App\Models\Author::find(1);
$posts = $author->posts;

// Sử dụng QueryBuilder để lấy tất cả các bài viết của một tác giả cụ thể
$posts = DB::table('posts')->where('author_id', 1)->get();
```

1. Độ trễ: Eloquent ORM có thể chậm hơn QueryBuilder trong một số trường hợp, vì nó phải khởi tạo các model và tải các đối tượng từ [cơ sở dữ liệu](https://hau.xyz/so-sanh-giua-eloquent-orm-va-querybuilder-trong-laravel/). Trong khi đó, QueryBuilder chỉ tạo câu truy vấn SQL và gửi nó đến cơ sở dữ liệu mà không cần tải các đối tượng.
    

Ví dụ:

```php
// Sử dụng Eloquent ORM để lấy tất cả các bài viết của một tác giả cụ thể và in ra tiêu đề của chúng
$author = App\Models\Author::find(1);
foreach ($author->posts as $post) {
echo $post->title;
}

// Sử dụng QueryBuilder để lấy tất cả các bài viết của một tác giả cụ thể và in ra tiêu đề của chúng
$posts = DB::table('posts')->where('author_id', 1)->get();
foreach ($posts as $post) {
echo $post->title;
}
```

Trong trường hợp này, sử dụng QueryBuilder có thể nhanh hơn vì nó chỉ cần tạo câu truy vấn SQL và gửi nó đến cơ sở dữ liệu mà không cần tải các model.

1. Khả năng đọc và ghi: Eloquent ORM cung cấp các [phương thức truy vấn](https://hau.xyz) để đọc và ghi dữ liệu vào cơ sở dữ liệu, trong khi QueryBuilder chỉ hỗ trợ các phương thức truy vấn để đọc dữ liệu.
    

Ví dụ:

```php
// Sử dụng Eloquent ORM để tạo mới một bài viết
$post = new App\Models\Post;
$post->title = 'New Post';
$post->content = 'Lorem ipsum dolor sit amet.';
$post->save();

// Sử dụng QueryBuilder để tạo mới một bài viết
DB::table('posts')->insert([
'title' => 'New Post',
'content' => 'Lorem ipsum dolor sit amet.'
]);
```

Trong trường hợp này, sử dụng Eloquent ORM cho phép bạn tạo mới một bài viết và lưu nó vào cơ sở dữ liệu một cách dễ dàng bằng cách sử dụng các phương thức của model. Trong khi đó, sử dụng QueryBuilder để tạo mới một bài viết đơn giản hơn và chỉ yêu cầu một câu truy vấn SQL.

1. Sử dụng: Eloquent ORM thường được sử dụng cho các ứng dụng lớn và phức tạp hơn, trong khi QueryBuilder thường được sử dụng cho các ứng dụng nhỏ hơn và đơn giản hơn.
    

Ví dụ:

```php
// Sử dụng Eloquent ORM để lấy tất cả các bài viết có chứa từ khóa "Laravel"
$posts = App\Models\Post::where('title', 'like', '%Laravel%')->get();

// Sử dụng QueryBuilder để lấy tất cả các bài viết có chứa từ khóa "Laravel"
$posts = DB::table('posts')->where('title', 'like', '%Laravel%')->get();
```

Trong trường hợp này, sử dụng Eloquent ORM cho phép bạn xử lý các tác vụ phức tạp và truy vấn dữ liệu một cách dễ dàng bằng cách sử dụng các tính năng của model, trong khi đó sử dụng QueryBuilder thích hợp cho các truy vấn đơn giản và nhanh hơn.

Về hiệu năng, Eloquent ORM có thể chậm hơn QueryBuilder trong một số trường hợp, đặc biệt là khi truy vấn dữ liệu trên các bảng lớn. Tuy nhiên, Eloquent ORM có thể được tối ưu hóa bằng cách sử dụng eager loading và caching để giảm thiểu số lần truy vấn cơ sở dữ liệu và cải thiện hiệu suất. Còn QueryBuilder có thể nhanh hơn Eloquent ORM trong các trường hợp đơn giản hơn, nhưng nó không cung cấp các tính năng quản lý mối quan hệ và truy vấn dữ liệu phức tạp như Eloquent ORM........

Xem đầy đủ bài viết tại đây: [https://hau.xyz/so-sanh-giua-eloquent-orm-va-querybuilder-trong-laravel/](https://hau.xyz/so-sanh-giua-eloquent-orm-va-querybuilder-trong-laravel/)