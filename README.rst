## 安装源
> git clone  https://github.com/mylanch/ssr.git

## 初始化配置

> cd shadowsocksr   
#进入ShadowsocksR根目录

> bash initcfg.sh   
>   #初始化ShadowsocksR服务端

> sed -i "s/API_INTERFACE = 'sspanelv2'/API_INTERFACE = 'mudbjson'/" userapiconfig.py
> 
> sed -i "s/SERVER_PUB_ADDR = '127.0.0.1'/SERVER_PUB_ADDR = '$(wget -qO- -t1 -T2 ipinfo.io/ip)'/" userapiconfig.py

#需要修改一下API接口和本服务器IP(用于生成SSR链接)，默认是 sspanelv2 改为 mudbjson 



## 添加账号
> python mujson_mgr.py -a -u user -p 443 -k password -m aes-256-cfb -O auth_aes128_md5 -G 20 -o tls1.2_ticket_auth_compatible

> python mujson_mgr.py -l   #查看所有用户信息

## 脚本命令

赋予脚本执行权限（执行一次就好）

> chmod +x *.sh

后台运行 但不记录日志（ssh窗口关闭后也继续运行）

> ./run.sh

后台运行 且 记录日志（ssh窗口关闭后也继续运行）

> ./logrun.sh

查看 SS日志（用 logrun.sh 脚本启动才会打开日志）

> ./tail.sh

停止运行
> ./stop.sh


## 设定ssr开机启动

> chmod +x /etc/rc.d/rc.local

在rc.local最后加入/root/shadowsocksr/logrun.sh

## mujson_mgr.py 参数说明
  
>   1. 使用说明: python mujson_mgr.py -a|-d|-e|-c|-l [选项( -u|-p|-k|-m|-O|-o|-G|-g|-t|-f|-i|-s|-S )]
>   2.  
>   3. 操作:
>   4.   -a ADD               添加 用户
>   5.   -d DELETE            删除 用户
>   6.   -e EDIT              编辑 用户
>   7.   -c CLEAR             清零 上传/下载 已使用流量
>   8.   -l LIST              显示用户信息 或 所有用户信息
>   9.  
>   10. 选项:
>   11.   -u USER              用户名
>   12.   -p PORT              服务器 端口
>   13.   -k PASSWORD          服务器 密码
>   14.   -m METHOD            服务器 加密方式，默认: aes-128-ctr
>   15.   -O PROTOCOL          服务器 协议插件，默认: auth_aes128_md5
>   16.   -o OBFS              服务器 混淆插件，默认: tls1.2_ticket_auth_compatible
>   17.   -G PROTOCOL_PARAM    服务器 协议插件参数，可用于限制设备连接数，-G 5 代表限制5个
>   18.   -g OBFS_PARAM        服务器 混淆插件参数，可省略
>   19.   -t TRANSFER          限制总使用流量，单位: GB，默认:838868GB(即 8PB/8192TB 可理解为无限)
>   20.   -f FORBID            设置禁止访问使用的端口
>   21.                        -- 例如：禁止25,465,233~266这些端口，那么这样写: -f "25,465,233-266"
>   22.   -i MUID              设置子ID显示（仅适用与 -l 操作）
>   23.   -s value             当前用户(端口)单线程限速，单位: KB/s(speed_limit_per_con)
>   24.   -S value             当前用户(端口)端口总限速，单位: KB/s(speed_limit_per_user)
>   25.  
>   26. 一般选项:
>   27.   -h, --help           显示此帮助消息并退出
