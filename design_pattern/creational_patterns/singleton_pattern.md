```php
<?php

class DatabaseManager {
    private static $count;
    private static $singletonObject = null;

    public static function createSingletonObject() {
        if (self::$singletonObject !== null) {
            return self::$singletonObject;
        }

        self::$singletonObject = new self();
        is_null(self::$count++) ? self::$count = 1 : self::$count++; // first
        echo self::$count;
        return self::$singletonObject;
    }
}

DatabaseManager::createSingletonObject();
DatabaseManager::createSingletonObject();
DatabaseManager::createSingletonObject();
```