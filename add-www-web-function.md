# 为web添加新功能

原文在代码目录 `doc/addwebfunc` 下：
 
```
	为web添加新功能

本文由 ytht系统维护组负责维护。
您认为在本文中发现了怀疑有错的地方，或是不通的语句、错字别字，请与sofire@ytht.net联系。

假设要添加 bbsmyfunc功能，具体作用是打印字符串：it's my function。
此处的账号要求用bbs，不要用root。

1，修改nju09/bbsmain.c 函数的 cgi_applet applets 结构体
  仿照 {bbsdoc_main, {"bbsdoc", "doc", NULL}} ，添加一条：
  {bbsmyfunc_main,{"bbsmyfunc","myfunc",NULL}}

2，为新功能添加一个新文件：nju09/bbsmyfunc.c
  内容为：

#include "bbslib.h"

int
bbsmyfunc_main()
{
        html_header(1);
        check_msg();

	printf("it's my function\n");

        http_quit();
        return 0;
}

3，修改nju09/Makefile
  在 CFILE 中添加上bbsmyfunc.c

4，重新生成 proto.h 文件，这步很关键。
  make proto

5，重新编译安装
  make
  make install

6，测试
  http://ip/SMAGICxxxxxxxxxxxxxxxxxxxxxxxx/myfunc
  http://ip/SMAGICxxxxxxxxxxxxxxxxxxxxxxxx/bbsmyfunc
  							sofire
							2004.5.2
```