CC = gcc
src = src
inc = inc
test = test
objdir = obj
lib = 
doxygenFile = doxyfile

RELEASE = assembler.exe

incFiles = $(wildcard $(inc)/*.h)
obj = $(patsubst $(src)%.c, $(objdir)%.o, $(wildcard $(src)/*.c))
objWithoutMain = $(subst $(objdir)/main.o,,$(obj))
testObj = $(patsubst $(test)%.c, $(objdir)%.o, $(wildcard $(test)/*.c))
testExe = $(patsubst $(test)%.c, $(test)%.exe, $(wildcard $(test)/*.c))

help:
	@echo ""
	@echo "Informatique project: MIPS assembler"
	@echo ""
	@echo "Usage:"
	@echo ""
	@echo "make release         => build RELEASE version"
	@echo "make test/test%.exe  => build the test/test%.c file"
	@echo "make allTest         => build build all tests from test directory"
	@echo "make clean           => clean object file from obj directory"
	@echo "make cleanAll        => clean everything"
	@echo "make documentation   => create a documentation"
	@echo ""


$(objdir)/%.o : $(src)/%.c
	$(CC) -c -g -I$(inc) -o $@ $<

$(objdir)/%.o : $(test)/%.c
	$(CC) -c -g -I$(inc) -o $@ $<

release: $(obj)
	$(CC) -o $(RELEASE) $^ $(lib)

$(test)/test%.exe: $(objWithoutMain) $(objdir)/test%.o
	$(CC) -o $@ $^ $(lib)

allTest: $(testExe)
	
documentation : 
	doxygen $(doxygenFile)

clean:
	rm $(objdir)/*.o

cleanAll:
	$(MAKE) clean
	rm -rf *.exe
	rm -rf test/*.exe