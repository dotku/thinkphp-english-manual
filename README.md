# English Guide For ThinkPHP 3.2
## General
### Introduction

ThinkPHP is a free open source light PHP framework. It is quick, simple, and object oriented. The project started from beginning of 2006, and it is under Apache 2 License. The purpose is speed up web application development and enterprise application development.

### Features

- MVC Design Pattern
- ORM Support, including major database programs
- Template Support
- RESTFul Support
- Cloud Platform Support, especially for Sina Cloud and Baidu Cloud
- CLI Support, using command line for development
- RPC Support, including PHPRpc, HProse, jsonRPC, and Yar
- MongoDB Support
- Chace Support, including File, Database, Memcache, Xcache, Redis and ect.

### License

	Apache 2.0

## ThinkPHP Global Functions

C()  
	get or set value in <$MODULE>/Conf/config.php file; the set feature only temporarily set the value, and it won’t overwrite the setting in config.php file.

```	
# eg. some config in config.php file
# return array(
#    …
#    ‘SITE_TITLE’ => ‘BlueJay’,
#    …
# );

// get config value
echo C(‘SITE_TITLE’); // BlueJay
C(‘SITE_TITLE’, ‘BlueJay 2’);
echo C(‘SITE_TILTE’); // BlueJay2
```

E()**  
	Exception handling

G()**  
	Monitoring the time consuming during the procedure.

L()**  
	i18n support

I()  
	read variables from path

```
I('id',0); // return the value of id, similar to $_REQUEST[‘id’]
I('post.name','','htmlspecialchars'); // return $_POST[‘name’];
I('get.name'); // return $_GET[‘name’];
I(‘path.0’); // get path phrase
```

N()**  
	database read write statistic, eg. N(‘read’);

D()  
	create an instance of Model with customized model under Model folder; if there is no customized Model, the systematically Model will return.

M()  
	create an instance of Model automatically, without customized model.

A()  
	create an instance of controller, eg. A(‘Access’)->index();

R()  
	run a function directly, eg. R(‘Access/index’);

B()**  
	run a behavior logic. eg. B(‘CheckAuth’)

redirect()  
	change path to other URL

S()  
	cache management, using File as cache by default.

F()  
	file management

xml_encode(), data_to_xml()  
	convert mixed data to xml string
	
session()  
	working with session.

cookie()  
	working with cookie

get_client_ip();  
	retrieve visitor’s IP

send_http_status();  
	eg. send_http_status(404); // not found

in_array_case()  
	case insensitive in_array() function.

\*\* those functions are not commonly used.

## CURD

CURD stands for Create, Update, Read, and Delete.

### Create

```
// create data and save to database
$User = D('User');
$data['name'] = 'ThinkPHP';
$data['email'] = 'ThinkPHP@gmail.com';
$User->data($data)->add();
```

### Read
where($array)  
	query result filtered by where  
	eg. D(‘User’)->where(array(‘userId’=> ‘1’));

table($databaseTableName)  
	by default, ThinkPHP would use lowercase table name only,   
	eg D(‘User’) would look for table ‘user’.   
If we want to have case sensitive, we must use D()->table(‘User’)  

field($columnName)  
	eg. $Model->field('id,title,content')->select();  
	
order($orderArray)  
	eg. $Model->where('status=1')->order('id desc')->limit(5)->select();  

fetchSql  
	return only SQL string without running.  
	eg. $result = M('User')->fetchSql(true)->find(1);  
	return: SELECT * FROM think_user where id = 1  

## Commonly Development Cases

to be continued ...
