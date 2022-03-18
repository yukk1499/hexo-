---
  title: yagmail模块
  tags:
  - python
---

https://www.osgeo.cn/yagmail/usage.html

yagmailAPI及相关教程

python利用yagmail(第三方登录)模块实现邮件发送

```
import yagmail   这不会不懂吧！
```

```python
yag = yagmail.SMTP('自己的邮箱账号','授权密码','服务器')
注意授权密码不是账户登录密码(登录第三方平台需要授权密码，慎用！！)
授权密码需要登录邮箱网页版 设置———开启POP3/SMTP/IMAP服务，即可获得授权码
服务器：例如xx@163.com  则服务器为smtp.163.com
```

```python
yag.send('目标邮箱账号','主题名称', '邮件内容')
发送给多个人(列表或元组)
       变量名=['邮箱账号',邮箱账号]
       yag.send(变量名,'主题名称', '内容')
想发送给多个人，还要写上收件人名称咋办？（字典）
       定义一个变量名用来保存这些邮箱账号
       变量名={'邮箱账号':'别名','邮箱账号':'别名'}
          注意:其实别名就是收件人名称(自己定义)
       yag.send(变量名,'主题名称', '内容')
```

![](C:\Users\wyw\Desktop\QQ.png)

