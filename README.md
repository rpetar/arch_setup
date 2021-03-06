# Multiple Versions of CUDA Libraries On The Same Machine

This file contains some useful aliases and way to handle multiple CUDA versions in Arch-based distributions.
After doing all steps from [CUDA installation](#cuda-installation), reboot system. Initially, CUDA will not be set up. 
You need to set it using alias **_set-cuda-X-Y_**. 
If you want to change version, you must first use **_unset-cuda_** alias, and then set new version.

>## Edit content of `~/.bashrc`
```
# some useful aliases, not related to CUDA
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
```
-------------------
```
# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# All things that you want to add to the path on login add before this comment!
RVG_PATH=$PATH
```

>## Create if not exists or edit `~/.bash_aliases`

```alias clean-path='export PATH="${RVG_PATH}"'  
alias clear-path='export PATH="${RVG_PATH}"'  
  
alias unset-cuda='export PATH="${RVG_PATH}"'  
alias unset-cudas='export PATH="${RVG_PATH}"'  
alias set-cuda-9-2='export PATH="${RVG_PATH}:/opt/cuda-9.2/bin"'  
alias set-cuda-8-0='export PATH="${RVG_PATH}:/opt/cuda-8.0/bin"'
  
alias gpu-temp="nvidia-smi --query-gpu=temperature.gpu --format=csv,noheader"  
```


>## CUDA installation

1. Download CUDA & CUDNN from https://archive.archlinux.org/packages/c.
2. Install CUDA & CUDNN: `pacman -U cuda-X-Y`.
3. Rename `/opt/cuda` to `/opt/cuda-X.Y`.
4. Uninstall CUDA & CUDNN: `pacman -R cudnn cuda` (first remove cudnn).
----------------
5. Remove file `/etc/profile.d/cuda.sh.`
6. Rename `/etc/ld.so.conf.d/cuda.conf` to `/etc/ld.so.conf.d/cuda-X.Y.conf`, and change content of file to point to correct location. (same for CUDNN).  

Repeat steps 1-4 to install all versions you need. At the end, if you want to have the latest version that will recieve regular updates, you can install it with `pacman -S cuda cudnn`. `pacman` will update only that version.  
Then, you shoud do steps 5 and 6.
After system reboot, you should be able to activate *X.Y* version, simply typing in terminal **set-cuda-X-Y**.
