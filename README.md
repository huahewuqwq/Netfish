校园网Web验证账密钓鱼自动化脚本   
-----------------语言------------------    
Bash,Powershell,Python,VBScript  
-----------------------------------作用--------------------------------------  
集成了Wireshark抓包工具 可以实现在校园网等其他环境下在班级  
电脑上进行账密钓鱼并且自动将所抓到的http包上传到指定的服务器当中  
-----------------------------------原理--------------------------------------   
【以下以校园为背景进行讲述】  
原理嘛 大概就是先将东西复制到U盘 在无人的时候在某个班电脑上(最好是经常用电脑的班) 执行一键  
部署脚本然后便会部署在此台电脑上在C:\Application\Netfish里并且通过修改注册表实现开机自启动  
然后当电脑重启或者有人手动运行main1.cmd时便会开始运行 流程如下  
1.通过Taskkill的方式强制结束explorer.exe程序实现黑屏效果  
    (恢复方式也十分简单 通过Ctrl+Shift+Esc组合按键调出任务管理器运行explorer程序即可)  
2.自动运行设定好的抓包脚本wireshark.bat 并且运行Reminder.exe在顶端显示"请进行网络Web验证 请勿关闭命令提示符 连接成功后自动重启 方可使用电脑"文字  
3.自动打开指定的登陆网址(需要您自行摸索学校的登陆网址并提前写进脚本指定位置 并不难) 这里检测的是edge浏览器  
  如果被关闭则会重新打开 并且期间自动进行Ping测试网络连接  
4.如果用户登陆成功（Ping成功）则会结束抓包进程，在间隔7秒后执行上传命令(vbs脚本是自动输入密码用的 具有模拟键盘输入功能 再次间隔7  
  秒后执行start "" "C:\Application\Netfish\Auto_remove_run.cmd"命令 删除所有文件并且删除开机自启动(此处可能不一定成功 有BUG待修复)  
5.在第四步执行结束后等待7秒后执行"shutdown -r -t 0 -f"重启电脑  
----------------------------------部署----------------------------------------  
将仓库内所有文件下载后拷入U盘 然后修改"main1.cmd","wireshark.bat","ssh_scp/scp.vbs"里的相关内容 已经全部标记好了    
然后将U盘插入目标电脑执行Auto_build_run.cmd脚本就行 如果想卸载就执行Auto_remove_run.cmd脚本即可  
----------------------------------声明----------------------------------------  
此项目仅供学习交流 由于错误使用此项目的内容所造成的一切后果与作者无关。  
祝你生活愉快!  
