CHECKED_DEBUG_FLAGS:= \
	-ggdb \
	-g3 \
	-O2 \
	-pedantic \
	-Wall \
	-Wextra \
	-Wno-long-long \
	-Wconversion \
	-D_FORTIFY_SOURCE=2 \
	-Wformat=2 \
	-Wredundant-decls \
	-Wcast-qual \
	-Wnull-dereference \
	-Wno-deprecated-declarations \
	-Wmissing-declarations \
	-Wmissing-prototypes \
	-Wmissing-noreturn \
	-Wmissing-braces \
	-Wparentheses \
	-Wstrict-aliasing=3 \
	-Wstrict-overflow=2 \
	-Wlogical-op \
	-Wwrite-strings \
	-Wcast-align=strict \
	-Wdisabled-optimization \
	-Wshift-overflow=2 \
	-Wundef \
	-Wshadow \
	-Wmisleading-indentation \
	-Wabsolute-value \
	-Wunused-parameter \
	-Wunused-function

# check_c_compiler_flag("-fstack-protector-all"  HAVE_STACK_PROTECTOR_ALL)
# target_compile_options(${target} PRIVATE -fPIE)
# target_link_options(${target} PRIVATE -fPIE -pie)
# target_link_options(${target} PRIVATE -Wl,-z,relro)
# target_link_options(${target} PRIVATE -Wl,-z,now)
# target_link_options(${target} PRIVATE -Wl,-z,noexecstack)

CC:=gcc
LDLIBS:=-lz -lcurl -lcrypto -lssl -ldl
LDFLAGS:=-pthread
CFLAGS:=$(CHECKED_DEBUG_FLAGS) -fstack-protector-all
CPPFLAGS:=-DHAVE_SYS_MMAN_H -DENABLE_CURL
all: osslsigncode
SOURCES:=$(filter-out applink%,$(wildcard *.c))
OBJDIR:=./obj
OBJECTS:=$(addprefix $(OBJDIR)/,$(SOURCES:.c=.o))
$(OBJECTS): $(OBJDIR)
osslsigncode: $(OBJECTS)
	$(LINK.c) $^ $(LOADLIBES) $(LDLIBS) -o $@

$(OBJDIR)::
	mkdir $(OBJDIR)

obj/%.o: %.c
	$(COMPILE.c) $(OUTPUT_OPTION) $<

clean:
	-rm -rf $(OBJDIR)

rebuild: clean all

.NOTPARALLEL: rebuild
.PHONY: all clean rebuild
