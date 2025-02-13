
# **Installing and Using XC8 Compiler on Linux (WSL)**  

## **1. Install XC8 Compiler**  
```bash
# Navigate to the directory where the installer is downloaded
cd Downloads

# Give execution permission to the installer
chmod +x xc8-v3.00-full-install-linux-x64-installer.run

# Run the installer with sudo
sudo ./xc8-v3.00-full-install-linux-x64-installer.run
```

---

## **2. Add XC8 Compiler to System Path**  
```bash
# Open the shell configuration file (use ~/.zshrc if you use zsh)
nano ~/.bashrc

# Add the following line at the end of the file
export PATH=$PATH:/opt/microchip/xc8/v3.00/bin

# Apply changes
source ~/.bashrc  # Or use source ~/.zshrc if using zsh
```

---

## **3. Verify Installation**  
```bash
xc8-cc --version
```

---

## **4. Create `input.c` and `Makefile`**  

### **Create `input.c` File**  
```c
#include <pic.h>

void main() {
// your desire code 
}
```

---

### **Create `Makefile`**  
```makefile
CC = /opt/microchip/xc8/v3.00/bin/xc8-cc
CHIP = -mcpu=16F84A -traditional
SRC = input.c
HEX = main.hex
WIN_DIR = /mnt/c/Users/aryan/Desktop # Change to your actual Windows directory

transfer: $(HEX)
	cp $(HEX) $(WIN_DIR)  # Transfer HEX file to Windows

all: $(HEX)
$(HEX): $(SRC)
	$(CC) $(CHIP) $(SRC) -o $(HEX)

clean:
	rm -rf $(HEX) __eeprom.* main.* startup.* *.o *.p1 *.d *.cmf *.elf *.hxl *.sdb *.lst *.rlf *.sym
```

---

## **5. Compile and Clean and transfer**  
### **To compile**  
```bash
make
```

### **To clean the directory**  
```bash
make clean
```

---

## **6. Transfer HEX File to Windows**  
```bash
make transfer
```

