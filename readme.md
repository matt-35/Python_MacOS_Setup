# Python Setup for Apple Silicon 

Mac OS is in a transition phase from intel x86 CPUs to Apple Silicon based on ARM. While the default choice might be to setup and install ARM versions of Python, sometimes you might encounter a project that requires intel based python for compatibility. 

This guide acts a complimation of guides that I found on the internet and that I find preferable. 

## Conda Setup 
In this guide we will be installing miniconda twice, both for intel and arm. 

### Intel Setup
1. Download the latest version of miniconda for intel x86. https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh

2. Run the installer using the following command in the file's directory. 

```
sh ./Miniconda3-latest-MacOSX-x86_64.sh
```

3. Continue through the license agrement and type `yes` to continue. 

4. When it asks for an installation path, set your custom path to `/Users/[your user name]/miniconda3-intel`

5. When the prompt asks to intialize with `conda init`, type `no` and press `enter`.

### ARM Setup

1. Download the latest miniconda for arm. https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh

1. Repeat steps 1-5 in the intel section with the arm installer and set your install path to `/Users/[your user name]/miniconda3-arm`.

## Terminal Setup 

Right now, conda is not set to activate in the terminal for either installations. We will need to create two shell scripts that will be used to call each one. 

1. Create two new `.sh` files under your user folder. Name one `py-arm.sh` and the other `py-intel.sh`. 

Copy and paste the following contents into each file:

 - `py-arm.sh`

```sh
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/Users/[your user name]/miniconda3-arm/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/Users/[your user name]/miniconda3-arm/etc/profile.d/conda.sh" ]; then
        . "/Users/[your user name]/miniconda3-arm/etc/profile.d/conda.sh"
    else
        export PATH="/Users/[your user name]/miniconda3-arm/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

- `py-intel.sh`

```sh
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/Users/[your user name]/miniconda3-intel/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/Users/[your user name]/miniconda3-intel/etc/profile.d/conda.sh" ]; then
        . "/Users/[your user name]/miniconda3-intel/etc/profile.d/conda.sh"
    else
        export PATH="/Users/[your user name]/miniconda3-intel/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

## Activation 

To activate an environment, use one of the following commands in the terminal for your desired installation. 

```
# ARM
source ~/py-arm.sh 
# Intel
source ~/py-intel.sh
```
