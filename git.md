# Git版本控制的只言片语

[link](http://gitref.org/zh/basic/#diff)

git clone <url> [FolderName]

git add

  > 缓存(追踪)文件（选择哪些文件需要缓），可以接多个文件名，以空格分开；可以用*或者.表示通配符

git diff

  > 后退出按键为：“q”  
  diff列出add(追踪)过的文件的改动  
  没有参数 => 显示**未缓存**的改动  
  --stat => 无参数的简介输出
  --cached => 显示**已缓存**改动  
  HEAD => 显示**所有**的改动  

git status [-s]

  > 查看当前修改状态，`-s`为输入简洁版  
  文件左边为红色表示没有追踪，绿色反之  
  commit的时候是提交已经追踪的代码（左边为绿色的）