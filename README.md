#系统实现总结报告
##一、实现环境
###1. 环境依赖
本课程设计采用python 3.5实现，后端框架采用Django 2.0.1，数据库使用MySQL。搭建本项目所需要的环境依赖如下：
```
Django	                          2.0.1	
Pillow	                          5.3.0	
PyYAML	                          3.13	
confusable-homoglyphs	          3.2.0	
defusedxml	                      0.5.0	
diff-match-patch	              20181111	
django-crispy-forms	              1.7.2	
django-formtools	              2.1
django-import-export	          1.0.1	
django-pure-pagination	          0.3.0	
django-ranged-response	          0.2.0	
django-registration	              2.4.1	
django-reversion	              3.0.0	
django-simple-captcha	          0.5.9	
et-xmlfile	                      1.0.1	
future	                          0.17.1	
httplib2	                      0.12.0	
jdcal	                          1.4	
mysqlclient	                      1.3.13	
odfpy	                          1.4.0	
openpyxl	                      2.5.12	
pip	                      		  18.1
pytz	                          2018.7	
setuptools	                      40.6.2	
six	                              1.12.0
tablib	                          0.12.1	
unicodecsv	                      0.14.1	
wheel	                          0.32.3	
xlrd	                          1.1.0	
xlwt	                          1.3.0	
```
###2. 运行项目
>使用pycharm打开该项目，安装上面所列举的环境依赖，然后运行项目，在浏览器输入：http://127.0.0.1:8000/
>或者，在项目目录下打开cmd，然后输入 python manage.py runserver
接着在浏览器输入上面的地址即可以运行。

##二、系统功能结构图

