# Projeto de exemplo para uso do GenICam com C++ e Python
project('Aplicação', 'cpp', default_options : ['cpp_std=c++20'])

# Inicia as flags de compilação como um vetor vazio
cpp_args = []

# Adiciona flags de compilação para o GCC e Clang
cc = meson.get_compiler('cpp')
if cc.get_id() == 'g++' or cc.get_id() == 'clang++'
  cpp_args += '-Wno-deprecated'
endif

# Importa as dependências e pastas de cabeçalho
inc = include_directories('include', '/usr/local/include', 'libs/freeimage')

# Importa os arquivos de código fonte
app_src = files(
 'src/main.cpp',
 'src/App.cpp',
 'src/Camera.cpp',
 'src/Color.cpp',
 'src/Coordinate2D.cpp',
 'src/Coordinate3D.cpp',
 'src/Helpers.cpp',
 'src/Object.cpp',
 'src/Shapes.cpp',
 'src/Utils.cpp'
)

# Local para importar as dependencias
compiler = meson.get_compiler('cpp')

# Local para importar as dependencias
openGL_dep = dependency('gl')
gluL_dep = dependency('glu')
glut_dep = dependency('glut', required: false)
freeimage_dep = dependency('freeimage', required: false)


libsPath = '/usr/lib/x86_64-linux-gnu/'
if not glut_dep.found()
  glut_dep = compiler.find_library('glut', dirs: libsPath)
endif

if not freeimage_dep.found()
  path = meson.current_source_dir() + '/libs/freeimage/libfreeimage.a'
  freeimage_dep = declare_dependency(link_args: path)
endif

# Aplicação Central
executable('main', 
    sources : [
      app_src
    ], 
    include_directories : inc, 
    dependencies: [
      openGL_dep, 
      glut_dep, 
      gluL_dep, 
      freeimage_dep
    ],
    install: true, 
    cpp_args : cpp_args
  )