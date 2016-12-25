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

![ThinkPHP 5 Installation](http://box.kancloud.cn/2016-03-11_56e274a2376df.png)
