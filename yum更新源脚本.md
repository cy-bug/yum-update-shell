```bash
#!/bin/bash
# yum update shell
# author:Chen
# 只适用于有/etc/yum.repos.d这个文件夹的系统

echo "The time and date are:"
date
echo "Let's see who's logged into the system:"
who
echo "================================"
# 1.获取用户输入确认要进行yum的更新
read -p "Make sure you start updating yum（y/n）：" sure
# 2.
if [[ "$sure" == "y" ]]
	then
		yum -y install wget
	# 进入目录
		cd /etc/yum.repos.d/
	# 重命名旧文件
		mv CentOS-Base.repo CentOS-Base.repo.old
	# 获取阿里云的更新源
		wget  -O /etc/yum.repos.d/Centos-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
		wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
	# 清除并生成缓存，开始更新
		yum clean all
		yum makecache
		yum update -y
		echo "更新完成！！"
else [[ "$sure" == "n" ]]
	exit 0
fi

```

