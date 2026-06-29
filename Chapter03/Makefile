CXX := g++
CXXFLAGS := -std=c++17 -Wall -Wextra -I include/ -I../External
LDFLAGS :=
LIBS :=

SDL2_CFLAGS := $(shell pkg-config --cflags sdl2)
SDL2_LIBS := $(shell pkg-config --libs sdl2)
SDL2_IMAGE_CFLAGS := $(shell pkg-config --cflags SDL2_image)
SDL2_IMAGE_LIBS := $(shell pkg-config --libs SDL2_image)

CXXFLAGS += $(SDL2_CFLAGS) $(SDL2_IMAGE_CFLAGS)
LIBS += $(SDL2_LIBS) $(SDL2_IMAGE_LIBS)

SRCS := $(shell find src/ -name "*.cpp")
OBJS := $(patsubst src/%.cpp,obj/%.o,$(SRCS))

TARGET := bin/app

.PHONY: all clean

all: $(TARGET)

obj/:
	mkdir -p obj

bin/:
	mkdir -p bin

$(OBJS): | obj/

$(TARGET): | bin/

$(TARGET): $(OBJS)
	$(CXX) $(CXXFLAGS) -o $@ $^ $(LDFLAGS) $(LIBS)

obj/%.o: src/%.cpp
	$(CXX) $(CXXFLAGS) -c -o $@ $<

clean:
	rm -rf obj bin
