## View

### View Instantiation

### Template Engine

### Template Variable Assign

```
namespace index\app\controller;

class Index extends \think\Controller
{
    public function index()
    {
        // 模板变量赋值
        $this->assign('name','ThinkPHP');
        $this->assign('email','thinkphp@qq.com');
        // 或者批量赋值
        $this->assign([
            'name'  => 'ThinkPHP',
            'email' => 'thinkphp@qq.com'
        ]);
        // 模板输出
        return $this->fetch('index');
    }
}
```

### Template Render

### Output Replace