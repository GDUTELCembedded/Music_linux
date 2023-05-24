







# Music_linux

# [2022 嵌入式组 linux练习项目.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/25784032/1684931877432-17b8e1c6-4011-4793-94fc-16c4aaeee79c.pdf?_lake_card=%7B%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2023%2Fpdf%2F25784032%2F1684931877432-17b8e1c6-4011-4793-94fc-16c4aaeee79c.pdf%22%2C%22name%22%3A%222022%20%E5%B5%8C%E5%85%A5%E5%BC%8F%E7%BB%84%20linux%E7%BB%83%E4%B9%A0%E9%A1%B9%E7%9B%AE.pdf%22%2C%22size%22%3A114255%2C%22ext%22%3A%22pdf%22%2C%22source%22%3A%22%22%2C%22status%22%3A%22done%22%2C%22download%22%3Atrue%2C%22taskId%22%3A%22u501c2905-d66e-4557-8d00-769c8ba7d3d%22%2C%22taskType%22%3A%22upload%22%2C%22type%22%3A%22application%2Fpdf%22%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22u70288f6a%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22file%22%7D)

名称：基于Linux平台的智能音箱 
功能： 编写桌面客户端访问云服务器，通过云服务器控制音箱播放，并可以实现切歌、开始暂停播放等功能通过Linux系统编程编写音箱软件，可以监听开发板按键消息、服务器消息两路IO， 并实现解码音频并实际播放编写按键设备驱动程序，并加载到内核中音箱软件应与系统打包移植或单独移植到硬件开发板上。
进阶功能（不作必须要求）： 编写蓝牙设备驱动，实现蓝牙音箱功能 
你将收获： 
Linux用户层软件开发，系统编程的应用实例 Linux内核设备驱动的开发 网络编程部分内容（涉及一点点） 
Linux系统在硬件平台的部署 
对Linux系统input子系统和音频子系统（内核4.1版本较新的ALSA架构）有初步的了解 
说明： 最好自己准备一块开发板平台，厂商任意，韦东山、正点啥的都可以，arm架构最好新一些，商家提供的系统内核版本最好在4.0以上  



use QT to servey and control linux board to play music

# 基于linux平台的智能音箱 - 软件开发2022.08.20 - 2022.10.20

项目描述：该项目采用C/S架构实现了QT桌面客户端通过访问服务端去控制linux音箱的暂停、播放、切歌、增减音量和文件传输等功能；

1. linux音箱通过监听网络消息以及检测本机按键，多进程实现播放音乐；
2. 服务端采用libevent框架实现了对客户端连接请求和网络消息接收的并发处理；
3. 采用Tcp协议以及Json数据格式进行服务端与客户端、服务端与linux音箱的网络通信和数据解析；
4. 编写驱动程序通过访问设备树生成设备节点，实现获取按键值以及控制led的亮灭；
5. 采用微服务实现从客户端传输本地音乐文件至服务器本地，并更新全部歌曲。
# 音箱（Linux开发板）
韦东山 正点原子开发板
## 基本开发工具
linux虚拟机（用于编译） vscode cmake makefile vim shell脚本
## 驱动（按键 led灯）
设备树 驱动程序 加载/卸载驱动 insmod rmmod
## 网络（select epoll）
TCPsocket 连接 传输消息 消息采用JSON格式
## 播放（可执行文件aplay）
通过多进程exec族播放音乐（实现解码.mp4或.wav文件）
通过循环链表对音乐文件进行管理
# QT（客服端）
## 正常ui界面

![](https://user-images.githubusercontent.com/77655959/203470282-4d4c4ccf-8f50-4570-b6b7-c167eca44fba.png#id=ZwT4Y&originHeight=645&originWidth=1016&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

tcp消息连接端口9999
## QT路径设置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/25784032/1684930730610-240747ca-9157-4c56-9ca2-cabb64864793.png#averageHue=%232e2422&clientId=ue16e28b8-655a-4&from=paste&height=168&id=u012d75a8&originHeight=210&originWidth=868&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=22959&status=done&style=none&taskId=udc1756cf-e091-40b8-934f-9508aabe9db&title=&width=694.4)
打开工程文件
进入工程设置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/25784032/1684930776578-38e03408-75cb-476c-aa2f-aa0a2de8d788.png#averageHue=%23f7f5f5&clientId=ue16e28b8-655a-4&from=paste&height=500&id=u2856fd3f&originHeight=625&originWidth=1361&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=60599&status=done&style=none&taskId=u1811759a-9108-4641-aff8-a8832e8314b&title=&width=1088.8)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/25784032/1684930822447-ce2555a6-9e62-461c-8331-0b996b155ddc.png#averageHue=%233e302f&clientId=ue16e28b8-655a-4&from=paste&height=130&id=u0197eb82&originHeight=162&originWidth=833&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=15000&status=done&style=none&taskId=u9b5dbfd7-8fd3-4100-bbb1-1fb9c6c2ccb&title=&width=666.4)
选择该build文件夹
解决因为移动源文件而导致构建目录与源文件路径不一致问题
另外的解决方案
![image.png](https://cdn.nlark.com/yuque/0/2023/png/25784032/1684930939219-45645072-d52f-48b9-9557-6e9b4becf19a.png#averageHue=%232e2322&clientId=ue16e28b8-655a-4&from=paste&height=162&id=udf19d8fd&originHeight=202&originWidth=847&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=21481&status=done&style=none&taskId=ub3e4dbd2-73e8-482f-aadc-b5a7a572b7c&title=&width=677.6)
删除该文件并重新打开工程文件进行重新配置
## 传输文件界面

![](https://user-images.githubusercontent.com/77655959/203470343-fd53eb0a-4b56-44c2-a745-7b8c4fdbc5c4.png#id=JhcmQ&originHeight=324&originWidth=353&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

文件传输连接端口8080
采用两个服务 避免传输过程中一个服务奔溃而导致另一服务页奔溃

# Linux（服务端）
libevent 
对网络事件进行监听，可对多个客服端进行连接，通过设备号进行区分
![image.png](https://cdn.nlark.com/yuque/0/2023/png/25784032/1684932268077-9e8e838d-0fd9-4365-9110-93ecc1901161.png#averageHue=%23f5f4f3&clientId=ue16e28b8-655a-4&from=paste&height=475&id=u2f400ab0&originHeight=594&originWidth=1124&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=33539&status=done&style=none&taskId=uee09e939-69b3-4216-9768-bbe8352f919&title=&width=899.2)

# 


