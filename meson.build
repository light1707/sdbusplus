project('sdbusplus', 'cpp', 'c',
    default_options: [
      'buildtype=debugoptimized',
      'cpp_std=c++17',
      'werror=true',
    ],
    version: '1.0.0',
)

libsystemd_pkg = dependency('libsystemd')
root_inc = include_directories('include')

libsdbusplus_src = files(
    'src/exception.cpp',
    'src/sdbus.cpp',
    'src/server/transaction.cpp',
)

libsdbusplus = library(
    'sdbusplus',
    libsdbusplus_src,
    include_directories: root_inc,
    dependencies: libsystemd_pkg,
    version: meson.project_version(),
    install: true,
)

sdbusplus_dep = declare_dependency(
    include_directories: root_inc,
    link_with: libsdbusplus,
    dependencies: libsystemd_pkg
)

subdir('tools')

boost_dep = dependency(
    'boost',
    required: false,
    modules: [ 'coroutine' ],
)
pthread_dep = dependency('threads')

subdir('example')
subdir('test')

install_subdir(
    'include/sdbusplus',
    install_dir: get_option('includedir'),
    strip_directory: false,
)

import('pkgconfig').generate(
    libraries: libsdbusplus,
    name: meson.project_name(),
    version: meson.project_version(),
    requires: libsystemd_pkg,
    description: 'C++ bindings for sdbus',
)
