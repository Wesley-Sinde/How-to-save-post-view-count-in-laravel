# How to save post view count in laravel?
# ✍ Laravel
# ⚇ by wesley
# ⌚ 01-02-20222
Today i will show you how to Implement  Post views count using Laravel . i will add this using easy and simple method for small Projects  click counter or  post visit count . We will create this traffic counter using Laravel.



# show all posts
```php
<?php
namespace App\Http\Controllers;
use App\Models\Post;
use Illuminate\Http\Request;
class PostController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function getAllPost()
    {
        $posts = Post::all();
        return view('posts.all-posts', compact('posts'));
    }


all-posts.blade.php

@foreach ($posts as $post)
    <h3>{{ $post->name }}</h6>
    <a href="{{ route('posts.show',$post->id) }}" 
      class="btn btn-info">View
    </a>
@endforeach
```

Write Post Route
```php
<?php

use App\Http\Controllers\PostController;
use Illuminate\Support\Facades\Route;

Route::get('posts',[ PostController::class,'getAllPost']);

```
Now write Logic View Count

we can implement two way by using(++) or increment() method

# 1) using(++)
```php
public function getViewPost($id)
    {
        $post = Post::find($id);
        $post->view_count++;
        $post->save();
        return view('posts.view-post', compact('post'));
    }

```
# 2) increment() recommended
```php
public function getViewPost($id)
    {
        $post = Post::find($id);
         $post->increment('view_count');
        $post->save();
        return view('posts.view-post', compact('post'));
    }
```

i personally use increment() because it more readable and easy to understand

```php
 <?php
use App\Http\Controllers\PostController;
use Illuminate\Support\Facades\Route;
Route::get('posts/{id}',[ PostController::class,'getViewPost']);
```
