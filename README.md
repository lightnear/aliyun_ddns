# aliyun_ddns

## 1 install python and requirements

```shell
yum -y install python36 python36-devel python3-devel
# 建立 Python 虚拟环境
python3.6 -m venv /opt/py3
source /opt/py3/bin/activate
# PyPI 镜像源
pip install -i https://mirrors.aliyun.com/pypi/simple pip setuptools -U
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple
pip config set install.trusted-host mirrors.aliyun.com
# 安装python依赖
pip install wheel
pip install --upgrade pip setuptools
# 安装Aliyun SDK
pip install aliyun-python-sdk-core-v3 aliyun-python-sdk-alidns requests
```

## 2 aliyun_ddns

```shell
git clone https://github.com/lightnear/aliyun_ddns.git /opt/ddns
cp /opt/ddns/config_template.json /opt/ddns/config.json
# 修改config.json的内容
```

## 3 crontab shedule

```shell
echo "* * * * * source /opt/py3/bin/activate && python /opt/ddns/aliyun_ddns.py > /dev/null
" >> /var/spool/cron/root
```
