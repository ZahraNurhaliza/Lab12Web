# Lab12Web

## Langkah-langkah Praktikum

### *DDL: Table user*
```c
CREATE TABLE `user`(
`id` INT NOT NULL AUTO_INCREMENT,
`username` VARCHAR(50),
`password` VARCHAR(50),
PRIMARY KEY (`id`),
UNIQUE INDEX `UNIQUE` (`username`)
) ENGINE=MYISAM;

INSERT INTO `user` (`username`, `password`) VALUES ('admin'
, md5('admin'));
```

### *File: login_session.php*
```php
<?php

session_start();

if (!isset($_SESSION['isLogin']))
    header('location: login.php');

?>
```

### *File: login.php*
```php
<?php
session_start();

$title = 'Data Barang';
include_once '../../class/config.php';

if (isset($_POST['submit'])) {
    $user = $_POST['user'];
    $password = $_POST['password'];

    $sql = "SELECT * FROM user WHERE username = '{$user}' AND password = md5('{$password}') ";
    $result = $db->query($sql);
    if ($result && mysqli_affected_rows($conn) != 0) {
        $_SESSION['isLogin'] = true;
        $_SESSION['user'] = mysqli_fetch_array($result);

        header('location: home.php');
    } else {
        $errorMsg = "<p style=\"color:red;\">Gagal Login, silakan ulangi lagi.</p>";
    }
}


if (isset($errorMsg)) echo $errorMsg;
?>

    
    <h2>Login</h2>
    <form method="post">
        <div class="input">
            <label>Username</label>
            <input type="text" name="user" />
        </div>
        <div class="input">
            <label>Password</label>
            <input type="password" name="password" />
        </div>
        <div class="submit">
            <input type="submit" name="submit" value="Login" />
        </div>
    </form>
<?php include_once 'footer.php'; ?>
```

### *OUTPUT*
![ss 1](https://github.com/ZahraNurhaliza/Lab12Web/assets/115614417/bdfaa821-9f7f-4c03-89c5-3d0c23a3a0db)

![ss 2](https://github.com/ZahraNurhaliza/Lab12Web/assets/115614417/a7c506fc-81cc-4910-8507-85625235ff09)

![ss 3](https://github.com/ZahraNurhaliza/Lab12Web/assets/115614417/0220aa47-5072-4eef-902c-18416b1d5b51)
