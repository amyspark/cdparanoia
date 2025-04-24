interface_args = []

if get_option('optimization') == '0'
    interface_args += ['-DCDDA_TEST']
endif

cdda_interface = library(
    'cdda_interface',
    files(
        'scan_devices.c',
        'common_interface.c',
        'cooked_interface.c',
        'interface.c',
        'scsi_interface.c',
        'smallft.c',
        'toc.c',
        'test_interface.c',
    ),
    c_args: project_args + interface_args,
    dependencies: [m_dep, rt_dep],
    pic: true,
    version: '0.@0@'.format(meson.project_version())
)

install_header(
    files(
        'cdda_interface.h'
    )
)
