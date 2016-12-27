## 1. View Define
## 2. Theme
## 3. Variable Assign
```
// following two statments are the same
$this->assign('name',$value);
$this->name = $value;

// use specified template file
$this->display('read');

// use template over module
$this->display('Member:read');
```

### 4. Getting Template File Path
```
T('Public/menu');
// /View/Public/menu.html

T('blue/Public/menu');
// /View/blue/Public/menu.html

T('Public/menu','Tpl');
// /Tpl/Public/menu.html

T('Public/menu');
// /Tpl/Public_menu.html

T('Public/menu');
// /Tpl/Public/menu.tpl

T('Admin@Public/menu');

// Admin/View/Public/menu.html

T('Extend://Admin@Public/menu');
// Extend/Admin/View/Public/menu.html
```
