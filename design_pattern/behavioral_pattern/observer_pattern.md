```php
<?php

interface Observer
{
    function attach($observer);
    function detach($observer);
    function notify();
}

interface EvenntAction
{
    function update($observer);
}

class ManageUser implements Observer
{
    private $observers;
    private $users;

    public function addUser($user)
    {
        $this->_users[] = $user;
        $this->notify();
        return $this;
    }

    public function getOldMembers()
    {
        return array_slice($this->_users, 0, -1) ?? [];
    }

    public function getLastMember()
    {
        return end($this->_users);
    }

    function attach($observer)
    {
        $this->observers[] = $observer;
        return $this;
    }

    function detach($observer)
    {
        // if (($key = array_search($observer, $this->observers)) !== false) {
        //     unset($messages[$key]);
        // }
    }

    function notify()
    {
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }
    }
}

class MailNewMember implements EvenntAction
{
    function update($observer)
    {
        echo 'Welcome:' . $observer->getLastMember() . "\r\n";
    }
}

class MailOldMember implements EvenntAction
{
    function update($observer)
    {
        foreach ($observer->getOldMembers() as $member) {
            echo $member . 'Welcome to ' . $observer->getLastMember() . "\r\n";
        }
    }
}

$manageUser = new ManageUser();
$manageUser
    ->attach(new MailNewMember())
    ->attach(new MailOldMember());

$manageUser->addUser('1_Member');
$manageUser->addUser('2_Member');
$manageUser->addUser('3_Member');
```