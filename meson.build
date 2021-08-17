project('cimgui', 'c', 'cpp')

sdl2_dep = dependency('sdl2')
freetype2_dep = dependency('freetype2')
glad_dep = subproject('glad').get_variable('glad_dep')

add_project_arguments(
  '-DIMGUI_USER_CONFIG="_cimgui_config.h"',
  language : 'cpp',
)

imgui_src = files(
  'imgui/imgui.cpp',
  'imgui/imgui_demo.cpp',
  'imgui/imgui_draw.cpp',
  'imgui/imgui_tables.cpp',
  'imgui/imgui_widgets.cpp',
  'imgui/misc/freetype/imgui_freetype.cpp',
)

imgui_lib = library('imgui',
  imgui_src,
  dependencies : [freetype2_dep],
  include_directories : include_directories('imgui'),
)

imgui_dep = declare_dependency(
  link_with : imgui_lib,
  include_directories : include_directories('imgui'),
)

imgui_sdl_src = files(
  'imgui/backends/imgui_impl_sdl.cpp',
)

imgui_sdl_lib = library('imgui-sdl',
  imgui_sdl_src,
  dependencies : [imgui_dep, sdl2_dep],
  include_directories : include_directories('imgui/backends'),
)

imgui_sdl_dep = declare_dependency(
  link_with : imgui_sdl_lib,
  include_directories : include_directories('imgui/backends'),
)

imgui_gl3_src = files(
  'imgui/backends/imgui_impl_opengl3.cpp',
)

imgui_gl3_lib = library('imgui-gl3',
  imgui_gl3_src,
  dependencies : [imgui_dep, glad_dep],
  cpp_args : ['-DIMGUI_IMPL_OPENGL_LOADER_GLAD2'],
  include_directories : include_directories('imgui/backends'),
)

imgui_gl3_dep = declare_dependency(
  link_with : imgui_gl3_lib,
  include_directories : include_directories('imgui/backends'),
)

cimgui_src = files(
  'cimgui.cpp',
)

cimgui_lib = library('cimui',
  cimgui_src,
  dependencies : [imgui_dep, imgui_sdl_dep, imgui_gl3_dep],
  include_directories : include_directories('.'),
)

cimgui_dep = declare_dependency(
  link_with : cimgui_lib,
  include_directories : include_directories('.'),
)

