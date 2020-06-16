```php
<?php

interface EmailInterface
{
    public function sendEmail();
}

interface FileInterface
{
    public function sendFile($file);
}

class SendUserEmail implements EmailInterface
{
    public function sendEmail()
    {
        echo '[send mail for user]';
    }
}

class SendAdminUser implements EmailInterface
{
    public function sendEmail()
    {
        echo '[send mail for admin]';
    }
}

class AmazonS3 implements FileInterface
{
    public function sendFile($file)
    {
        echo '[logic send file api s3]' . $file . "\r";
    }
}

class Azure implements FileInterface
{
    public function sendFile($file)
    {
        echo '[logic send file api azure]' . $file . "\r";
    }
}

class GoogleDriver implements FileInterface
{
    public function sendFile($file)
    {
        echo '[logic send file api google driver]' . $file . "\r";
    }
}

class FileUpload
{
    private $mailService;
    private $fileService;

    public function setMailService(EmailInterface $mailService)
    {
        $this->mailService = $mailService;
        return $this;
    }

    public function setFileService(FileInterface $fileService)
    {
        $this->fileService = $fileService;
        return $this;
    }

    public function sendMail()
    {
        $this->mailService->sendEmail();
        return $this;
    }

    public function sendFile($file)
    {
        $this->fileService->sendFile($file);
        return $this;
    }
}

$file = 'jav.png';
$fileUpload = new FileUpload();
$fileUpload->setFileService(new GoogleDriver())
    ->setMailService(new SendUserEmail())
    ->sendFile($file) // [logic send file api google driver]jav.png
    ->sendMail(); // [send mail for user]
```