MAINSOURCE := Main.cpp base/tests/LoggingTest.cpp tests/HTTPClient.cpp
SOURCE  := $(wildcard *.cpp base/*.cpp tests/*.cpp) # 展开为已经存在的、使用空格分开的、匹配此模式的所有文件列表ß
override SOURCE := $(filter-out $(MAINSOURCE),$(SOURCE)) # filter pattern,text 过滤掉text中符合pattern的
OBJS    := $(patsubst %.cpp,%.o,$(SOURCE)) # patsubst 目标模式,源模式,文件列表

TARGET  := WebServer
CC      := g++
LIBS    := -lpthread
INCLUDE:= -I./usr/local/lib
CFLAGS  := -std=c++11 -g -Wall -O3 -D_PTHREADS
CXXFLAGS:= $(CFLAGS)

# Test object
SUBTARGET1 := LoggingTest
SUBTARGET2 := HTTPClient

.PHONY : objs clean veryclean rebuild all tests debug
all : $(TARGET) $(SUBTARGET1) $(SUBTARGET2)
objs : $(OBJS)
rebuild: veryclean all

tests : $(SUBTARGET1) $(SUBTARGET2)
clean :
	find . -name '*.o' | xargs rm -f
veryclean :
	find . -name '*.o' | xargs rm -f
	find . -name $(TARGET) | xargs rm -f
	find . -name $(SUBTARGET1) | xargs rm -f
	find . -name $(SUBTARGET2) | xargs rm -f
debug:
	@echo $(SOURCE)

$(TARGET) : $(OBJS) Main.o
	$(CC) $(CXXFLAGS) -o $@ $^ $(LDFLAGS) $(LIBS)

$(SUBTARGET1) : $(OBJS) base/tests/LoggingTest.o
	$(CC) $(CXXFLAGS) -o $@ $^ $(LDFLAGS) $(LIBS)

$(SUBTARGET2) : $(OBJS) tests/HTTPClient.o
	$(CC) $(CXXFLAGS) -o $@ $^ $(LDFLAGS) $(LIBS)

