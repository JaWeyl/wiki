# Usage:
# make 				# compile all binary
# make clean 	# remove all binaries and objects

.PHONY = all clean

CC = gcc
LINKERFLAG = -lm

SRCS := foo.c
BINS := foo

all: foo

foo: foo.o
	@echo "Checking..."
	${CC} ${LINKERFLAG} foo.o -o foo

foo.o: foo.c
	@echo "Creating object..."
	${CC} -c foo.c

clean:
	@echo "Cleaning up..."
	rm -rvf foo.o foo