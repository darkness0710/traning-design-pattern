```php
<?php

interface Builder
{
    public function setName($name);
    public function setEmail($email);
    public function setAdress($address);
    public function build();   
}

class MemberBuider implements Builder
{
    private $name;
    private $email;
    private $address;

    function setName($name)
    {
        $this->name = $name;
        return $this;
    }

    function getName()
    {
        return $this->name;
    }

    function setEmail($email)
    {
        $this->email = $email;
        return $this;
    }

    function getEmail()
    {
        return $this->email;
    }

    function setAdress($name)
    {
        $this->name = $name;
        return $this;
    }

    function getAddress()
    {
        return $this->address;
    }

    function build()
    {
        return new Member($this);
    }
}

class Member
{
    private $name;
    private $email;
    private $address;

    function __construct(MemberBuider $member) {
        $this->name = $member->getName();
        $this->email = $member->getEmail();
        $this->address = $member->getAddress();
    }

    static function createBuilder() {
        return new MemberBuider();
    }
}

$member = Member::createBuilder()
    ->setName('123')
    ->setEmail('test@gmail.com')
    ->build();

var_dump($member);
```