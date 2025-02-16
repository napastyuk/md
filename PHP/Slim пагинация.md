#php/slim 

```php
$app->get('/posts', function ($request, $response) use($repo) {
    $perPage = 5;
    $currentPage = $request->getQueryParam('page', 1);
    $basePath = $request->getUri()->getPath();
    if ($currentPage < 1) $currentPage = 1;
    
    $prevPage = $currentPage === 1 ? 1 : $currentPage - 1;
    $prevPageUrl = $basePath.'?'.http_build_query(['page' => $prevPage]);
    
    $pageCount = intval(count($repo->all()) /  $perPage);
    $nextPage = $currentPage >= $pageCount ? $pageCount : $currentPage + 1;
    $nexpPageUrl = $basePath.'?'.http_build_query(['page' => $nextPage]);
    
    $fromIndex = $perPage * ($currentPage - 1);
    $toIndex = ($perPage * $currentPage);
    $pagedPosts = array_slice($repo->all(), $fromIndex, $perPage);
    $params = ['posts' => $pagedPosts,
               'prevPageUrl'=> $prevPageUrl,
               'nextPageUrl'=> $nexpPageUrl
    ];
    
    return $this->get('renderer')->render($response, 'posts/index.phtml', $params);
});
```

еще один вариант `public/index.php`
```php
$app->get('/posts', function ($request, $response) use ($repo) {
    $per = 5;
    $page = $request->getQueryParam('page', 1);
    $offset = ($page - 1) * $per;
    // In real life this request is bad, because it pull all data from the database
    // It would be better to do sql query with LIMIT and OFFSET
    $posts = $repo->all();

    $sliceOfPosts = array_slice($posts, $offset, $per);
    $params = [
        'page' => $page,
        'posts' => $sliceOfPosts
    ];
    return $this->get('renderer')->render($response, 'posts/index.phtml', $params);
})->setName('posts');

$app->get('/posts/{id}', function ($request, $response, array $args) use ($repo) {
    $id = $args['id'];
    $post = $repo->find($id);
    if (!$post) {
        return $response->withStatus(404)->write('Page not found');
    }
    $params = [
        'post' => $post,
    ];
    return $this->get('renderer')->render($response, 'posts/show.phtml', $params);
})->setName('post');
```

`templates/posts/index.phtml`
```php
<?php foreach ($posts as $post) : ?>
  <div>
    <a href="/posts/<?= $post['id'] ?>"><?= htmlspecialchars($post['name']) ?></a>
  </div>
<?php endforeach ?>

<br>

<div>
<a href="?page=<?= $page < 2 ? 1 : $page - 1 ?>">Prev</a> <a href="?page=<?= $page + 1 ?>">Next</a>
</div>
```

`templates/posts/show.phtml`
```php
<h1><?= htmlspecialchars($post['name']) ?></h1>
<div>
    <?= htmlspecialchars($post['body']) ?>
</div>
```