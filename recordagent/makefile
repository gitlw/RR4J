# compiler
CC = g++

OS := $(shell uname)

# all headers files
INCLUDES = /includes

# compiler flags
CFLAGS = -I$(INCLUDES)/ -g -fPIC -fno-omit-frame-pointer -fno-strict-aliasing -std=c++11

# agent name
AGENT = recordagent.cpp

#File compilations
all: cleanObj cleanTgt createTgt objectsGenerate copyToTarget generateAgent createSharedLib

clean: cleanObj cleanTgt

cleanObj:
	rm -f *.o rm -f *.so rm -f *.dylib

cleanTgt:
	rm -rf target

createTgt:
	mkdir target

objectsGenerate:
	$(CC) $(CFLAGS) -c core/*.cpp

copyToTarget:
	mv *.o ./target/

generateAgent:
	$(CC) $(CFLAGS) -c -o recordagent.o recordagent.cpp target/*.o

createSharedLib:
ifeq ($(OS),Darwin)
	$(CC) $(CFLAGS) -dynamiclib -o librecordagent.dylib recordagent.o target/*.o
else
	$(CC) $(CFLAGS) -shared -o librecordagent.so recordagent.o target/*.o
endif
