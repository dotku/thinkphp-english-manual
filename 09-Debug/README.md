## 1. Debug Switch
```
<?php
 define('APP_DEBUG', true); // turn on debug mode
 define('APP_PATH', './Application/');
 require './ThinkPHP/ThinkPHP.php';
```

## 2. Display errors
![Display errors](http://document.thinkphp.cn/Uploads/Editor/2013-12-30/52c10dcb263d8.jpg)

## 3. Log Record
```
# File: config.php
'LOG_RECORD' => true, // 开启日志记录
'LOG_LEVEL'  =>'EMERG,ALERT,CRIT,ERR', // 只记录EMERG ALERT CRIT ERR 错误
```

## 4. Trace page
## 5. Trace Method
## 6. Dump()
## 7. Performance Testing
## 8. Error Debug
```
E($msg); // stop and display msg
```

## 9. Model Debug
```
$User = M("User"); 
$User->find(1);
echo $User->getLastSql();
```
