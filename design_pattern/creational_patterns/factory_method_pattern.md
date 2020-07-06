```php
<?php

class MySQLConnection
{
    public function __construct()
    {
        echo "MySQL Database Connection" . PHP_EOL;
    }
    public function select() {
        echo "Your mysql select query execute here" . PHP_EOL;
    }
}

class OracleConnection {
    public function __construct()
    {
        echo "Oracle Database Connection" . PHP_EOL;
    }

    public function select()
    {
        echo "Your oracle select query execute here" . PHP_EOL;
    }

}

class DBFactory {
    public static function getConnection($connection)
    {
        // if (!class_exists($connection)) {
        //     throw new Exception("Unknown social network post class $className");
        // }
        $model = $connection . 'Connection';
        return new $model();
    }
}

$dbconn1 = DBFactory::getConnection('MySQL');
$dbconn1->select();

$dbconn2 = DBFactory::getConnection('Oracle');
$dbconn2->select();
```