conf_data = configuration_data()
conf_data.set('PROJECT_VER', '0.2.0')
conf_data.set('PROJECT_VER_MAJOR', 0)
conf_data.set('PROJECT_VER_MINOR', 2)
conf_data.set('LIBFREENECT2_WITH_CXX11_SUPPORT', true)
conf_data.set('LIBFREENECT2_THREADING_STDLIB', true)

if glfw_dep.found()
    conf_data.set('LIBFREENECT2_WITH_OPENGL_SUPPORT', true)
endif
if jpegturbo_dep.found()
    conf_data.set('LIBFREENECT2_WITH_TURBOJPEG_SUPPORT', true)
endif

configure_file(input: 'config.h.in',
               format: 'cmake@',
               output: 'config.h',
               configuration: conf_data)

