# realtek spi flash 
![flash](https://github.com/henerywang/usefultools/blob/master/15236044790021641664232.jpg)

## bootload and kernel offset 
保证bootload .config里CONFIG_LINUX_IMAGE_OFFSET_START和kernel .config里CONFIG_RTL_LINUX_IMAGE_OFFSET的地址相同或者没有越过bootload里kernel的分区就可以了。
