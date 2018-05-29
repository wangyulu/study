装饰者模式
---------

* 案例一

  ```
    <?php

    interface Decorate
    {
        public function display();
    }

    class FangFang implements Decorate
    {
        public function display()
        {
            echo "Fangfang go " . PHP_EOL;
        }
    }

    class Finery implements Decorate
    {
        private $compoment;

        public function __construct(Decorate $compoment)
        {
            $this->compoment = $compoment;
        }

        public function display()
        {
            $this->compoment->display();
        }
    }

    class Shoes extends Finery
    {
        public function display()
        {
            echo 'shoes go ' . PHP_EOL;
            parent::display();
        }
    }

    class Skirt extends Finery
    {
        public function display()
        {
            echo "skirt go " . PHP_EOL;
            parent::display();
        }
    }

    class Fire extends Finery
    {
        public function display()
        {
            echo "before go " . PHP_EOL;
            parent::display();
            echo "after go " . PHP_EOL;
        }
    }

    $fang = new FangFang();
    $shoes = new Shoes($fang);
    $skirt = new Skirt($shoes);
    $fire = new Fire($skirt);
    var_dump($fire);
    $fire->display();


    // 输出：
    object(Fire)#4 (1) {
      ["compoment":"Finery":private]=>
      object(Skirt)#3 (1) {
        ["compoment":"Finery":private]=>
        object(Shoes)#2 (1) {
          ["compoment":"Finery":private]=>
          object(FangFang)#1 (0) {
          }
        }
      }
    }
    before go
    skirt go
    shoes go
    Fangfang go
    after go

  ```

* 案例二

  ```
    <?php

    /*
     * 去公司
     */

    interface GoCompany
    {
        public function go();
    }

    class Traffic implements GoCompany
    {
        private $compoment;

        public function __construct(GoCompany $company)
        {
            $this->compoment = $company;
        }

        public function go()
        {
            $this->compoment->go();
        }
    }

    class Worker implements GoCompany
    {
        public function go()
        {
            echo '出站了' . PHP_EOL;
        }
    }

    class Metro extends Traffic
    {
        public function go()
        {
            echo '准备出地铁站了' . PHP_EOL;
            parent::go();
            echo '到公司了' . PHP_EOL;
        }
    }

    class Bus extends Traffic
    {
        public function go()
        {
            echo '下公交，准备上地铁' . PHP_EOL;
            parent::go();
        }
    }

    class Bike extends Traffic
    {
        public function go()
        {
            echo '停放自行车，准备上公交' . PHP_EOL;
            parent::go();
        }
    }

    class Fire extends Traffic
    {
        public function go()
        {
            echo '骑自行车去公司' . PHP_EOL;
            parent::go();
            echo '上班。。。' . PHP_EOL;
        }
    }

    $worker = new Worker();
    $metro = new Metro($worker);
    $bus = new Bus($metro);
    $bike = new Bike($bus);
    $fire = new Fire($bike);
    var_dump($fire);
    $fire->go();


    // 输出
    object(Fire)#5 (1) {
      ["compoment":"Traffic":private]=>
      object(Bike)#4 (1) {
        ["compoment":"Traffic":private]=>
        object(Bus)#3 (1) {
          ["compoment":"Traffic":private]=>
          object(Metro)#2 (1) {
            ["compoment":"Traffic":private]=>
            object(Worker)#1 (0) {
            }
          }
        }
      }
    }
    骑自行车去公司
    停放自行车，准备上公交
    下公交，准备上地铁
    准备出地铁站了
    出站了
    到公司了
    上班。。。

  ```

* 案例三

  ```
    <?php

    /*
     * 去公司
     */

    interface GoCompany
    {
        public static function go(Closure $next);
    }

    class Metro implements GoCompany
    {
        public static function go(Closure $next)
        {
            echo '准备出地铁站了' . PHP_EOL;
            $next();
            //echo '到公司了' . PHP_EOL;
        }
    }

    class Bus implements GoCompany
    {
        public static function go(Closure $next)
        {
            echo '下公交，准备上地铁' . PHP_EOL;
            $next();
        }
    }

    class Bike implements GoCompany
    {
        public static function go(Closure $next)
        {
            echo '停放自行车，准备上公交' . PHP_EOL;
            $next();
        }
    }

    function getSlice()
    {
        return function ($stack, $pipe) {
            return function () use ($stack, $pipe) {
                return $pipe::go($stack);
            };
        };
    }

    function then()
    {
        $pipes = [
            Bike::class,
            Bus::class,
            Metro::class
        ];

        $firstSlice = function () {
            echo '公司了，上班了。。' . PHP_EOL;
        };

        $pipes = array_reverse($pipes);
        var_dump(array_reduce($pipes, getSlice(), $firstSlice));
        call_user_func(array_reduce($pipes, getSlice(), $firstSlice));
    }

    then();


    // 输出
    object(Closure)#5 (1) {
      ["static"]=>
      array(2) {
        ["stack"]=>
        object(Closure)#4 (1) {
          ["static"]=>
          array(2) {
            ["stack"]=>
            object(Closure)#3 (1) {
              ["static"]=>
              array(2) {
                ["stack"]=>
                object(Closure)#1 (0) {
                }
                ["pipe"]=>
                string(5) "Metro"
              }
            }
            ["pipe"]=>
            string(3) "Bus"
          }
        }
        ["pipe"]=>
        string(4) "Bike"
      }
    }
    停放自行车，准备上公交
    下公交，准备上地铁
    准备出地铁站了
    公司了，上班了。。

  ```