---
title: Enable touchpad gestures on Ubuntu 18.04
author: rachit kinger
date: '2018-06-06'
slug: enable-touchpad-gestures-on-ubuntu-18-04
categories:
  - linux
tags:
  - ubuntu
  - '18.04'
  - touchpad gestures
  - gnome
subtitle: ''
---
_Note: originally I wrote this post as [an answer on stackexchange](https://askubuntu.com/a/1044184/783538)._  


Here is the problem: my laptop (Dell XPS-15 9560), has quite a good touchpad which work wonderfully smooth in Windows 10 but when I use Ubuntu (18.04, X.org) there is no out of the box functionality for multi-touch gestures like three fingers slide up.  

I have managed to get multi-gestures working on my computer. Kohei Yamada has developed an application called Fusuma to enable multi-touch gestures on Linux. It requires you to install Ruby on your machine if it isn't already installed. 

Follow the instructions from  fusuma [GitHub's Readme](https://github.com/iberianpig/fusuma/blob/master/README.md) page or you could follow these steps which worked for me:  

First of all check if your current user is part of the input group. You can do that by  

    sudo gpasswd -a $USER input  

Then log out and log back in. Now install xdotool and libinput-tools.  
    
    sudo apt-get install libinput-tools  

    sudo apt-get install xdotool  

If you haven't installed Ruby you can do that now:  

    sudo apt install ruby  

Now install fusuma  

    gem install fusuma  

## Deciding your gestures  

This is basically creating a `.yml` file with the desired configuration. If you want standard gestures you can follow these instructions or feel free to tweak around to get desired gestures.   

Go to your config folder in home directory.  

    cd ~/.config    

Now create a folder named `fusuma`  

    mkdir fusuma  

In there create a file called `config.yml`  

    touch config.yml   

Now you can use your favourite text editor to enter the contents in this file.   

    nano config.yml   

Copy and paste the following instructions if you are using GNOME, which is the default environment in 18.04.   

    swipe:
      3: 
        left: 
          command: 'xdotool key alt+Right'
        right: 
          command: 'xdotool key alt+Left'
        up: 
          command: 'xdotool key super'
        down: 
          command: 'xdotool key super'
      4:
        left: 
          command: 'xdotool key ctrl+alt+Down'
        right: 
          command: 'xdotool key ctrl+alt+Up'
        up: 
          command: 'xdotool key ctrl+alt+Down'
        down: 
          command: 'xdotool key ctrl+alt+Up'
    pinch:
      in:
        command: 'xdotool key ctrl+plus'
      out:
         command: 'xdotool key ctrl+minus'
    
    threshold:
      swipe: 0.4
      pinch: 0.4
    
    interval:
      swipe: 0.8
      pinch: 0.1


Note that the gestures that this configuration has created for you are the following:  

Mult-touch Gesture | Action |  
-------------------|--------|  
3 Fingers - Left | Go Next on Browser |  
3 Fingers - Right | 	Go Back on Browser |  
3 Fingers - Up	| Show all Windows|   
3 Fingers - Down | 	Close Exposé (Esc) |  
4 Fingers - Left | 	Next Desktop |  
4 Fingers - Right | 	Previous Desktop|   
4 Fingers - Up	 | Next Desktop|   
4 Fingers - Down	| Previous Desktop|  

After this you can run the command in terminal to test if it has installed  

    sudo fusuma  

nothing will happen in the terminal. Just start using your multi-touch gestures - swipe away on your touchpad.  

Now all you have to do is add Fusuma and the command for it in your start-up applications.  

Hope this helps.  
