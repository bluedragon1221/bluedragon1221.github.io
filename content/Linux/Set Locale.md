
# Set Locale
## `Locale-gen`
If this part is a bit confusing, here's a video that explains it. [link](https://youtu.be/68z11VAYMS8?t=711)

Edit `/etc/locale.gen`, uncomment `en_US.UTF-8 UTF-8`.
```sh
... 
#en_SC.UTF-8 UTF-8  
#en_SG.UTF-8 UTF-8  
#en_SG ISO-8859-1  
en_US.UTF-8 UTF-8  
#en_US ISO-8859-1  
#en_ZA.UTF-8 UTF-8  
#en_ZA ISO-8859-1 
...
```

If you installed `vim`, you can use these `vim` commands.
```vim
:%s/#en_US.UTF-8/en_US.UTF-8
:wq
```

Generate the locales by running: 
```sh
locale-gen
```

## `Locale.conf`
Create `/etc/locale.conf` with the following information:
```sh
### /etc/locale.conf ###

LANG=en_US.UTF-8
```