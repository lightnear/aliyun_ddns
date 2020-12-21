# aliyun ddns

## 0x01 install python and requirements

```shell
yum -y install python36 python36-devel
yum -y install python3-devel
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

```shell
# CentOS8/RHEL8
dnf module -y install python38
alternatives --config python
#PyPI 镜像源
pip3 install -i https://mirrors.aliyun.com/pypi/simple pip setuptools -U
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple
pip config set install.trusted-host mirrors.aliyun.com
#安装python依赖
pip install wheel
pip install --upgrade pip setuptools
#安装Aliyun SDK
pip install aliyun-python-sdk-core-v3 aliyun-python-sdk-alidns requests
```

## 0x02 aliyun_ddns

```bash
git clone https://github.com/lightnear/aliyun_ddns.git /opt/ddns
cp /opt/ddns/config_template.json /opt/ddns/config.json
#配置文件更改 config.json
```

## 0x03 编写自动调用的脚本 aliyun_ddns.sh

```shell
#添加cron_job定时任务
cron_job="* * * * * source /opt/py3/bin/activate && python /opt/ddns/aliyun_ddns.py > /dev/null 2>&1"
(crontab -l | grep -v "$cron_job"; echo "$cron_job") | crontab -
#删除cron_job定时任务
#cron_job="/opt/cert_sync.sh"
#crontab -l | grep -v "$cron_job" | crontab -
```
