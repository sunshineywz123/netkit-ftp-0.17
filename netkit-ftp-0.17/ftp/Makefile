all: ftp

include ../MCONFIG
include ../MRULES

ifeq ($(USE_READLINE),1)
CFLAGS += -D__USE_READLINE__
LIBS += -lreadline $(LIBTERMCAP)
endif

ftp: cmds.o cmdtab.o domacro.o ftp.o glob.o main.o ruserpass.o
	$(CC) $(LDFLAGS) $^ $(LIBS) -o $@

domacro.o ftp.o glob.o main.o ruserpass.o: ftp_var.h pathnames.h
cmds.o cmdtab.o: ftp_var.h pathnames.h cmds.h
cmds.o glob.o: glob.h

install: ftp
	mkdir -p $(DESTDIR)$(BINDIR) $(DESTDIR)$(MANDIR)/man{1,5}
	install -m$(BINMODE) ftp $(DESTDIR)$(BINDIR)
	cd $(DESTDIR)$(BINDIR)/ && ln -sf ftp pftp
	install -m$(MANMODE) ftp.1 $(DESTDIR)$(MANDIR)/man1
	cd $(DESTDIR)$(MANDIR)/man1 && ln -sf ftp.1 pftp.1
	install -m$(MANMODE) netrc.5 $(DESTDIR)$(MANDIR)/man5

clean:
	rm -f *.o ftp

