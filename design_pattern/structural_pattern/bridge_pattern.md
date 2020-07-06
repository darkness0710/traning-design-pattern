```php
<?php

interface PointApi
{
    function getPoint();
}

class BankingPoint implements PointApi
{
    function getPoint()
    {
        echo 'banking point';
    }   
}

class EcomPoint implements PointApi
{
    function getPoint()
    {
        echo 'ecom point';
    }   
}

class User
{
    private $name;
    private $pointApi;

    public function setUp($name, PointApi $pointApi)
    {
        $this->name = $name;
        $this->pointApi = $pointApi;
    }

    public function pay()
    {
        $this->pointApi->getPoint();
    }
}

$user = new User;
$user->setUp('Test', new BankingPoint);
$user->pay();

```