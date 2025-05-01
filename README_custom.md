# Fastfetch Custom Build with Arch & Penguin ASCII Logo

This repository contains instructions and configuration for building Fastfetch from source, including a custom ASCII logo that combines the Arch Linux logo and a Linux penguin, with multi-color support.

```bash
                       : "If it ain't broke, don't fix it" - Lucascito_03
                    ┌──────────────────────────────────────────┐
        .             󰇺 Chassis : Desktop  
       / \            󰣇 OS : Arch Linux
      /^  \            Kernel : 6.14.4-arch1-1
     /  _  \          󰏗 Packages : 1581 (pacman), 39 (flatpak-user)
    /  | | ~\         󰍹 Display : 1920x1080 @ 165Hz [External]
   /.-'   '-.\         Terminal : code-insiders 1.100.0-insider
                      󱗃 WM : Hyprland
                    └──────────────────────────────────────────┘

                       : xgen0 @ arch-home
                    ┌──────────────────────────────────────────┐
     .--.              CPU : AMD Ryzen 5 7600X @ 5.46 GHz
    |o_o |            󰊴 GPU : AMD Raphael
    |:_/ |            󰊴 GPU : NVIDIA GeForce RTX 4060
   //   \ \            GPU Driver : amdgpu
  (|     | )           GPU Driver : nvidia (proprietary) 570.144
 /'\_   _/`\           Memory  : 8.48 GiB / 30.51 GiB (28%)
 \___)=(___/          󱦟 OS Age  : 98 days
                      󱫐 Uptime  : 1 day, 10 hours, 35 mins
                    └──────────────────────────────────────────┘
                      ● ● ● ● ● ● ● ●
```

## Features

- Custom ASCII logo with color placeholders ($1, $2, $3, $4)
- Example `config.jsonc` for Fastfetch
- Step-by-step build and usage instructions

---

## 1. Prerequisites

- CMake
- GCC or Clang
- git

Install on Arch/Manjaro:

```sh
sudo pacman -S cmake gcc git
```

Install on Debian/Ubuntu:

```sh
sudo apt install cmake build-essential git
```

---

## 2. Clone Fastfetch Source

```sh
git clone https://github.com/fastfetch-cli/fastfetch.git
cd fastfetch
```

---

## 3. Add or Edit Your Custom ASCII Logo

- Go to the ASCII logo directory:

  ```sh
  cd src/logo/ascii/
  ```

- Create or edit `arch_penguin.txt`:

  ```sh
  nano arch_penguin.txt
  ```

- Example content (with color placeholders):

  ```bash
    $1        .       
        / \      
        /^  \     
        /  _  \    
        /  | | ~\   
    /.-'   '-.\  

    $2   .--.  
    $3  |o_o | 
    |:_/ | 
    //   \\ \\ 
    (|     | )
    $4 /'\\_   _/`\\
    $1 \\___)=(___/
  ```

---

## 4. Build Fastfetch

From the project root:

```sh
mkdir -p build
cd build
cmake ..
cmake --build . --target fastfetch -j$(nproc)
```

Or use the provided script:

```sh
./run.sh
```

---

## 5. Install Fastfetch (Optional)

```sh
sudo make install
```

Or with CMake:

```sh
sudo cmake --install build
```

---

## 6. Configure Fastfetch

Edit `~/.config/fastfetch/config.jsonc`:

```jsonc
"logo": {
  "source": "/home/xgen0/fastfetch/src/logo/ascii/arch_penguin.txt",
  "padding": { "top": 2 },
  "color": {
    "1": "cyan",
    "2": "black",
    "3": "white",
    "4": "yellow"
  }
}
```

---

## 7. Run Fastfetch

If installed system-wide:

```sh
fastfetch
```

Or from the build directory:

```sh
cd ~/fastfetch/build
./fastfetch
```

---

## 8. Troubleshooting

- If you see `Logo: Failed to load / convert the image source`, check:
  - The file path and permissions
  - The file is plain ASCII (no BOM, no Windows line endings)
  - Try placing the logo in `~/.config/fastfetch/` and referencing it by filename only
- For more info, see [fastfetch-cli/fastfetch#1191](https://github.com/fastfetch-cli/fastfetch/discussions/1191)

---

## 9. Use a Local Build Without Installing

Add this to your `~/.zshrc` for convenience:

```sh
alias fastfetch="$HOME/fastfetch/build/fastfetch"
```

---

## License

See [LICENSE](LICENSE) for details.

---

## Credits

- [Fastfetch](https://github.com/fastfetch-cli/fastfetch)
- Custom ASCII art by @xgen0
