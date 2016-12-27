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

