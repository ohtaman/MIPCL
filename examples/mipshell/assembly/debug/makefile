CC=g++
ARC=-mfpmath=sse -msse2
CFLAGS=-c -std=c++17 -fno-rtti -g $(ARC) -I$(HDR_MIPSHELL) -I$(HDR_MIPCL)
LDFLAGS=-shared-libgcc
#
INS=install
MIP_DIR=$(MIPCLDIR)
INSDIR=$(MIP_DIR)/examples/bin
RM=rm -f
CFLAGS+=-DMIPSHELL_API="" -DMIP_API=""
LDFLAGS+= -L$(MIP_DIR)/lib -lmipcl -lmipshell
TARGET=assembly_dbg
#
HDR_MIPCL=$(MIP_DIR)/mipcl/headers
HDR_MIPSHELL=$(MIP_DIR)/mipshell/headers
#
VPATH=../sources
CFLAGS+=-I$(VPATH)
MOD= $(shell echo $(VPATH)/*.mod)
AUX=$(MOD:.mod=.aux)
SRC=$(notdir $(shell echo $(VPATH)/*.cpp))
OBJS=$(SRC:.cpp=.o)
#
.cpp.o:
	$(CC) $(CFLAGS) $< -o $@
%.aux : %.mod ;	$(MIP_DIR)/bin/mod2cpp $< $(<D)/$@
#
build: $(OBJS) 
	$(CC) $(LDFLAGS) $(OBJS) -o $(TARGET)
#dependencies
assembly.cpp: assembly.mod 
assembly.o: assembly.cpp assembly.aux assembly.h
main.o: main.cpp assembly.h
#
.PHONY: clean
clean:
	$(RM) $(OBJS) $(AUX)
install: $(TARGET)
	$(INS) $(TARGET) $(INSDIR)
	$(RM) $(TARGET)
all: build install
