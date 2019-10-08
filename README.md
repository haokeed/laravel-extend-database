<h1 align="center"> laravel-extend-database </h1>

<p align="center"> .</p>


## Installing

```shell
$ composer require haokeed/laravel-extend-database
```

## 描述

这是针对于laravel的观察者模型在进行完善的扩展

```php
Model::where('id', '1')->update([
  'name' => 'laravel'
]);
```

如上的方式修改或者删除而观察者事件失效进一步扩展该功能，使用的方式只需要在模型中引用`ShineYork\LaravelExtend\Database\Eloquent\SEvents`即可

```php
use Illuminate\Database\Eloquent\Model;
use Haokeed\LaravelExtend\Database\Eloquent\SEvents;

class Category extends Model
{
    use SEvents;
}
```


为了改进方案可以将use SEvents进行转移到父类去执行
```php
<?php

namespace Haokeed\LaravelShop\Data\Goods\Models;

use Illuminate\Database\Eloquent\Model as  laravelModel;
use Haokeed\LaravelExtend\Database\Eloquent\SEvents;


class Model extends laravelModel
{
    use SEvents;

}

```

为了更加方便的加载观察者类，可以将观察者添加到配置文件中。

```php
<?php

namespace Haokeed\LaravelShop\Data\Goods\Providers;

use Illuminate\Support\ServiceProvider;
use Haokeed\LaravelShop\Data\Goods\Models\Model;

class GoodsServiceProvider extends ServiceProvider
{
    public function boot()
    {
        Model::observe();

    }
}
```

```php
<?php
//  /Users/sunsheng/Documents/wwwroot/haokeed/laravel-shop/src/Data/Goods/Config/goods.php
return [
    'database' => [
        'observes' => [
            // 批量添加关注者
            // 以后只要有对应的Observer就直接可以添加在这里了
            'Category' => 'CategoryObserver'
        ],
    ]


];
```
