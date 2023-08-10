project('wayland-utils',
	'c',
	version: '1.2.0',
	default_options: [
		'warning_level=3',
		'c_std=c99',
		'b_lundef=true',
	],
	meson_version: '>= 0.47',
	license: 'MIT/Expat',
)


dir_prefix = get_option('prefix')
dir_man = join_paths(dir_prefix, get_option('mandir'))
dir_inc = include_directories('.')

pkgconfig = import('pkgconfig')

cc = meson.get_compiler('c')
add_project_arguments(cc.get_supported_arguments([
	'-Wundef',
	'-Wno-unused-parameter',
]), language: 'c')

dep_wayland_client = dependency('wayland-client', version: '>= 1.20.0')
dep_libdrm = dependency('libdrm', version: '>=2.4.109', required: get_option('drm'))
dep_libdrm_version = dep_libdrm.version()

config_h = configuration_data()
config_h.set('_POSIX_C_SOURCE', '200809L')
config_h.set('HAVE_LIBDRM', dep_libdrm.found().to_int())

configure_file(output: 'config.h', configuration: config_h)

subdir('wayland-info')
subdir('man')
