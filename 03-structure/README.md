## 1. Module Design
## 2. URL Model
## 3. HMVC (Multiple Level MVC)
## 4. CBD (Core, Behavior, Driver)

```
# Core

ThinkPHP/Common/functions.php // 核心函数库
ThinkPHP/Conf/convention.php  // 惯例配置文件
ThinkPHP/Conf/debug.php  // 惯例调试配置文件
ThinkPHP/Mode/common.php  // 普通模式定义文件
ThinkPHP/Library/Think // 核心类库包
ThinkPHP/Library/Behavior // 系统行为类库
ThinkPHP/Library/Think/App.class.php // 核心应用类
ThinkPHP/Library/Think/Behavior.class.php // 基础行为类
ThinkPHP/Library/Think/Cache.class.php // 核心缓存类
ThinkPHP/Library/Think/Controller.class.php // 基础控制器类
ThinkPHP/Library/Think/Db.class.php // 数据库操作类
ThinkPHP/Library/Think/Dispatcher.class.php // URL解析调度类
ThinkPHP/Library/Think/Exception.class.php // 系统基础异常类
ThinkPHP/Library/Think/Hook.class.php // 系统钩子类
ThinkPHP/Library/Think/Log.class.php // 系统日志记录类
ThinkPHP/Library/Think/Model.class.php // 系统基础模型类
ThinkPHP/Library/Think/Route.class.php // 系统路由类
ThinkPHP/Library/Think/Storage.class.php // 系统存储类
ThinkPHP/Library/Think/Template.class.php // 内置模板引擎类
ThinkPHP/Library/Think/Think.class.php // 系统引导类
ThinkPHP/Library/Think/View.class.php // 系统视图类
```

```
# Driver

ThinkPHP/Library/Think/Cache/Driver // 缓存驱动类库
ThinkPHP/Library/Think/Db/Driver // 数据库驱动类库
ThinkPHP/Library/Think/Log/Driver // 日志记录驱动类库
ThinkPHP/Library/Think/Session/Driver // Session驱动类库
ThinkPHP/Library/Think/Storage/Driver // 存储驱动类库
ThinkPHP/Library/Think/Template/Driver // 第三方模板引擎驱动类库
ThinkPHP/Library/Think/Template/TagLib // 内置模板引擎标签库扩展类库
```

```
# Behavior

app_init 应用初始化标签位
module_check 模块检测标签位（3.2.1版本新增）
path_info PATH_INFO检测标签位
app_begin 应用开始标签位
action_name 操作方法名标签位
action_begin 控制器开始标签位
view_begin 视图输出开始标签位
view_template 视图模板解析标签位
view_parse 视图解析标签位
template_filter 模板解析过滤标签位
view_filter 视图输出过滤标签位
view_end 视图输出结束标签位
action_end 控制器结束标签位
app_end 应用结束标签位
```

## 5. Namespace
## 6. Autoload
## 7. Module Type
## 8. Compiler
## 9. Working Flow
