
##### 原因1
  解决方法：在配置文件/etc/ppp/options末尾添加上noauth即可。
##### 原因2

  其实导致上面的错误是在修改chap-secrets配置文件的时候遗漏了最后的*，这个还真不容易发现是神马问题，但是知道错误出在神马地方就简单了。
  http://www.xuebuyuan.com/2102391.html
