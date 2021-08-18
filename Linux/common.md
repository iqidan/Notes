# Linux常用功能
## 1 从服务下载文件(参考 https://www.cnblogs.com/yanghj010/p/6009376.html)
### scp(远程复制)
	scp -- secure copy (remote file copy program)
	scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
	         [-l limit] [-o ssh_option] [-P port] [-S program] source ... target
	scp [参数] <源地址（用户名@IP地址或主机名）>:<文件路径> <目的地址（用户名 @IP 地址或主机名）>:<文件路径>

	例如 将服务器47.101.222.255的/home/baison/tensorflow/bazel-bin/tensorflow/examples/android/tensorflow_demo.apk文件拷贝到本地/Users/iqidan/tensorflow/tensorflow_test文件夹下 
	scp root@47.101.222.255:/home/baison/tensorflow/bazel-bin/tensorflow/examples/android/tensorflow_demo.apk /Users/iqidan/tensorflow/tensorflow_test 

## 2 远程连接
### ssh([参考](https://www.cnblogs.com/ftl1012/p/ssh.html))
	ssh -- OpenSSH SSH client (remote login program)
	ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface] [-b bind_address]
		[-c cipher_spec] [-D [bind_address:]port] [-E log_file]
		[-e escape_char] [-F configfile] [-I pkcs11] [-i identity_file]
		[-J destination] [-L address] [-l login_name] [-m mac_spec]
		[-O ctl_cmd] [-o option] [-p port] [-Q query_option] [-R address]
		[-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]] destination
		[command]

	简单登录: ssh root@47.101.222.255
	加端口: ssh -p 8888 root@192.168.25.137    

## 3 查看网络相关信息[Netstat](https://baike.baidu.com/item/Netstat/527020?fr=aladdin)
### netstat([参考](https://www.cnblogs.com/ftl1012/p/netstat.html))
	netstat [-a][-e][-n][-o][-p Protocol][-r][-s][Interval]

	-a 显示所有socket，包括正在监听的。
　　-c 每隔1秒就重新显示一遍，直到用户中断它。
　　-i 显示所有网络接口的信息，格式“netstat -i”。
　　-n 以网络IP地址代替名称，显示出网络连接情形。
　　-r显示核心路由表，格式同“route -e”。
　　-t 显示TCP协议的连接情况
　　-u 显示UDP协议的连接情况。
　　-v 显示正在进行的工作。
　　-p 显示建立相关连接的程序名和PID。
　　-b 显示在创建每个连接或侦听端口时涉及的可执行程序。
　　-e 显示以太网统计。此选项可以与 -s 选项结合使用。
　　-f 显示外部地址的完全限定域名(FQDN)。
　　-o显示与与网络计时器相关的信息。
	-s 显示每个协议的统计。
　　-x 显示 NetworkDirect 连接、侦听器和共享端点。
　　-y 显示所有连接的 TCP 连接模板。无法与其他选项结合使用。
　　interval 重新显示选定的统计，各个显示间暂停的 间隔秒数。按 CTRL+C 停止重新显示统计。如果省略，则 netstat 将打印当前的配置信息一次。