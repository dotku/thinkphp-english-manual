## Configuration

ThinkPHP provides flexible global configuration feature. It is using the most efficent way by using the declare of PHP 
array return. It supports conventional configuration, common configuration, module configuration, extension 
configuration, scenario configuration, environmental configuration and dynamical configuration.

### Environmental Configuration

In development process, it can use the `.env` file under root folder to visualize environmental configuration. `.env` 
file is using ini format, eg:

```
app_debug =  true
app_trace =  true
```

If your deploy environment has environmental variable configuration, please remove `.env` configuration file to avoid 
conflict.

(to be continue ...)