MODS=r_debug r_reg r_util
LDFLAGS+=$(shell pkg-config --libs ${MODS}) -g
CFLAGS+=$(shell pkg-config --cflags ${MODS}) -g -I/usr/local/include -L/usr/local/lib
W32OBJ=debug_windows.o
include unicorn.mk

CFLAGS+=-fPIC

include ../../../options.mk


all: debug_windows.$(EXT_SO) debug_unicorn.$(EXT_SO)

%.o: %.c
	$(CC) $(CFLAGS) $(LDFLAGS) $(LIBS) -c $< -o $@

debug_windows.$(EXT_SO): $(W32OBJ)
	$(CC) -shared -fPIC $(CFLAGS) -o debug_windows.$(EXT_SO) $(W32OBJ) $(LDFLAGS)

debug_unicorn.$(EXT_SO): $(UNICORN_OBJ)
	$(CC) -shared -fPIC $(CFLAGS) -o debug_unicorn.$(EXT_SO) $(UNICORN_LDFLAGS) $(LDFLAGS)

install:
	mkdir -p ~/.config/radare2/plugins/
	cp debug_unicorn.${EXT_SO} ~/.config/radare2/plugins/

uninstall:
	rm ~/.config/radare2/plugins/debug_unicorn.${EXT_SO} 

clean:
	rm *.$(EXT_SO) *.o
