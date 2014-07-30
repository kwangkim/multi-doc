# Prerequisites Install
* Install Python v2.7: [here](http://toomuchdata.com/2014/02/16/how-to-install-python-on-centos/)
```sh
# yum install libffi libffi-devel
# yum install libxslt-devel libxml2-devel
# yum groupinstall "Development tools"
# yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
# vi /etc/ld.so.conf
include ld.so.conf.d/*.conf
/usr/local/lib
# wget http://python.org/ftp/python/2.7.6/Python-2.7.6.tar.xz
# tar xf Python-2.7.6.tar.xz; cd Python-2.7.6
./configure --prefix=/usr/local --enable-unicode=utf8 --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib"
make && make altinstall
```
# Install pip
```sh
# wget https://bootstrap.pypa.io/get-pip.py
# /usr/local/bin/python2.7 ./get-pip.py
# wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py
# /usr/local/bin/python2.7 ./ez_setup.py
# /usr/local/bin/easy_install-2.7 pip
```

# Installing Scrapy
```sh
# /usr/local/bin/pip2.7 install scrapy
```

# Using Scrapy
