#1 从服务下载文件(参考 https://www.cnblogs.com/yanghj010/p/6009376.html)
##scp(远程复制)
	scp -- secure copy (remote file copy program)
	scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
	         [-l limit] [-o ssh_option] [-P port] [-S program] source ... target
	scp [参数] <源地址（用户名@IP地址或主机名）>:<文件路径> <目的地址（用户名 @IP 地址或主机名）>:<文件路径>

	例如 将服务器47.101.222.255的/home/baison/tensorflow/bazel-bin/tensorflow/examples/android/tensorflow_demo.apk文件拷贝到本地/Users/iqidan/tensorflow/tensorflow_test文件夹下 
	scp root@47.101.222.255:/home/baison/tensorflow/bazel-bin/tensorflow/examples/android/tensorflow_demo.apk /Users/iqidan/tensorflow/tensorflow_test 

#2 远程连接
##ssh(参考 https://www.cnblogs.com/ftl1012/p/ssh.html)
	ssh -- OpenSSH SSH client (remote login program)
	ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface] [-b bind_address]
		[-c cipher_spec] [-D [bind_address:]port] [-E log_file]
		[-e escape_char] [-F configfile] [-I pkcs11] [-i identity_file]
		[-J destination] [-L address] [-l login_name] [-m mac_spec]
		[-O ctl_cmd] [-o option] [-p port] [-Q query_option] [-R address]
		[-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]] destination
		[command]

	简单登录: ssh root@47.101.222.255