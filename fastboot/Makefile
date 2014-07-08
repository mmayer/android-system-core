CFLAGS?=-O2 -Wall

CPPFLAGS+=-I. \
	-I../include \
	-I../mkbootimg \
	-I../../android_core/libsparse/include \
	-I../../android-system-extras/ext4_utils

LDLIBS=../../android_core/libsparse/libsparse.a \
	../../android_core/libzipfile/libzipfile.a \
	../../android-system-extras/ext4_utils/make_ext4fs.o \
	../../android-system-extras/ext4_utils/allocate.o \
	../../android-system-extras/ext4_utils/ext4_utils.o \
	../../android-system-extras/ext4_utils/ext4_sb.o \
	../../android-system-extras/ext4_utils/crc16.o \
	../../android-system-extras/ext4_utils/uuid.o \
	../../android-system-extras/ext4_utils/sha1.o \
	../../android-system-extras/ext4_utils/extent.o \
	../../android-system-extras/ext4_utils/indirect.o \
	../../android-system-extras/ext4_utils/contents.o \
	-lz

fastboot_src_files := \
	protocol.c \
	engine.c \
	bootimg.c \
	fastboot.c \
	util.c \
	fs.c

ifeq ($(shell uname -s),Darwin)
	fastboot_src_files += usb_osx.c util_osx.c
	LDLIBS += -lpthread -framework CoreFoundation -framework IOKit \
		-framework Carbon
endif

fastboot_src_obj := $(fastboot_src_files:.c=.o)

all: fastboot

fastboot: $(fastboot_src_obj)

.PHONY: clean
clean:
	rm -rf *.o fastboot
