##	arch下dwm的配置
		* 官方源码克隆地址	(git clone https://git.suckless.org/dwm)	# st dmenu slstatus 同理
		* 进入相应的文件夹执行	`sudo make clean install # 安装`
		
##	依赖
		```
			sudo pacman -S xorg-xinit		# 启动dwm
			sudo pacman -S feh		# 设置壁纸，看图工具
			sudo pacman -S udisks2 udiskid		# 识别硬盘	
			sudo pacman -S pcmanfm		# 文件管理器	
			sudo pacman -S alsa-utils		# 音量管理	命令： amxier	
			sudo pacman -S alacritty		# 和st一样的终端，但是带GPU加速，自带功能比st强大	
			sudo pacman -S backlight		# 屏幕亮度调节	命令： light	
			sudo pacman -S kdiff3		# git merge 冲突时的调试工具	
			sudo yay -S picom-jonaburg-git		# 屏幕混成器(pacman内的我无法设置terminal背景透明)	
			```

##	配置文件
	```
		cp /etc/X11/xinit/xinitrc ~/.xinitrc	
		# 拷贝 xinitrc 到用户目录，用来设置启动项目，删除 twm & 所在向下行, 添加 exec dwm 
		# 重启，tty登陆，之后输入 startx 就可以进入dwm

		sudo systemctl enable --now udisks2		# 为硬盘识别设置开机自启
		git config --global merge.tool kdiff3		#为git指定merge冲突时的工具

~/.xinitrc  在 exec dwm 之前写入 
		picom --experimental-backends --config ~/.config/picom/picom.conf -b  # 屏幕混合器(背景透明，特效。。。)
		xrandr --output eDP --mode 2880x1800 --rate 60 --scale 0.5x0.5	#适配分辨率
	```

##	其他
		* 由于dwm打入了 autostart 补丁，所以可以在 ～/.dwm/autostart.sh 中写入需要的配置
		```
			#!/bin/bash
			fcitx5 -d

			while true
			do
			feh --recursive --randomize --bg-fill  /your backgorund img path
			sleep 5m		# 每隔5分钟换壁纸
			
			done
			
		```
