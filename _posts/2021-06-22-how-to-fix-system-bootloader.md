---
layout: post
title: How to Fix System BootLoader not found. Initializing defaults.
image: "[https://miro.medium.com/v2/resize:fit:828/format:webp/1*F6M8t3WFYgROk0dr-np06w.png]"
category: Linux
author: Me
---

## How to Fix: System BootLoader not found. Initializing defaults.

If your Linux computer has these criteria and symptoms :
- Using Linux Mint or **Ubuntu derivatives**
- Found this problem when booting then **directly boot into Linux** (without entering GRUB menu)
- and probably, you are running a dual-boot system (?)

Then yes, this method might work for you.

> _Disclaimer: Do with your own risk_

I am running a dual-boot operating system with Linux Mint 20 “Ulyana” and Windows 10. At that time, I just updated my Linux Mint and restarted my laptop. Then this problem appeared.

It brought me directly into Linux Mint without entering the GRUB, so I couldn’t choose which operating system I want to boot.

Then I searched on Google to find how to fix this problem. Finally, I found this [video](https://www.youtube.com/watch?v=GzObzq0V25A&ab_channel=Pygrammer) by Pygrammer on YouTube. The steps are simple, and most importantly, it works!

> _Wait, I suggest you watch the video, but first let me tell you what happened next._

### Short explanation on what happened

Based on the video, the reason why this problem occurs is that the system couldn’t find the GRUB bootloader configuration file.

Actually, the file already exists. We just need some adjustments so the system can find the required file.

Yes, it works. But that problem might appear again **whenever you do an update on packages that are related to the kernel.**

### The bash script

Normally, you need to do the multiple steps explained in the video whenever that problem occurs. But with this script below, you only need to run it and let the script do the rest.

```bash
#! /bin/sh

if [ "$(id -u)" = 0 ]
then
    if [ ! -d "/boot/efi/EFI/Boot.bak/" ]
    then
        echo "Boot.bak does not exist"    
        mv /boot/efi/EFI/Boot /boot/efi/EFI/Boot.bak
        cp -R /boot/efi/EFI/ubuntu /boot/efi/EFI/Boot
        mv /boot/efi/EFI/Boot/shimx64.efi /boot/efi/EFI/Boot/bootx64.efi
    else
        echo "Boot.bak exists"
        rsync -ar --delete /boot/efi/EFI/Boot/ /boot/efi/EFI/Boot.bak/
        rsync -ar --delete /boot/efi/EFI/ubuntu/ /boot/efi/EFI/Boot/
        mv /boot/efi/EFI/Boot/shimx64.efi /boot/efi/EFI/Boot/bootx64.efi
    fi
    echo "Please reboot your system"
else
    echo "Please run as root"
fi
```

> _Before you try the script, please kindly read the following article so you are aware of what you will run._

### The steps

Actually, the script is based on what Pygrammer explained in the video. All the things that he did were inside **/boot/efi/EFI/** directory, and only focused on these 2 folders:
- Boot
- ubuntu

And here are the 3 simple steps :
1. Rename the *Boot* folder to *Boot.bak*
2. Copy *ubuntu* folder and paste it as *Boot*
3. Inside *Boot*, rename *shimx64.efi* to *bootx64.efi*

Done. It’s as simple as that. You can find these steps on this part of the script, or you can just simply run this 3-lines-command to fix the problem.
```bash
mv /boot/efi/EFI/Boot /boot/efi/EFI/Boot.bak        
cp -R /boot/efi/EFI/ubuntu /boot/efi/EFI/Boot        
mv /boot/efi/EFI/Boot/shimx64.efi /boot/efi/EFI/Boot/bootx64.efi
```
Remember the configuration file that can’t be found by the system? I guess it’s the bootx64.efi that was previously named as shimx64.efi.

### The problem on the next run

Let’s say that you’ve already fixed the issue. Then comes the next kernel update. You face that problem again. Will you do the same commands?

Well, I did, and it gave me some errors :
1. We can’t rename the _Boot_ folder to _Boot.bak_, as the _Boot.bak_ folder already exists and contains files
2. We can’t copy the _ubuntu_ folder and paste it as _Boot_, as the Boot folder already exists and contains files

I found the reason after reading this [source](https://askubuntu.com/a/269818). Glad that the explanation in the source also proposes the use of `rsync`.

> _With `rsync`, you can synchronize between two directories. As the folders already exist, you just need to synchronize all the things inside the folders._

I add `-ar --delete` so that :
- `a` : Archive mode. Not only copy files, but also the permissions
- `r` : Recursive. Copy all the files and subfolders inside the parent folder
- `--delete` : Delete files in the destination folder that are not included in the source folder

And here is the command after I made some changes. The third line is the same as the previous command.

```bash
rsync -ar --delete /boot/efi/EFI/Boot/ /boot/efi/EFI/Boot.bak/
rsync -ar --delete /boot/efi/EFI/ubuntu/ /boot/efi/EFI/Boot/
mv /boot/efi/EFI/Boot/shimx64.efi /boot/efi/EFI/Boot/bootx64.efi
```

### Combining into one bash script

Now we have two types of commands that should be run based on suitable conditions. The first one should be run when we’re fixing the problem for the first time, and the second one should be run when we have fixed the problem earlier.

But how does our computer know if we have fixed it earlier or not?

> _Well, we can check whether the **Boot.bak** folder exist or not._

As the folder does not exist in the default condition, we can assume that if _Boot.bak_ doesn’t exist then we should run the first command, and vice versa.

That’s why I add this line below to check :
```bash
if [ ! -d "/boot/efi/EFI/Boot.bak/" ]
```
Check this [link](https://www.cyberciti.biz/faq/howto-check-if-a-directory-exists-in-a-bash-shellscript/) if you want to know more about checking whether a directory exists or not.

### Running as root
One more important thing that we should remember is that we should run this as root, as a normal user doesn’t have access to the directory that we’re talking about. To make sure that we are running it as root, I add this line:
```bash
if [ "$(id -u)" = 0 ]
```
If we open Terminal and run ```id -u``` as root, it will return ```0```. When we run it as a normal user, it will return a number other than ```0``` . I found this method from this [link](https://stackoverflow.com/a/28776100).

### Conclusion

I’ve been running the dual-boot for quite a while. During the time, I found so many problems and always tried to fix it. For one problem, there could be more than one solution. It really depends on the case and the condition of your computer. Maybe one solution works for you, but maybe it does not work for others.

So does the method that I explained here. I can’t guarantee that it will fix the same problem that you have. But at least, some people saying that Pygrammer’s method works well on their computer. And here I just made some adjustments that might be work also, at least on my computer.

Big thanks to Pygrammer on YouTube. Although it seems like he is not an active content creator, at least this one video helped me a lot and I can access my Windows 10 again lol.

I’m not a Linux expert. Feel free to leave comments if you found something that’s not right in this article.

Thanks!

###### _This article has been posted on [Medium](https://medium.com/@arkanhadna/how-to-fix-system-bootloader-not-found-initializing-defaults-b96321f12e8e) on Jun 22, 2021_
