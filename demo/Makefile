
all: simple.exe signals.exe use-module.exe shadow.exe hash.exe print-host.cc


C++ = g++
C++-FLAGS = -g -Wall

#C++ = CC
#C++-FLAGS = -g

C++-FLAGS += -I..
LINK-FLAGS = -g

PERL = perl
PERL-EMBED = -MExtUtils::Embed
PERL-INCS = `$(PERL) $(PERL-EMBED) -e ccopts`
PERL-LINKAGE = `$(PERL) $(PERL-EMBED) -e ldopts`

PERL-GLUE = ../perl-glue.o xsinit.o

xsinit.c:
	$(PERL) $(PERL-EMBED) -e xsinit -- -o xsinit.c

xsinit.o: xsinit.c
	$(C++) $(C++-FLAGS) $(PERL-INCS) -c -o $@ $<

../perl-glue.o:
	(cd ..; make perl-glue.o)

clean:
	/bin/rm -f \#* *.o *.exe xsinit.c


%.o: %.cc
	$(C++) $(C++-FLAGS) -c -o $@ $<

%.exe: %.o $(PERL-GLUE)
	$(C++) $(LINK-FLAGS) -o $@ $+ $(PERL-LINKAGE)
