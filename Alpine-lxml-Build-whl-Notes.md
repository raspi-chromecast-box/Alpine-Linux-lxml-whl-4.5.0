```
sudo docker run -dit \
--name lxml-build \
-v /home/morphs/DOCKER_VOLUME/:/home \
alpine:latest
```
```
sudo docker exec -i -t lxml-build /bin/ash
```

```
apk add bash wget tar curl
cd /home
wget https://www.python.org/ftp/python/3.7.7/Python-3.7.7.tgz
tar -xf Python-3.7.7.tgz
cd Python-3.7.7
apk add alpine-sdk gcc nano build-base linux-headers musl-dev \
make autoconf zlib zlib-dev openssl openssl-dev sqlite-dev \
libffi libffi-dev libxml2-dev libxslt-dev
./configure --enable-optimizations --prefix=/opt/python-3.7.7
make -j 8
make -j 8 install
/opt/python-3.7.7/bin/pip3.7 install pip -U
/opt/python-3.7.7/bin/pip3.7 install setuptools -U
/opt/python-3.7.7/bin/pip3.7 install wheel
cd ..
wget https://github.com/lxml/lxml/archive/lxml-4.5.0.tar.gz
tar -xf lxml-4.5.0.tar.gz
cd lxml-lxml-4.5.0
apk add --no-cache g++
apk add --no-cache libxml2-dev libxslt-dev
apk add --no-cache libxml2 libxslt
```
```
ln -s /opt/python-3.7.7/bin/python3.7 /usr/local/bin/python
ln -s /opt/python-3.7.7/bin/python3.7 /usr/local/bin/python3
/opt/python-3.7.7/bin/pip3.7 install -r requirements.txt
/opt/python-3.7.7/bin/python3.7 setup.py build --without-cython
```
```
nano Makefile
    PYTHON3?=/opt/python-3.7.7/bin/python3
    add --without-cython to inpace and inplace3 args
```
```
CFLAGS="-O0"  make inplace
python setup.py build
python setup.py bdist_egg --without-cython
python setup.py bdist_wheel --without-cython
find . -name '*.whl'
file ./dist/lxml-4.5.0-cp37-cp37m-linux_x86_64.whl
cp ./dist/lxml-4.5.0-cp37-cp37m-linux_x86_64.whl /home/
```
