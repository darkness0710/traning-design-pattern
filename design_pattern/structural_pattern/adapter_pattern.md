```php
<?php

interface iStatusUpdate {
    function getUserToken($userId);
    function postUpdate($message);
}

class Facebook implements iStatusUpdate {    
    public function getUserToken($userId) {
        echo 'Facebook get token from id ' . $userId . PHP_EOL;
    }

    public function postUpdate($message) {
        echo 'Facebook send message' . $message . PHP_EOL;
    }
}

class Twitter implements iStatusUpdate {    
    public function getUserToken($userId) {
        echo 'Twitter get token from id ' . $userId . PHP_EOL;
    }

    public function postUpdate($message) {
        echo 'Twitter send message' . $message . PHP_EOL;
    }
}

class SocialAdapter {

    protected $social;

    public function __construct(iStatusUpdate $social){
        $this->social = $social;
    }

    public function getUserToken($userId) {
        $this->social->getUserToken($userId);
    }

    public function postUpdate($message) {
        $this->social->postUpdate($message);
    }
}


$socialAdapter = new SocialAdapter(new Facebook);
$socialAdapter->getUserToken('6969');
$socialAdapter->postUpdate('send message');

$socialAdapter = new SocialAdapter(new Twitter);
$socialAdapter->getUserToken('6969');
$socialAdapter->postUpdate('send message');

```