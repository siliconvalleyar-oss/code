CXX := g++
CXXFLAGS := -std=c++17 -Wall -Wextra -I include/
LDFLAGS :=
LIBS :=

SDL2_CFLAGS := $(shell pkg-config --cflags sdl2)
SDL2_LIBS := $(shell pkg-config --libs sdl2)
GLEW_CFLAGS := $(shell pkg-config --cflags glew)
GLEW_LIBS := $(shell pkg-config --libs glew)

CXXFLAGS += $(SDL2_CFLAGS) $(GLEW_CFLAGS)
LIBS += $(SDL2_LIBS) $(GLEW_LIBS)

# SOIL
SOIL_DIR := ../External/SOIL
CXXFLAGS += -I$(SOIL_DIR)/include
LIBS += $(SOIL_DIR)/lib/linux/libSOIL.a

# rapidjson (header-only)
CXXFLAGS += -I../External/rapidjson/include

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
