project('cdparanoia', 'c',
    version: '10.2',
    default_options: [
        'c_std=gnu99,c11',
        'buildtype=debugoptimized',
    ],
    meson_version: '>= 1.3.0'
)

cc = meson.get_compiler('c')

project_args = cc.get_supported_arguments([
    '-fsigned-char',
    # Warnings from recent GCC
    '-Wno-unused-but-set-variable',
    '-Wno-misleading-indentation',
    '-Wno-maybe-uninitialized',
    '-Wno-unused-function',
    '-Wno-parentheses',
    '-Wno-sizeof-pointer-memaccess',
    '-Wno-unused-variable',
    '-Wno-pointer-sign',
    '-Wno-address',
    # Warnings from recent clang
    '-Wno-absolute-value'
])

if host_machine.cpu_family() == 'x86' and get_option('optimization') != '0'
    project_args += cc.get_supported_arguments(
        ['-ffast-math', '-finline-functions']
    )
endif

if cc.has_header('linux/sbpcd.h')
    project_args += ['-DSBPCD_H=1']
endif

if cc.has_header('linux/ucdrom.h')
    project_args += ['-DUCDROM_H=1']
endif

m_dep = cc.find_library('m', required: false)
rt_dep = cc.find_library('rt', required: false)

subdir('interface')
subdir('paranoia')

cdparanoia = executable(
    'cdparanoia',
    files(
        'main.c',
        'report.c',
        'header.c',
        'buffering_write.c',
        'cachetest.c',
    ),
    link_with: [cdda_interface, cdda_paranoia],
    dependencies: [m_dep, rt_dep],
    install: true,
)

install_man(
    files(
        'cdparanoia.1',
    ),
)

install_header(
    files(
        'utils.h'
    )
)
