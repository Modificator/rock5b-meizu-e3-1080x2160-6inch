# 指定内核源码路径
KERNEL_DIR := /lib/modules/$(shell uname -r)/build
# 或指定绝对路径
# KERNEL_DIR := /usr/src/linux-headers-$(shell uname -r)

# 指定要编译的模块
obj-m += sec_ts.o

sec_ts-objs += sec_ts_main.o sec_ts_fw.o sec_ts_fn.o sec_ts_selftest.o

ccflags-y += -Wno-error=unused-label -Wno-error=unused-function -Wno-unused-label -Wno-unused-function
ccflags-y += -Wno-error=unused-variable -Wno-unused-variable
#ccflags-y += -std=gnu90

ccflags-y += -Wno-vla
# 指定源文件（如果模块有多个源文件）
# mymodule-objs := main.o helper.o

PWD := $(shell pwd)

all:
	make -C $(KERNEL_DIR) M=$(PWD) modules

clean:
	make -C $(KERNEL_DIR) M=$(PWD) clean

install:
	sudo cp sec_ts.ko /lib/modules/$(shell uname -r)/
	sudo depmod -a
	echo sec_ts | sudo tee -a /etc/modules