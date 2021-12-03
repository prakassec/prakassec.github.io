---
layout: post
title: Package installation from the tar file
date: 2019-02-07 20:35:00
categories: Linux
desc: Installation of a package from the tar file.
---
Hi, I tried to install sublime text in my kali machine, while doing that i face some challenges which are documented here.  
If you are a linux beginner then this post will help you.

**How to install a package from tar ball:**  

**Step 1**  
Download the package from official source(Make sure you are downloading correct package depending on your system whether it is debian or other)  
`Mistake 1`: I downloaded RPM package of Libre office for my Kali machine, later only i came to know about that RPM will not support for debian based os.  
So dont waste your bandwidth here.  

**Step 2**  
Extract the downloaded package.  

**Step 3**  
Move that folder to '/opt' directory (In the opt directory only we store third party packages.)  
> mv /your_download_directory   /opt
```console
$ mv /Downloads/Sublime_Text_3  /opt
```

**Step 4**  
Then we need to create a symbolic link(I made some mistake here, which is added at the end)  
```console
$ sudo ln -s /opt/Sublime_Text_3/sublime_text  /usr/bin/sublime

```
**Step 5**
Inorder to setup sublime to launcher(for ubuntu users)  
>sudo your_favourite_editor(vi,sublime)   /usr/share/applications/sublime.desktop
```console
$ sudo vi   /usr/share/applications/sublime.desktop
```

    
```console
Then copy the following text into that file:

[Desktop Entry]
Version=1.0
Name=Sublime Text 3
# Only KDE 4 seems to use GenericName, so we reuse the KDE strings.
# From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.
GenericName=Text Editor

Exec=sublime
Terminal=false
Icon=/opt/Sublime Text 3/Icon/48x48/sublime-text.png
Type=Application
Categories=TextEditor;IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow

[NewWindow Shortcut Group]
Name=New Window
Exec=sublime -n
TargetEnvironment=Unity

```

**Mistake 2**
>I mentioned that in the `step 4` i made some mistake right, lets see whats that is and make me feel awkward  
I forget to mention the `sublime_text` after `sublime_text_3`(i dont know why i forget that), hence the symbolic link points to folder.  
So it cant open sublime when i search for that.  
For that you can also mention exact path at the `Exec= your_path_to_sublime_text` instead of `Exec = sublime`(This is the file which we opened to add sublime to the launcher)
