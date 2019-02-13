# git相关
[git bash环境设置](https://blog.csdn.net/jingtingfengguo/article/details/51892864)
[git相关原理和常用命令](https://segmentfault.com/a/1190000017114656)
# .gitlab-ci.yml
cache:
  cache用来指定需要在job之间缓存的文件或目录。只能使用该项目工作空间内的路径。
  如果cache定义在jobs的作用域之外，那么它就是全局缓存，所有jobs都可以使用该缓存。
