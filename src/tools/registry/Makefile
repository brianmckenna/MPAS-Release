.SUFFIXES: .c .o

EZXML_PATH= ../../external/ezxml

OBJS = parse.o dictionary.o gen_inc.o fortprintf.o utility.o

all: ezxml parse
	($(MAKE) parse CPPFLAGS="$(CPPFLAGS)" CPPINCLUDES="$(CPPINCLUDES)")

ezxml:
	(cd $(EZXML_PATH); $(MAKE) CFLAGS="$(CFLAGS) $(TOOL_TARGET_ARCH)")

parse: ezxml $(OBJS)
	$(CC) $(CPPFLAGS) $(EZXML_PATH)/ezxml.o  -I$(EZXML_PATH) -o $@ $(OBJS)

clean:
	$(RM) *.o parse
	@# Certain systems with intel compilers generate *.i files
	@# This removes them during the clean process
	$(RM) *.i

.c.o: ezxml
	$(CC) $(TOOL_TARGET_ARCH) $(CFLAGS) $(CPPFLAGS) -I$(EZXML_PATH) -c $<
