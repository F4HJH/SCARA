## sources
SRCS_PI = main.c
SRCS_UNIVERSAL = error.c file.c gpio.c task.c task_gpio.c
SRCS = $(SRCS_PI)

## objects
OBJS_PI = $(SRCS_PI:.c=.o)
OBJS_UNIVERSAL = $(SRCS_UNIVERSAL:.c=.o)
OBJS = $(SRCS:.c=.o)

## output
BINS = pi

DEFINES = -DUSE_GPIO
CFLAGS = -Wall -std=gnu99 -funsigned-char -funsigned-bitfields -ffunction-sections -fpack-struct -fshort-enums -I. $(DEFINES)
CFLAGS = -Wall -std=gnu99 -funsigned-char -funsigned-bitfields -ffunction-sections -fpack-struct -I. $(DEFINES)
CFLAGS = -Wall -std=gnu99 -Ofast -mfpu=vfp -mfloat-abi=hard -march=armv6zk -mtune=arm1176jzf-s -I. $(DEFINES)
CFLAGS = -Wall -std=gnu99 -mfpu=vfp -mfloat-abi=hard -march=armv6zk -mtune=arm1176jzf-s -I. $(DEFINES)
CFLAGS = -g -Wall -std=gnu99 -funsigned-char -funsigned-bitfields -ffunction-sections -fpack-struct -I. $(DEFINES)
CC = gcc $(CFLAGS)

all: $(BINS) 

.c.o: Makefile
	$(CC) -c $< -o $@

Makefile.depend:
	touch Makefile.depend

depend: Makefile.depend
	makedepend -fMakefile.depend -- $(CFLAGS) -- $(SRCS)

clean: depend
	rm -f $(ELFS) $(BINS) $(OBJS) $(OBJS_UNIVERSAL)

pi: $(OBJS_PI) $(OBJS_UNIVERSAL)
	$(CC) -o $@ $(OBJS_PI) $(OBJS_UNIVERSAL) -lm -lpthread

test: $(BINS)
	sudo ./pi gpio test 23 65535 5000

include Makefile.depend