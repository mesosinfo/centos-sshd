centos-sshd
===========================================================
1. Run the centos-sshd on docker with docker containerizers

	docker run -d -p 2022:22 mesosinfo/centos-sshd:6.7

2. Client connect the container by ssh
    
    ssh -p 2022 root@129.168.203.195
	
	user:root
	password:rootroot