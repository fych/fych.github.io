学习redis客户端命令
```
redis-cli -h
```

使用命令登陆客户端
```
redis-cli
```
学习命令组，在客户端中输入help @，并按tab键，学习各种命令,如通用指令
```
help @generic
```

也可以精确指令，可以使用tab补全，如
```
help flushall
help strlen
```

对于String类型
```
type key
String
```

```
object encoding key
raw
int
embstr
```
append方法会将类型变为raw类型

对于值为int型，有incr和decr方法等，incr等方法会将类型变为int类型


学习redis配置
```
vi /etc/redis/redis.conf
```