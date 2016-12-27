## 1. Data Cache
ThinkPHP supports follow caches:

- Apachenote
- Apc
- Db
- Eaccelerator
- File
- Memcache
- Redis
- Shmop
- Sqlite
- Wincache
- Xcache

By default ThinkPHP would use File as cache.

## 2. Quick Cache
```
F('data',$Data);
F('data',$Data,TEMP_PATH);
$Data = F('data');
F('data',NULL); // remove cache
F('User/data',$Data);
```

## 3. Query Cache
```
$Model->cache(true)->where('status=1')->select();
$Model->cache(true,60,'xcache')->select();
$value = S('cache_name');
$Model->where($map)->cache('key',60)->find(); // save query for 60s
```

## 4. SQL Query Cache
## 5. Static Cache
