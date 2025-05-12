# Copyright (c) 2025 Maxime Leroy

project(
  'zebra_dplane_grout',
  'c',
  default_options: [
    'buildtype=release',
    'c_std=gnu11',
    'werror=false',
    'warning_level=1',
])

# Ensure the header exists, fail early if not
assert(run_command('test', '-f', '/usr/include/gr_api.h', check: true).returncode() == 0,
       'gr_api.h not found in /usr/include')

grout_dep = declare_dependency()

# Use pkg-config for FRR
frr_dep = dependency('frr', required: true)

sources = [
  'zebra_dplane_grout.c',
  'rt_grout.c',
  'if_grout.c',
]

incdir = include_directories('.')
shared_module(
  'zebra_dplane_grout',
  sources,
  name_prefix: '',
  dependencies: [grout_dep, frr_dep],
  include_directories: incdir,
  install: true,
  install_dir: join_paths(frr_dep.get_variable(pkgconfig: 'libdir'), 'modules'),
  install_mode: 'rw-r--r--',
)
