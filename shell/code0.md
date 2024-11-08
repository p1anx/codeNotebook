# 1 获取脚本函数所在的文件夹的位置
```shell
function rofi_config() {
  if ! command -v rofi >/dev/null 2>&1; then
    if grep -q "arch" /etc/os-release; then
      sudo pacman -S rofi-wayland
    fi
  fi

  if [ ! -d ~/.config/rofi ]; then
    mkdir ~/.config/rofi
  else
    mv ~/.config/rofi ~/.config/rofi.bak
    mkdir ~/.config/rofi
  fi
#==================================================================
  # 获取脚本文件所在的目录
  local script_dir=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
  echo "脚本所在的目录是: $script_dir"
#==================================================================
  cp "$script_dir/config.rasi" ~/.config/rofi/
}

rofi_config
```
# 2 设置shell输出文字颜色
```
# Set some colors for output messages
OK="$(tput setaf 2)[OK]$(tput sgr0)"
ERROR="$(tput setaf 1)[ERROR]$(tput sgr0)"
NOTE="$(tput setaf 3)[NOTE]$(tput sgr0)"
INFO="$(tput setaf 4)[INFO]$(tput sgr0)"
WARN="$(tput setaf 5)[WARN]$(tput sgr0)"
CAT="$(tput setaf 6)[ACTION]$(tput sgr0)"
ORANGE=$(tput setaf 166)
YELLOW=$(tput setaf 3)
BLUE=$(tput setaf 4) 
RESET=$(tput sgr0)

echo "$OK hello"
```
