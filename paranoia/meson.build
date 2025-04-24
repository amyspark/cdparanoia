paranoia_args = []

cdda_paranoia = library(
    'cdda_paranoia',
    files(
        'paranoia.c',
        'p_block.c',
        'overlap.c',
        'gap.c',
        'isort.c',
    ),
    c_args: project_args + paranoia_args,
    link_with: cdda_interface,
    dependencies: [m_dep],
    pic: true,
    version: '0.@0@'.format(meson.project_version())
)

install_header(
    files(
        'cdda_paranoia.h'
    )
)
