# 编译

* make 生成执行程序 server 和 client, ip为本机默认ip, 端口9999

# 测试

* 方法一: 先 ./server & 把服务器抛后台, 再运行客户端 ./client

* 方法二: 直接运行测试脚本 ./start.sh &, 想提前停止测试则运行 ./kill.sh

* 方法三: 先 ./server & 把服务器抛后台, 再找个网页的在线websocket输入ip和端口测试

# 注意

* 1.在虚拟机里架服务器的话,最好用桥接的方式获得ip,net方式可能不通;

* 2.服务器示例代码未作过高并发压力测试,仅供开发参考;

* 3.关于服务端bind超时,通常是端口被占用或服务器关闭时有客户端未断开造成,后者会在1分钟后恢复正常.

# 其它

* websocket协议介绍: https://blog.csdn.net/SGuniver_22/article/details/74273839

* 欢迎提出bug、服务器和客户端优化建议、使用过程遇到的问题等等

* 有github帐号的可以左上角issues,或者上面csdn文章评论区提问.

# 限制服务器接入量的因素

* 性能因素:
  * 1.普通计算机接入破千之后CPU会逐渐拉满,很难再接入/发起更多客户端
  * 2.服务端表现为接入量上涨变缓
  * 3.客户端表现为connect阶段超时、登录阶段超时等

* 配置因素:
  * 1.线程数量上限,可自行搜索"linux最大线程数量"进一步了解
  * 2.文件描述符上限,使用指令“ulimit -a”在"open files"项可见,一般为4096,可尝试用指令"ulimit -n 8192"提高
  * 3.其它待续...

* 实测效果:
  * 1.虚拟机ubuntu 14.04 LTS,受制于文件描述符上限,最大接入4090+;
