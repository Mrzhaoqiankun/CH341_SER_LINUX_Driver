# CONFIG_MODULE_SIG=n

# ifeq ($(KERNELRELEASE), )
# KERNELDIR := /lib/modules/$(shell uname -r)/build
# PWD :=$(shell pwd)
# default:
#       $(MAKE) -C $(KERNELDIR)  M=$(PWD)
# clean:
#       rm -rf *.mk .tmp_versions Module.symvers *.mod.c *.o *.ko .*.cmd Module.markers modules.order *.a *.mod
# load:
#       insmod ch341.ko
# unload:
#       rmmod ch341
# install: default
#       rmmod ch341 || true
#       insmod ch341.ko || true
#       mkdir -p /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ || true
#       cp -f ./ch341.ko /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ || true
#       depmod -a
# uninstall:
#       rmmod ch341 || true
#       rm -rf /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ch341.ko || true
#       depmod -a
# else
#       obj-m := ch341.o
# endif


# --------------------------------------------------------------------
# CH341 内核模块交叉编译 Makefile
# --------------------------------------------------------------------

# 设置交叉编译前缀和架构
CROSS_COMPILE = /home/rk3506/HZ-EVM-RK3506_MINI_SDK/prebuilts/gcc/linux-x86/arm/gcc-arm-10.3-2021.07-x86_64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-
ARCH = arm

# 当前模块名字
obj-m := ch341.o

# 内核源码路径（请改成你开发板内核源码路径）
KERNEL_DIR = /home/rk3506/HZ-EVM-RK3506_MINI_SDK/kernel

# 输出目录
OUTPUT_DIR := $(PWD)/output

# 默认目标
all:
	@echo "==> 编译 CH341 内核模块..."
	# 创建输出目录
	@mkdir -p $(OUTPUT_DIR)
	# 编译模块
	$(MAKE) -C $(KERNEL_DIR) M=$(CURDIR) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) modules
	# 拷贝生成的 .ko 到 output
	@cp -v *.ko $(OUTPUT_DIR)/

# 清理
clean:
	@echo "==> 清理 CH341 模块编译文件"
	@rm -rf \
	*.o \
	*.ko \
	*.mod.c \
	*.mod \
	*.symvers \
	modules.order \
	.*.cmd \
	.tmp_versions \
	$(OUTPUT_DIR)


.PHONY: all clean
