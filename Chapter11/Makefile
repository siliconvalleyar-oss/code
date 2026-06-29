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

# SDL2_ttf
SDL2_TTF_CFLAGS := $(shell pkg-config --cflags SDL2_ttf 2>/dev/null)
SDL2_TTF_LIBS := $(shell pkg-config --libs SDL2_ttf 2>/dev/null)
ifeq ($(SDL2_TTF_CFLAGS),)
SDL2_TTF_CFLAGS := -I/tmp/opencode/sdl2_ttf/root/usr/include/SDL2
SDL2_TTF_LIBS := /tmp/opencode/sdl2_ttf/root/usr/lib/x86_64-linux-gnu/libSDL2_ttf.a
endif
CXXFLAGS += $(SDL2_TTF_CFLAGS)
LIBS += $(SDL2_TTF_LIBS)

# SOIL
SOIL_DIR := ../External/SOIL
CXXFLAGS += -I$(SOIL_DIR)/include
LIBS += $(SOIL_DIR)/lib/linux/libSOIL.a

# rapidjson (header-only)
CXXFLAGS += -I../External/rapidjson/include

# FMOD (if available)
ifneq ($(wildcard ../External/FMOD/api/inc),)
FMOD_DIR := ../External/FMOD/api
CXXFLAGS += -I$(FMOD_DIR)/inc
LIBS += -L$(FMOD_DIR)/lib -lfmodstudio -lfmod
endif

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
