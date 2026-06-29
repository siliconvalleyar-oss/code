# Compilación del proyecto "Game Programming in C++"

## Estructura de cada capítulo

Cada capítulo (Chapter01 a Chapter14) sigue esta estructura:

```
ChapterXX/
├── include/       # Archivos de cabecera (.h)
├── src/           # Archivos fuente (.cpp)
├── obj/           # Objetos compilados (generado)
├── bin/           # Ejecutable final (generado)
├── Assets/        # Recursos visuales/auditivos (si aplica)
├── Shaders/       # Shaders GLSL (si aplica)
├── Makefile       # Build con make
├── CMakeLists.txt # Build con CMake (Chapter01-02)
└── .gitignore
```

## Requisitos

### Dependencias base (todos los capítulos)
- **SDL2** - `libsdl2-dev`
- **Compilador** - `g++` con soporte C++17
- **CMake** (opcional, para Chapter01-02)
- **make**

### Capítulos 01-04
- SDL2
- SDL2_image (`libsdl2-image-dev`)

### Capítulos 05-06, 08
- SDL2
- GLEW (`libglew-dev`)
- SOIL (incluido en `External/SOIL/`)
- rapidjson (header-only, incluido en `External/rapidjson/`)
- OpenGL

### Capítulos 07, 09-14
Todo lo anterior más:
- **FMOD Studio API 1.09.x** - Requiere descarga manual desde
  https://www.fmod.com/download. Instalar en `External/FMOD/api/`.
- SDL2_ttf (Chapter11-14) - `libsdl2-ttf-dev`

## Compilación

### Con Make (recomendado)

```bash
cd ChapterXX
make        # Compila todo
make clean  # Limpia objetos y binarios
```

El ejecutable se genera en `bin/app`.

### Con CMake (Chapter01-02)

```bash
cd ChapterXX
mkdir build && cd build
cmake ..
make
```

## Capítulos compilados exitosamente

| Capítulo | Estado | Dependencias |
|----------|--------|-------------|
| Chapter01 | ✅ Listo | SDL2 |
| Chapter02 | ✅ Listo | SDL2, SDL2_image |
| Chapter03 | ✅ Listo | SDL2, SDL2_image |
| Chapter04 | ✅ Listo | SDL2, SDL2_image |
| Chapter05 | ✅ Listo | SDL2, GLEW, SOIL |
| Chapter06 | ✅ Listo | SDL2, GLEW, SOIL, rapidjson |
| Chapter07 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, **FMOD** |
| Chapter08 | ✅ Listo | SDL2, GLEW, SOIL |
| Chapter09 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, **FMOD** |
| Chapter10 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, **FMOD** |
| Chapter11 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, SDL2_ttf, **FMOD** |
| Chapter12 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, SDL2_ttf, **FMOD** |
| Chapter13 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, SDL2_ttf, **FMOD** |
| Chapter14 | ❌ Requiere FMOD | SDL2, GLEW, SOIL, rapidjson, SDL2_ttf, **FMOD** |

## Instalación de dependencias (Ubuntu/Debian)

```bash
sudo apt-get update
sudo apt-get install -y \
  build-essential \
  cmake \
  libsdl2-dev \
  libsdl2-image-dev \
  libsdl2-ttf-dev \
  libglew-dev
```

Para FMOD, descargar manualmente desde:
https://www.fmod.com/download
