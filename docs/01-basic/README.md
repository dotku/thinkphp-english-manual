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
## 1. Official Website Download Page

http://www.thinkphp.cn/down/framework.html

## 2. Composer

`composer create-project topthink/think tp5  --prefer-dist`

## 3. Install From GitHub

Application：https://github.com/top-think/think
Core Code：https://github.com/top-think/framework


```
# China

For user in China, you can install from Chinese Git service for a better network connection performance and speed

[ git.oschina ]

Application Project：https://git.oschina.net/liu21st/thinkphp5.git
Core Framework：https://git.oschina.net/liu21st/framework.git

[ Coding ]

Application Project：https://git.coding.net/liu21st/thinkphp5.git
Core Code：https://git.coding.net/liu21st/framework.git
```

> The reason why split project to Application Repo and Core Repo is for supporting Composer installation

First, copy and donwload Application Project repo.

```
git clone https://github.com/top-think/think tp5
```

Then, switch to tp5 folder, and clone core framework repo.

```
git clone https://github.com/top-think/framework thinkphp
```

After two repo clone, the ThinkPHP 5.0 Git dowlone is finished. If you need upgrade core framework, 
just switch to thinkphp core folder, and run:

```
git pull https://github.com/top-think/framework
```

If you don't familar with git command line, you can use a Git client to clone the repo. 
Please read related client document for detail opeartion instruction, we won't expend the topic here.

No matter what the is way you getting ThinkPHP Framework, you can varify the installation by run the URL.

eg. http://localhost/tp5/public/

The browser should return a page similar like:

![ThinkPHP 5 Installation](https://camo.githubusercontent.com/64cd85167fc67526ec9ea7fd14b2d01982d61c79/687474703a2f2f626f782e6b616e636c6f75642e636e2f323031362d30332d31315f353665323734613233373664662e706e67)
!!! in complete translation work.

After downloading the least version of framework, unzip to web folder, you will see the initial folder structure.

```
project  应用部署目录
├─application           应用目录（可设置）
│  ├─common             公共模块目录（可更改）
│  ├─index              模块目录(可更改)
│  │  ├─config.php      模块配置文件
│  │  ├─common.php      模块函数文件
│  │  ├─controller      控制器目录
│  │  ├─model           模型目录
│  │  ├─view            视图目录
│  │  └─ ...            更多类库目录
│  ├─command.php        命令行工具配置文件
│  ├─common.php         应用公共（函数）文件
│  ├─config.php         应用（公共）配置文件
│  ├─database.php       数据库配置文件
│  ├─tags.php           应用行为扩展定义文件
│  └─route.php          路由配置文件
├─extend                扩展类库目录（可定义）
├─public                WEB 部署目录（对外访问目录）
│  ├─static             静态资源存放目录(css,js,image)
│  ├─index.php          应用入口文件
│  ├─router.php         快速测试文件
│  └─.htaccess          用于 apache 的重写
├─runtime               应用的运行时目录（可写，可设置）
├─vendor                第三方类库目录（Composer）
├─thinkphp              框架系统目录
│  ├─lang               语言包目录
│  ├─library            框架核心类库目录
│  │  ├─think           Think 类库包目录
│  │  └─traits          系统 Traits 目录
│  ├─tpl                系统模板目录
│  ├─.htaccess          用于 apache 的重写
│  ├─.travis.yml        CI 定义文件
│  ├─base.php           基础定义文件
│  ├─composer.json      composer 定义文件
│  ├─console.php        控制台入口文件
│  ├─convention.php     惯例配置文件
│  ├─helper.php         助手函数文件（可选）
│  ├─LICENSE.txt        授权说明文件
│  ├─phpunit.xml        单元测试配置文件
│  ├─README.md          README 文件
│  └─start.php          框架引导文件
├─build.php             自动生成定义文件（参考）
├─composer.json         composer 定义文件
├─LICENSE.txt           授权说明文件
├─README.md             README 文件
├─think                 命令行入口文件
```

5.0 deploy suggestion is use `public` folder as web folder for visiting, other folder would be out from web folder. 
Of course, you must change public/index.php related path. If you can't make it, please remeber seting the folder's 
permission or adding folder list protecting files.

router.php is used for php webserver running. It could use for quick testing.

```
Command Line: php -S localhost:8888 router.php
```