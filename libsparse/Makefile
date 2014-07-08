CFLAGS?=-O2 -Wall -fPIC

CPPFLAGS+=-I. \
	-I../../android_core/include \
	-I../../android_core/libsparse/include \
	-I../../android_external/libselinux/include

LDLIBS+=-lz

libsparse_src_files := \
        backed_block.c \
        output_file.c \
        sparse.c \
        sparse_crc32.c \
        sparse_err.c \
        sparse_read.c

ifeq ($(shell uname -s),Darwin)
	SPARSE_LDLIBS=-lz
endif

libsparse_src_obj := $(libsparse_src_files:.c=.o)

all: libsparse.a libsparse.so simg2img

libsparse.a: $(libsparse_src_obj)
	$(AR) r $@ $^

libsparse.so: $(libsparse_src_obj)
	$(CC) $^ -shared -o $@ $(SPARSE_LDLIBS)

simg2img: simg2img.c libsparse.a

.PHONY: clean
clean:
	rm -rf *.o *.a *.so simg2img
