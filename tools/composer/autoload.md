> 参考地址：https://getyii.com/topic/697

Composer 自动载入的四种方式
========================
PSR-4（推荐）
------------------------
composer.json中的配置

    {
        "autoload" : {
            "psr-4" : {
                "Foo\\" : "src/"
            }
        }
    }

