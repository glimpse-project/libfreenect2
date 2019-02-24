project('freenect2', ['c', 'cpp'], version: '0.2.0')

cc = meson.get_compiler('cpp')
compiler_id = cc.get_id()

math_dep = cc.find_library('m', required: false)
threads_dep = dependency('threads')

subdir('tools')

libusb_dep = dependency('libusb-1.0', required: true)
jpegturbo_dep = dependency('libturbojpeg', required: true)

glfw_dep = dependency('glfw3')

if glfw_dep.found()
flextGL_lib = static_library('flextGL', ['src/flextGL.cpp'],
                             include_directories: include_directories('src'))

flextGL_link_args = []
if host_machine.system() == 'darwin'
    flextGL_link_args += [
        '-framework', 'OpenGL',
        '-framework', 'CoreGraphics',
        '-framework', 'QuartzCore',
    ]
endif

flextGL_dep = declare_dependency(link_with: flextGL_lib,
                                 include_directories: include_directories('src'),
                                 link_args: flextGL_link_args)
endif

fn2_defines = []
fn2_c_args = []
fn2_cpp_args = [ '-std=c++11' ]
fn2_link_args = []
fn2_inc = include_directories('include', 'include/internal')
fn2_deps = [ libusb_dep, jpegturbo_dep, math_dep, threads_dep ]

fn2_src = [
    'src/transfer_pool.cpp',
    'src/event_loop.cpp',
    'src/usb_control.cpp',
    'src/allocator.cpp',
    'src/frame_listener_impl.cpp',
    'src/packet_pipeline.cpp',
    'src/rgb_packet_stream_parser.cpp',
    'src/rgb_packet_processor.cpp',
    'src/depth_packet_stream_parser.cpp',
    'src/depth_packet_processor.cpp',
    'src/cpu_depth_packet_processor.cpp',
    'src/resource.cpp',
    'src/command_transaction.cpp',
    'src/registration.cpp',
    'src/logging.cpp',
    'src/libfreenect2.cpp',
]

if glfw_dep.found()
fn2_src += [
    'src/opengl_depth_packet_processor.cpp'
]
fn2_deps += [
    glfw_dep,
    flextGL_dep
]
endif

if jpegturbo_dep.found()
fn2_src += [
    'src/turbo_jpeg_rgb_packet_processor.cpp'
]
endif


subdir('include/libfreenect2')


fn2_lib = library('freenect2', fn2_src,
                  cpp_args: fn2_defines + fn2_cpp_args,
                  c_args: fn2_defines + fn2_c_args,
                  link_args: fn2_link_args,
                  include_directories: fn2_inc,
                  dependencies: fn2_deps)
fn2_dep = declare_dependency(link_with: fn2_lib,
                             include_directories: include_directories('include'))

subdir('examples')
