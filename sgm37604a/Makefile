# 指定内核源码路径
KERNEL_DIR := /lib/modules/$(shell uname -r)/build
# 或指定绝对路径
# KERNEL_DIR := /usr/src/linux-headers-$(shell uname -r)

# 指定要编译的模块
obj-m += sgm37604a.o

# 指定源文件（如果模块有多个源文件）
# mymodule-objs := main.o helper.o

PWD := $(shell pwd)

all:
	make -C $(KERNEL_DIR) M=$(PWD) modules

clean:
	make -C $(KERNEL_DIR) M=$(PWD) clean
	
install:
	sudo cp sgm37604a.ko /lib/modules/$(shell uname -r)/
	sudo depmod -a
	echo sgm37604a | sudo tee -a /etc/modules