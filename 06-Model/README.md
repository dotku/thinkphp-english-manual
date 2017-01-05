## 1. Model Define
```
// eg. Home\Model\UserModel
namespace Home\Model;
use Think\Model;
class UserModel extends Model {
}
```
### Properties
There are four properties you can sepcify in Model Defination:

1. tablePrefix  

    ```
# eg, you want to have top_category
namespace Home\Model;
use Think\Model;
class CategoryModel extends Model {
    protected $tablePrefix = 'top_'; 
}
```

2. tableName  
  If you use a table name which is different from the Model name.

  ```
namespace Home\Model;
use Think\Model;
class CategoryModel extends Model {
    protected $tableName = 'categories'; 
}
```

3. trueTableName  
  By default, ThinkPHP use underscore format for table, if you are using tables not follow the convention, you must could specify the table name with trueTableName.
  ```
namespace Home\Model;
use Think\Model;
class CategoryModel extends Model {
    protected $trueTableName = 'TopCategories'; 
}
```

4. dbName  
  If you want to use table accross different Database.
  ```
namespace Home\Model;
use Think\Model;
class CategoryModel extends Model {
    protected $trueTableName = 'top_categories'; 
    protected $dbName = 'top';
}
```

## 2. Instance

```
# directly instance

$User = new \Home\Model\UserModel();
$Info = new \Admin\Model\InfoModel();

// by string
new \Home\Model\NewModel('blog','think_','mysql://root:1234@localhost/demo');

// by array
$connection = array(
    'db_type'    =>   'mysql',
    'db_host'    =>   '192.168.1.2,192.168.1.3',
    'db_user'    =>   'root',
    'db_pwd'     =>   '12345',
    'db_port'    =>    3306,
    'db_name'    =>    'demo', 
    'db_charset' =>    'utf8',
    'db_deploy_type'=>    1,
    'db_rw_separate'=>    true, // write read seperate
    'db_debug'    =>    true, // enable debug
);
// Distribute Database Deploy, seperate write and read, and enable debug mode
new \Home\Model\NewModel('new','think_',$connection);

// by config define

// Database Config 1
'DB_CONFIG1' => array(
     'db_type'  => 'mysql',
     'db_user'  => 'root',
     'db_pwd'   => '1234',
     'db_host'  => 'localhost',
     'db_port'  => '3306',
     'db_name'  => 'thinkphp'
),
// Database Config 2
'DB_CONFIG2' => 'mysql://root:1234@localhost:3306/thinkphp',

new \Home\Model\NewModel('new','think_','DB_CONFIG1');
new \Home\Model\BlogModel('blog','think_','DB_CONFIG2');
```

```
# using functions

// create instance by D Function
$User = D('User');
// equal to $User = new \Home\Model\UserModel();
// run data operations
$User->select();

// create instance by M function
$User = M('User');
// equal to $User = new \Think\Model('User');
// other dta operations
$User->select();
```

> M function won't load Model define, which would have better performance; however, D function could used for Model redefine.

## 3. Field Define
System will cache the filed data in the first time of instanlization step, and save it under `Runtime/Data/_fields` forever by using followind format:

```
demo.user.php // User Model created fields
demo.article.php
```

If your data structure changes a lot, you don't want to turn off the cache feature, you can config it by:

```
'DB_FIELDS_CACHE'=>false
```

Or you can clean the cache by manual by delete files under `Data/_fields`.

If you want to improve the performance of the system without cache feature, you could create a Model manually:

```
namespace Home\Model;
use Think\Model;
class UserModel extends Model {
    protected $fields = array('id', 'username', 'email', 'age');
    protected $pk     = 'id'; // primary key
}
```

> 3.2.3+ support combin key
```
namespace Home\Model;
use Think\Model;
class ScoreModel extends Model {
    protected $fields = array('user_id', 'lession_id','score');
    protected $pk     = array('user_id','lession_id');
}
```

You can also define the filed type

```
namespace Home\Model;
use Think\Model;
class UserModel extends Model {
    protected $fields = array('id', 'username', 'email', 'age',
        '_type'=>array('id'=>'bigint','username'=>'varchar','email'=>'varchar','age'=>'int')
    );
}
```

## 4. Database Connect

1. Global Define by using config.php file

  ```
'DB_TYPE'   => 'mysql', 
'DB_HOST'   => 'localhost', 
'DB_NAME'   => 'thinkphp', 
'DB_USER'   => 'root', 
'DB_PWD'    => '123456', 
'DB_PORT'   => 3306, 
'DB_PREFIX' => 'think_', 
'DB_CHARSET'=> 'utf8', 
'DB_DEBUG'  =>  TRUE,
```

2. Define in Model Define

  ```
  namespace Home\Model;
use Think\Model;
class UserModel extends Model{
    protected $connection = array(
        'db_type'  => 'mysql',
        'db_user'  => 'root',
        'db_pwd'   => '1234',
        'db_host'  => 'localhost',
        'db_port'  => '3306',
        'db_name'  => 'thinkphp',
        'db_charset' =>    'utf8',
    );
}
```
  ```
  
namespace Home\Model;
use Think\Model;
class UserModel extends Model{
    // by connection
    protected $connection = 'mysql://root:1234@localhost:3306/thinkphp#utf8';
}
```

3. in instance step

  ```
  $User = M('User','other_','mysql://root:1234@localhost/demo#utf8');
```

## 5. Switch Database

  For instance, you define the database connection in config.php file:

  ```
'DB_CONFIG1' = array(
    'db_type'  => 'mysql',
    'db_user'  => 'root',
    'db_pwd'   => '1234',
    'db_host'  => 'localhost',
    'db_port'  => '3306',
    'db_name'  => 'thinkphp'
),
'DB_CONFIG2' => 'mysql://root:1234@localhost:3306/thinkphp';
```

  You can switch by:

  ```
$this->db(1,"DB_CONFIG1")->query("查询SQL");
$this->db(2,"DB_CONFIG2")->query("查询SQL");
```

  Or simply by
  
  ```
  $this->db(1,"mysql://root:123456@localhost:3306/test")->query("查询SQL");
  ```

## 6. Distribute Deploy

Under config.php file, and specify

```
'DB_DEPLOY_TYPE'=> 1, // Enable distribute dataabase deploy
'DB_TYPE'       => 'mysql', // must use same database type
'DB_HOST'       => '192.168.0.1,192.168.0.2',
'DB_NAME'       => 'thinkphp', // could define multiple db names
'DB_USER'       => 'user1,user2',
'DB_PWD'        => 'pwd1,pwd2',
'DB_PORT'       => '3306',
'DB_PREFIX'     => 'think_',
'DB_RW_SEPARATE'=>true, // (optional) sperate write and read; otherwise, will read/write to both database machine
```

## 7. Link Operation
- where\*	used for condition query

```
$User = M("User"); // create User Instance Object
$User->where('type=1 AND status=1')->select(); 

$User = M("User"); // create User Instance Object
$map['name'] = 'thinkphp';
$map['status'] = 1;
// pass query condition
$User->where($map)->select(); 
```

- table	use for table selection
```
$Model->table('think_user')->where('status>1')->select();
```

- alias
```
$Model = M('User');
$Model->alias('a')->join('__DEPT__ b ON b.user_id= a.id')->select();

// SELECT * FROM think_user a INNER JOIN think_dept b ON b.user_id= a.id
```

- data
```
$Model = M('User');
$data['name'] = 'liu';
$data['email'] = 'thinkphp@qq.com';
$Model->data($data)->add(); // add row to database
```

- field
```
$Model->field('id,title,content')->select();
// SELECT id,title,content FROM table
```

- order
```
$Model->where('status=1')->order('id desc,status')->limit(5)->select();
```

- limit	
```
$User = M('User');
$User->where('status=1')->field('id,name')->limit(10)->select();
```

- page
```
$Article = M('Article');
$Article->page('1,10')->select(); // page 1
$Article->page('2,10')->select(); // page 2
```

- group
```
$this->field('username,max(score)')->group('user_id')->select();
// SELECT username,max(score) FROM think_score GROUP BY user_id
```

- having
```
$this->field('username,max(score)')->group('user_id')->having('count(test_time)>3')->select(); 
// SELECT username,max(score) FROM think_score GROUP BY user_id HAVING count(test_time)>3
```

- join\*	
```
$Model = M('Artist');
$Model
->join('think_work ON think_artist.id = think_work.artist_id')
->join('think_card ON think_artist.card_id = think_card.id')
->select();
```

- union\*
```
$Model->field('name')
      ->table('think_user_0')
      ->union(array('field'=>'name','table'=>'think_user_1'))
      ->union(array('field'=>'name','table'=>'think_user_2'))
      ->select();
```

- distinct
```
$Model->distinct(true)->field('name')->select();
// SELECT DISTINCT name FROM think_user
```

- lock
```
lock(true); // for Oracle database, will add `FOR UPDATE` or `FOR UPDATE NOWAIT`
```

- cache	
```
$Model->where('id=5')->cache(true)->find();

// cache for 60s
$Model = M('User');
$result = $Model->cache('key',60)->find();
$data = S('key');
```

- comment
```
$this->comment('query top 10 score')
->field('username,score')
->limit(10)
->order('score desc')
->select();

// SELECT username,score FROM think_score ORDER BY score desc LIMIT 10 /* query top 10 score */
```

- relation
(no samples)

- using
(no samples)

- result
(no samples)

- fetchsql
```
$result = M('User')->fetchSql(true)->find(1);
// SELECT * FROM think_user where id = 1
```

- token
```
$model->token(false)->create();
// turn off token varify
```

- validate
(unkown)

- auto
(unkown)

- filter
(unkown)

- scope\*
(unkown)

- bind\*	
(unkown)

- index	
```
$Model->index('user')->select();
// index 'user' by force
```

- strict	
```
// varify if fields are exist; otherwise, would throw error
$model->strict(true)->add($data);
```
(*) Could be used multiple times in one query

## 8. Naming Scope
```
# File Model
namespace Home\Model;
use Think\Model;
class NewsModel extends Model {
     protected $_scope = array(
         // name scope normal
         'normal'=>array(
             'where'=>array('status'=>1),
         ),
         // name scope latest
         'latest'=>array(
             'order'=>'create_time DESC',
             'limit'=>10,
         ),
     );
}

# File Controller
$Model = D('News'); // It must use D function, since scope is defined in Model
$Model->scope('normal')->select();
$Model->scope('latest')->select();
```

## 9. CURD

### Create (Write)
```
$data['name'] = $_POST['name'];
$data['email'] = $_POST['email'];

if($User->create($data)){
    $result = $User->add(); // write to database
    if($result){
        // if primary key is increated automatically, return the least key
        $insertId = $result;
    }
}
```

### Update
```
$User = M("User"); 
$data['name'] = 'ThinkPHP';
$data['email'] = 'ThinkPHP@gmail.com';
$User->where('id=5')->save($data); 
```

### Read
```
$User = M("User");
$data = $User->where('status=1 AND name="thinkphp"')->find();
```

If you want to return a array of column you can use `getField('colName', true)`

```
$User->getField('id',true); // array(1,2,3,4,5)
```

### Delete

```
$User = M("User");
$User->where('id=5')->delete();
$User->delete('1,2,5'); 
$User->where('status=0')->delete(); 
```
## 10. Active Record
By Active Record, you can query and operate the model object easier:

```
$User = M("User"); 

// Tranditional
$User->where('id=8')->find();

// AR Mode
$User->find(8);
$userList = $User->select('1,3,8'); 

// Update
$User->find(1); 
$User->name = 'TOPThink'; 
$User->save(); 

$User->id = 1;
$User->name = 'TOPThink'; 
$User->save(); 

// Delete
$User->find(2);
$User->delete(); 

$User->delete(8); 
$User->delete('5,6'); 
```
> **warning**
> *There is bug for $User->select(1,2,3)*

## 11. Field Pointer
You can point the field to different column in database:

```
namespace Home\Model;
use Think\Model;
Class UserModel extends Model{
     protected $_map = array(
         'name' =>'username', 
         'mail'  =>'email', 
     );
}
```

## 12. Query Search
### Query Basic
```
$User = M("User"); // instanlized User Object
$User->where('type=1 AND status=1')->select(); 
```
### Query Express
> EQ	equal
> NEQ	not equal
> GT	greater
> EGT	equal or greater
> LT	less than
> ELT	equal or less than
> LIKE		
> [NOT] BETWEEN	
> [NOT] IN
> EXP	Express

```
$map['id']  = array('egt',100);
$map['name'] = array('like','thinkphp%');
$map['b'] =array('notlike',array('%thinkphp%','%tp'),'AND');
$map['id']  = array('exp',' IN (1,3,8) ');
...

$model->where($map)->select();
```

### Quick Query
```
$User = M("User");
$map['name|title'] = 'thinkphp';
$User->where($map)->select(); 
```

### Range Query
```
$map['id'] = array(array('gt',1),array('lt',10)) ; // ( id > 1) AND ( id < 10)
$map['id'] = array(array('gt',3),array('lt',10), 'or') ; // ( id > 3) OR ( id < 10)
$map['id']  = array(array('neq',6),array('gt',3),'and'); // ( id != 6) AND ( id > 3)
```

### Combo Query
```
$User = M("User"); // instanlized User Object
$map['id'] = array('neq',1);
$map['name'] = 'ok';
$map['_string'] = 'status=1 AND score>10';
$User->where($map)->select(); 
// ( `id` != 1 ) AND ( `name` = 'ok' ) AND ( status=1 AND score>10 )
```

### Static Query
```
$User = M("User");
$userCount = $User->count("id");
$maxScore = $User->max('score');
$minScore = $User->where('score>0')->min('score');
$avgScore = $User->avg('score');
$sumScore = $User->sum('score');
```

### SQL Query
```
$Model = new \Think\Model();
$Model->query("select * from think_user where status=1"); // read only
$Model->execute("update __PREFIX__user set name='thinkPHP' where status=1"); // write or update
```

### Dynamical Query
```
$user = $User->getByName('liu21st');
$user = $User->getByEmail('liu21st@gmail.com');
$userId = $User->getFieldByName('liu21st','id');
```

### Subquery
```
$subQuery = $model->field('id,name')->table('tablename')->group('field')->where($where)->order('status')->select(false); 
// returns SQL string
```

## 13. Auto Verify
### Static Define

In model class

```
namespace Home\Model;
use Think\Model;
class UserModel extends Model{
   protected $_validate = array(
     array('verify','require','require verify code！'), 
     array('name','','account name is already exist！',0,'unique',1), 
     array('value',array(1,2,3),'range is not correct！',2,'in'), 
     array('repassword','password','password doesn\'t match',0,'confirm'), 
     array('password','checkPwd','password format is incorrect',0,'function'), 
   );
}
```

In controller

```
$rules = array(
     array('verify','require','require verify code！'), 
     array('name','','account name is already exist！',0,'unique',1), 
     array('value',array(1,2,3),'range is not correct！',2,'in'), 
     array('repassword','password','password doesn\'t match',0,'confirm'), 
     array('password','checkPwd','password format is incorrect',0,'function'), 
);
$User = M("User"); 
if (!$User->validate($rules)->create()){
     exit($User->getError());
}else{
     // do something ...
}
```
## 14. Auto Complete

```
namespace Home\Model;
use Think\Model;
class UserModel extends Model{
     protected $_auto = array ( 
         array('status','1'),  // set status = 1 in add
         array('password','md5',3,'function') , // md5 the password
         array('name','getName',3,'callback'), 
         array('update_time','time',2,'function'),
     );
}
```

## 15. Param Bind
```
# We do this
$Model = M('User');
$Model->name = 'thinkphp';
$Model->email = 'thinkphp@qq.com';
$Model->add();

# Actually, the system help us do this

$Model = M('User');
$Model->name = ':name';
$Model->email = ':email';
$bind[':name']    = 'thinkphp';
$bind[':email']   = 'thinkphp@qq.com';
$Model->bind($bind)->add();
```

## 16. Virtual Model
```
// Virtual Model is not real Model, it won't connect with database
namespace Home\Model;
Class UserModel extends \Think\Model {
     Protected $autoCheckFields = false;
}
```

## 17. Model Layers

- Home\Model\UserModel
- Home\Logic\UserLogic
- Home\Service\UserService 

```
#eg. define a logic

namespace Home\Logic;
class UserLogic extends \Think\Model{
}
```

Instanlized in Controller: `D("User", "Logic")`


## 18. View Model

```
# File: App\Home\Model\BlogViewModel.class.php
# Create A View Model
namespace Home\Model;
use Think\Model\ViewModel;
class BlogViewModel extends ViewModel {
   public $viewFields = array(
     'Blog'=>array('id','name','title'),
     'Category'=>array('title'=>'category_name', '_on'=>'Blog.category_id=Category.id'),
     'User'=>array('name'=>'username', '_on'=>'Blog.user_id=User.id'),
   );
 }
```

Extral function for View Model array:

- `_table`, by default ThinkPHP use underscore format, if your table is using different format, you can use `_table` to specify the table name.
- `_as`, you can create another name for a table, such as `_as` => 'B' stands for table Blog
- `_on`, it is for condition, eg `'_on'=>'Blog.category_id=Category.id'`
- `_type`, is for JOIN type, eg `'_type'=>'LEFT'`

## 19. Relationship Model

There are 3 types for relations:

- HAS_ONE
- BLONGS_TO
- HAS_MANY
- MANY_TO_MANY

```
namespace Home\Model;
use Think\Model\RelationModel;
class UserModel extends RelationModel{
    protected $_link = array(
        'Profile'=>array(
            'mapping_type'      => self::HAS_ONE,
            'class_name'        => 'Profile',
            ……
            ),
        );
}
```

> Properties for HAS_ONE
- class_name: related model name
- mapping_name: it would use model_name if not defined
- foreign_key
- condition
- mapping_fields
- as_fields

> Properties for BELONGS_TO
- class_name: related model name
- mapping_name: it would use model_name if not defined
- foreign_key
- condition
- parent_key
- as_fields

> Properties for HAS_MANY
- class_name: related model name
- mapping_name: it would use model_name if not defined
- foreign_key
- parent_key
- condition
- mapping_fields
- mapping_limit
- mapping_order

> Properties for MANY_TO_MANY
- class_name
- mapping_name
- foreign_key
- relation_foreign_key
- mapping_limit
- mapping_order
- relation_table

### CRUD with Relation Model

```
$User = D("User");
$user = $User->relation(true)->find(1);

// OUTPUT
array(
    'id'        => 1,
    'account'   => 'ThinkPHP',
    'password'  => '123456',
    'Profile'   => array(
        'email'     => 'liu21st@gmail.com',
        'nickname'  => '流年',
        ),
    )

// OUTPUT for define as_fields
array(
    'id'        => 1,
    'account'   => 'ThinkPHP',
    'password'  => 'name',
    'email'     => 'liu21st@gmail.com',
    'nickname'  => '流年',
    )
```

```
// Write

$User = D("User");
$data = array();
$data["account"]    = "ThinkPHP";
$data["password"]   = "123456";
$data["Profile"]    = array(
  'email'    =>'liu21st@gmail.com',
  'nickname'    =>'流年',
);
$result = $User->relation(true)->add($data);

// Update

$User = D("User");
$data["account"]    = "ThinkPHP";
$data["password"]   = "123456";
$data["Profile"]    = array(
     'email'    =>'liu21st@gmail.com',
     'nickname'    =>'流年',
);
$result = $User-> relation(true)->where(array('id'=>3))->save($data);

// Delete
// Delete all
$result = $User->relation(true)->delete("3");
// Delete only Profile
$result = $User->relation("Profile")->delete("3");
```

## 20. Advanced Model
```
namespace Home\Model;
use Think\Model\AdvModel;
class UserModel extends AdvModel{
    protected $_filter = array(
        'content'=>array('contentWriteFilter','contentReadFilter'),
    );
    protected $serializeField = array(
        'info' => array('name', 'email', 'address'),
    );
    Protected  $blobFields = array('content');
    protected $readonlyField = array('name', 'email');
    
}
```

###  Pessimistic Locking and Optimistic Locking 
```
// Pessimistic Locking
$User->lock(true)->save($data);
```
For Optimistic Locking, just create a field "lock_version" under a table, and make it true by default.

### Lazy Update

```
$User = D("User"); 
$User->where('id=3')->setInc("score",10);
$User->where('id=3')->setInc("score",30);

// in lazy mode
User->where('id=3')->setLazyInc("score",10,60);
$User->where('id=3')->setLazyInc("score",30,60);
$User->where('id=3')->setLazyInc("score",10,60);
```

### Data Table Devide Query

For huge data query, might need Data Table Devide Query

```
protected $partition = array(
 'field' => 'name',
 'type' => 'md5',
 'expr' => 'name',
 'num' => 'name',
 );
```

## 21. MongoDB Model

MongoDB is non-relational database (NoSQL), ThinkPHP also support MongoDB Query.

### Key
```
namespace Home\Model;
use Think\Model\MongoModel;
Class UserModel extends MongoModel {
     Protected $_idType = self::TYPE_INT;
     protected $_autoinc =  true;
}
```
### fields auto check
```
Protected $autoCheckFields = true;
```

### Linked Operations
```
$Model = new Think\Model\MongoModel("User");
$Model->field("name,email,age")->order("status desc")->limit("10,8")->select();
```

### Query Operations
```
// FORMAT: $map['field'] = array('express','condition');
// eg. $map['name'] = array('like','^thinkphp');
```
| ThinkPHP Express | MongoDB Original |
| --- | --- |
|neq | $ne |
|lt | $lt |
|lte | $lte |
|gt | $gt |
|gte | $gte |
|like | --- |
|mod | $mod |
|in | $in |
|nin / not | $nin |
|all | $all
|between | --- |
|not between| --- |
|exists | $exists |
|size | $size |
|type | $type |
|regex | MongoRegex |
|exp | --- |

CRUD for MongoDB

```
$data['id'] = 5;
$data['score'] = array('inc',2);
$Model->save($data);
```
| ThinkPHP Express | Mongo |
| --- | --- |
| inc | $inc |
| set | $set |
| unset | $unset |
| push | $push |
| pushall | $pushall |
| addtoset | $addtoset |
| pop | $pop |
| pull | $pull |
| pullall | $pullall |

### Other

mongoCode(), run MongoCode
getMongoNextId(), get next auto increased key
clear(), clean current database table
