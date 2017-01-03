## 1. Model Define
```
// eg. Home\Model\UserModel
namespace Home\Model;
use Think\Model;
class UserModel extends Model {
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
    'db_rw_separate'=>    true,
    'db_debug'    =>    true,
);
// 分布式数据库部署 并且采用读写分离 开启数据库调试模式
new \Home\Model\NewModel('new','think_',$connection);

// by config define

//数据库配置1
'DB_CONFIG1' => array(
     'db_type'  => 'mysql',
     'db_user'  => 'root',
     'db_pwd'   => '1234',
     'db_host'  => 'localhost',
     'db_port'  => '3306',
     'db_name'  => 'thinkphp'
),
//数据库配置2
'DB_CONFIG2' => 'mysql://root:1234@localhost:3306/thinkphp',

new \Home\Model\NewModel('new','think_','DB_CONFIG1');
new \Home\Model\BlogModel('blog','think_','DB_CONFIG2');
```

```
# using functions

// create instance by D Function
$User = D('User');
// 相当于 $User = new \Home\Model\UserModel();
// 执行具体的数据操作
$User->select();

// create instance by M function
// 使用M方法实例化
$User = M('User');
// 和用法 $User = new \Think\Model('User'); 等效
// 执行其他的数据操作
$User->select();
```
** M function won't load Model define, which would have better performance; however, D function could used for Model redefine.

## 3. Field Define

## 4. Database Connect

## 5. Switch Database

## 6. Distribute Deploy

## 7. Link Operation
- where\*	used for condition query

```
$User = M("User"); // 实例化User对象
$User->where('type=1 AND status=1')->select(); 

$User = M("User"); // 实例化User对象
$map['name'] = 'thinkphp';
$map['status'] = 1;
// 把查询条件传入查询方法
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
$data['name'] = '流年';
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
$this->comment('查询考试前十名分数')
->field('username,score')
->limit(10)
->order('score desc')
->select();

// SELECT username,score FROM think_score ORDER BY score desc LIMIT 10 /* 查询考试前十名分数 */
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
         // 命名范围normal
         'normal'=>array(
             'where'=>array('status'=>1),
         ),
         // 命名范围latest
         'latest'=>array(
             'order'=>'create_time DESC',
             'limit'=>10,
         ),
     );
}

# File Controller
$Model = D('News'); // 这里必须使用D方法 因为命名范围在模型里面定义
$Model->scope('normal')->select();
$Model->scope('latest')->select();
```

## 9. CRUD
```
# Create (Write)
$data['name'] = $_POST['name'];
$data['email'] = $_POST['email'];

if($User->create($data)){
    $result = $User->add(); // 写入数据到数据库 
    if($result){
        // 如果主键是自动增长型 成功后返回值就是最新插入的值
        $insertId = $result;
    }
}

# Read
$User = M("User");
$data = $User->where('status=1 AND name="thinkphp"')->find();

# Update
$User = M("User"); 
$data['name'] = 'ThinkPHP';
$data['email'] = 'ThinkPHP@gmail.com';
$User->where('id=5')->save($data); 

# Delete
$User = M("User");
$User->where('id=5')->delete();
$User->delete('1,2,5'); 
$User->where('status=0')->delete(); 
```
## 10. Active Record
## 11. Field Pointer
## 12. Query Search
### Query Basic
```
$User = M("User"); // 实例化User对象
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
$User = M("User"); // 实例化User对象
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
## 14. Auto Complete
## 15. Param Bind
## 16. Virtual Model
```
// Virtual Model is not real Model, it won't connect with database
namespace Home\Model;
Class UserModel extends \Think\Model {
     Protected $autoCheckFields = false;
}
```

## 17. Model Layers
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

## 19. Relationship Model
## 20. Advanced Model
## 21. MeogoDB Model

