# 线报酷消息推送脚本
线报酷消息推送通知，适用于iphone端，主要使用了ios的bark应用程序来进行推送

# 如何使用
1.在ios苹果商城里面安装bark

2.需要一台服务器，阿里云，腾讯云等等都可，没什么太大配置要求

3.本人使用的ubuntu18.04.6 LTS

4.需要在服务器上安装python3.11.x版本(自行度娘安装),不建议使用服务器自带的低版本python3.6.x

5.需要安装redis

6.脚本上需要修改`BARK_DEVICE_TOKEN`的值,在bark移动端程序中可以查看到

7.其它参数`IXBK_ID_EX`和`SCHEDULER_SECONDS`可自行根据需求修改（线报酷提供的接口，不建议太过频繁的请求）

# 安装依赖库
```python
pip install apscheduler
pip install barknotificator
pip install redis
pip install requests
```

# 运行
```python
python push.py &
```

# 其它命令
```shell
# 杀掉运行的脚本进程
ps -ef | grep push.py | grep -v grep | awk '{print $2}' | xargs kill -15

# 定时任务(每天凌晨2点停止脚本运行，5点启动脚本)
>> crontab -e
0 2 * * * ps -ef | grep push.py | grep -v grep | awk '{print $2}' | xargs kill -15 
0 5 * * * /usr/local/bin/python3 /root/push.py &
```
