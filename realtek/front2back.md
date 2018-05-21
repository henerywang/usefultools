<meta http-equiv="refresh" content="10">
# rtl sdk cgi
主要介绍从rtl sdk页面post的数据怎么保存到flash,以及怎么让相应服务重带的。
## 前端POST请求
1. 以home.htm为列，修改页面中参数后，点击保存，页面会发送POST请求，如下图wireshark抓的http报文。  
![flash](https://github.com/henerywang/usefultools/blob/master/realtek/save-data.png?raw=true)  
* 第一个框对应的url是boa server即将调用的保存数据的函数，home页面对应的是formWlanSetup  
* 第二个框对应的是POST数据。这里面我们用到数据最终会存到flash中  

2. 数据保存后，如果需要重带相应的服务，可以通过web页面发送formRebootCheck的POST请求，如下图  
![flash](https://github.com/henerywang/usefultools/blob/master/realtek/do-service.png?raw=true)  
* 红色框就是后台即将调用的formRebootCheck函数。这个函数会把run_init_script_flag置1，这样相应的服务就会重启，这些服务会从flash中读取刚才存下去的参数  

## 后台重带服务
* 这个地方主要分析下sysconf函数，因为formRebootCheck最终会调到这里来。这里面完成了所有服务的重带工作。下图是代码流程,简要分析以下sysconf init ：  
![dsl](https://github.com/henerywang/usefultools/blob/master/realtek/frount2back.png?raw=true)  

