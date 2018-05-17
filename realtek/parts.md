

# realtek spi flash 
![flash](https://github.com/henerywang/usefultools/blob/master/realtek/flash.png?raw=true)

## bootload启动流程
1.检查image的头，从flash中拷贝image的头到sdram，检查checksum。rtk_check_bank_image()  
2.如果有做dual_image,会中band2_offset中读取image头，然后完成步骤一  
3.验证成功后跳到sdram中linux的位置，启动kernel  




## bootload and kernel offset 
保证bootload .config里CONFIG_LINUX_IMAGE_OFFSET_START和kernel .config里CONFIG_RTL_LINUX_IMAGE_OFFSET的地址相同或者没有越过bootload里kernel的分区就可以了。  

## tftp server burn addr
1.bootload下升级image主要是通过tftp，tftp client put到bootload的image先放到sdram中。  
2.读取sdram中image的头信息，找到burn addr和image size，burn addr就是kernel中.config配置offset地址  
3.烧录image到burn addr中  
NOTE：由于我们image由几个部门组成，所以每个部分都用相应的头，所以每个部分都会烧录到kernel中.config配置的offset。不过这些都不重要，只要保证linux的offset和ubootload中相同就可以了，因为bootload中只做了linux image这个头的验证。  


