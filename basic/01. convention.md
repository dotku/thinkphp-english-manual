## Name Standard

ThinkPHP 5 folows PSR-2 name standard and PSR-4 autoload standard, and please notic following change or standard:

## Folder and File

- Folder won't force any naming standard, supports both camel or underscore style;
- Class library, functions use .php as extension name;
- Class file name use namespace, and namespace path and class file keep the same;
- Class use camel naming style with first letter capitalized, other file use small case and underscore style;
- Class name and class file name are the same by using camel naming style with first letter capitalized

## Functions, Class and Property naming

- Class use camel style with first letter captialized, eg User, UserType;
- function use small case with underscore, eg. get_client_ip;
- method use camel with first letter small cased, eg. getUserName;
- property use camel style with first letter small cased;
- double underscore "__" function or method is magic method, eg. __call or __autoload;

## Constant and Config

- Constant use capital letters and underscore, eg. APP_PATH, and THINK_PATH;
- Config use smallcase and underscore, eg. url_router_on, and url_convert;

## Database Table and Column

Database table and column use small case and underscore naming style,
and please notice that column should not start with underscore, 
eg thinkphp_user and user_name. It is not suggested using camel and Chinese characters for database naming.

## Application Class Naming Standard

Application library root name space would all use app (It can be customized by using app_namespace),
eg. `app\index\controller\Index` and `app\index\model\User`.

> HINT:
> Please don't use reserved keywords for naming, it would cause systematical error.
> For detail keywords in PHP, please read page: 
> http://php.net/manual/reserved.keywords.php
