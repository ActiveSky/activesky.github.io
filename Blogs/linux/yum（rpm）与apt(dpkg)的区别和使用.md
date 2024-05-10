# 区别

##  yum

**配置文件：/etc/yum.conf**

  **yum可以用于运作rpm包** 

 **支持tar包** 

 **rpm -ivh** 

##  apt 

**配置文件：/etc/apt/sources.list**

 **apt-get可以用于运作deb包** 

 **支持tar包** 

 **dpkg -i**

# 常见使用

## yum

​      列出所有已安装包：yum list installed

​      列出所有可安装的包：yum list

​	  安装软件包：yum install <package_name>

​	  查询软件包：yum search <keyword>

​	  删除软件包：yum remove <package_name>

​	  更新软件包：yum update <package_name>

**rpm命令用法：**

​      安装：rpm -ivh *.rpm
​     		 卸载：rpm -e packgename
​      		查看是否已经安装：rpm -q nginx 
​    		  升级：rpm -Uvh xxx
​      		查询所有安装的包： rpm -qa
​      		查询某个包：rpm -qa | grep xxx    rpm -qi xxx
​      		查询软件的安装路径：rpm -ql xxx   rpm -qc xxx
​      		查询某个文件是那个rpm包产生：rpm -qf /etc/yum.conf   rpm -qpi xxx
​      		查看已安装的RMP包：rpm -qa|grep php 

## apt 

​      列出所有已安装包：apt list --installed

 	 安装软件包：sudo apt-get install package

  	重新安装包 ：sudo apt-get install package -- reinstall

  	查询软件包：apt-cache search package 

  	获取包的详细信息：apt-cache show package

  	删除软件包：sudo apt-get remove package   sudo apt-get remove package -- purge（连同配置文件一起删除）

​	  更新软件包：sudo apt-get upgrade package

​	  清理无用的包：sudo apt-get clean && sudo apt-get autoclean

 	 查看该包被哪些包依赖:apt-cache rdepends package

**dpkg命令用法：**

 安装软件包：dpkg -i <package.deb>
    	 列出包 的内容：dpkg -c <package.deb>
    	 查看包信息：dpkg -I <package.deb>
     	移除安装的包：dpkg -r <package>
  	   完全清除包dpkg -P <package>
    	 列出 <package> 安装的所有文件清单：dpkg -L <package>
    	 显示已安装包：dpkg -s <package>
    	 重新配置已安装包dpkg-reconfigure <package>