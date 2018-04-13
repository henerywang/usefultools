# 指针套路：
* 一个有10个指针的数组，该指针是指向一个整型数的
> int *i[10]  
* 一个指向有10个整型数数组的指针
> int *(i)[10]  
* 一个指向函数的指针，该函数有一个整型参数并返回一个整型数
> int *(i)(int)  
* 一个有10个指针的数组，该指针指向一个函数，该函数有一个整型参数并返回一个整型数
>  int *(i[10])(int)

# sizeof套路：
```c
char  str1[] = “Hello” ;
char  str2[5] = {'H','e','l','l','o'};
char  str3[6] = {'H','e','l','l','o','/0'};
char   *p1 = "Hello";
char  *p2[]={"hello","world"}; 
int     n = 10;
int    *q = &n;
```
> sizeof(str1)=6 自动加'/0'  
> strlen(str1)=5 不会加上'/0'的长度  
> sizeof(str2)=5  
> strlen(str2)=? 一直到出现结束符'/0'的地址位置  
> sizeof(str3)=6  
> strlen(str3)=5  
> sizeof(p1)=4  
> strlen(p1)=5  



