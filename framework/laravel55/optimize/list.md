Laravel 优化点
-------------

* 配置加载从缓存文件里获取
  在加载 Illuminate\Foundation\Bootstrap\LoadConfiguration::class 这个类的时候，即配置参数的加载，在处理的时候程序
  首先会判断“/bootstrap/cache/config.php”这个文件是否存在，存在则直接加载，不会再一次全部遍历一次配置目录文件

  代码片段：
  ```
    if (file_exists($cached = $app->getCachedConfigPath())) {
        $items = require $cached;

        $loadedFromCache = true;
    }

    public function getCachedConfigPath()
    {
        return $this->bootstrapPath().'/cache/config.php';
    }
  ```