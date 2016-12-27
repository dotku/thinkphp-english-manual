## 1. Define Controller
## 2. Before After Runing
## 3. Action Run
## 4. Fake Static
## 5. URL Case
## 6. URL Generatrion
```
U('User/add') // eg. http://PROJECT_DOMAIN/User/add
U('Blog/read?id=1')
U('Admin/User/select')
```

## 7. AJAX Return
```
# Return JSON format by default
$data['status']  = 1;
$data['content'] = 'content';
$this->ajaxReturn($data);

# Return XML format
$data['status']  = 1;
$data['content'] = 'content';
$this->ajaxReturn($data,'xml');
```
## 8. Redirection
```
$User = M('User'); //实例化User对象
$result = $User->add($data); 
if($result){
    // redirec in success
    $this->success('新增成功', 'User/list');
} else {
    // display error message
    $this->error('新增失败');
}
```

```
// Redirect by URL Geneartion
$this->redirect('New/category', array('cate_id' => 2), 5, '页面跳转中...');
// Redirect by static URL
redirect('/New/category/cate_id/2', 5, '页面跳转中...');
```

## 8. Getting Variables
```
# Tranditional
$id    =  $_GET['id']; // 获取get变量
$name  =  $_POST['name'];  // 获取post变量
$value =  $_SESSION['var']; // 获取session变量
$name  =  $_COOKIE['name']; // 获取cookie变量
$file  =  $_SERVER['PHP_SELF']; // 获取server变量

# ThinkPHP Style

I('post.name','','htmlspecialchars'); // 采用htmlspecialchars方法对$_POST['name'] 进行过滤，如果不存在则返回空字符串
I('session.user_id',0); // 获取$_SESSION['user_id'] 如果不存在则默认为0
I('cookie.'); // 获取整个 $_COOKIE 数组
I('server.REQUEST_METHOD'); // 获取 $_SERVER['REQUEST_METHOD'] 

# URL Variable
# eg. http://serverName/index.php/New/2013/06/01
echo I('path.1'); // 输出2013
echo I('path.2'); // 输出06
echo I('path.3'); // 输出01

## 9. Request Type Detect
> IS_GET	判断是否是GET方式提交
> IS_POST	判断是否是POST方式提交
> IS_PUT	判断是否是PUT方式提交
> IS_DELETE	判断是否是DELETE方式提交
> IS_AJAX	判断是否是AJAX提交
> REQUEST_METHOD	当前提交类型

```
class UserController extends Controller{
     public function update(){
         if (IS_POST){
             $User = M('User');
             $User->create();
             $User->save();
             $this->success('保存完成');
         }else{
             $this->error('非法请求');
         }
     }
}
```

## 10. Empty Operation

```
<?php
namespace Home\Controller;
use Think\Controller;
class CityController extends Controller{
    public function _empty($name){
        //把所有城市的操作解析到city方法
        $this->city($name);
    }
    //注意 city方法 本身是 protected 方法
    protected function city($name){
        //和$name这个城市相关的处理
         echo '当前城市' . $name;
    }
}

/*
Input:

http://serverName/index.php/Home/City/beijing/
http://serverName/index.php/Home/City/shanghai/
http://serverName/index.php/Home/City/shenzhen/

Output:

当前城市:beijing
当前城市:shanghai
当前城市:shenzhen
*/
```

## 11. Empty Controller

```
<?php
namespace Home\Controller;
use Think\Controller;
class EmptyController extends Controller{
    public function index(){
        //根据当前控制器名来判断要执行那个城市的操作
        $cityName = CONTROLLER_NAME;
        $this->city($cityName);
    }
    //注意 city方法 本身是 protected 方法
    protected function city($name){
        //和$name这个城市相关的处理
         echo '当前城市' . $name;
    }
}

/*
Input:

http://serverName/index.php/Home/beijing/
http://serverName/index.php/Home/shanghai/
http://serverName/index.php/Home/shenzhen/

Output:

当前城市:beijing
当前城市:shanghai
当前城市:shenzhen
*/

## 12. Plugin Controller
## 13. Action Bind Class
