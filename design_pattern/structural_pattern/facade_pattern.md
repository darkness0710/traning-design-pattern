```php
<?php

interface SocialAction
{
    function share($message, $id);
}

class Twitter implements SocialAction
{
    function share($message, $id)
    {
        echo 'Twitter shared with ' . $id . ':' . $message . PHP_EOL;
    }
}

class Facebook implements SocialAction
{
    function share($message, $id)
    {
        echo 'Facebook shared with ' . $id . ':' . $message . PHP_EOL;
    }
}


class Reddit implements SocialAction
{
    function share($message, $id)
    {
        echo 'Reddit shared with ' . $id . ':' . $message . PHP_EOL;
    }
}

class ShareFacade
{
    protected $twitter;    
    protected $facebook;   
    protected $reddit;    
    
    function __construct(SocialAction $twitter, SocialAction $goole, SocialAction $reddit)
    {
        $this->twitter = $twitter;
        $this->facebook = $goole;
        $this->reddit = $reddit;
    }  
        
    function share($message, $id)
    {
        $this->twitter->share($message, $id);
        $this->facebook->share($message, $id);
        $this->reddit->share($message, $id);
    }
}

$socialNetwork = new ShareFacade(new Twitter, new Facebook, new Reddit);
$socialNetwork->share('Share messages', 6969);
```