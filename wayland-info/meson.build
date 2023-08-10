dep_scanner = dependency('wayland-scanner', native: true)
prog_scanner = find_program(dep_scanner.get_pkgconfig_variable('wayland_scanner'))

dep_wp = dependency('wayland-protocols', version: '>= 1.24')
dir_wp_base = dep_wp.get_pkgconfig_variable('pkgdatadir')

generated_protocols = {
	# stable
	'presentation-time': dir_wp_base / 'stable/presentation-time/presentation-time.xml',

	# staging
	'drm-lease-v1': dir_wp_base / 'staging/drm-lease/drm-lease-v1.xml',

	# unstable
	'linux-dmabuf-unstable-v1': dir_wp_base / 'unstable/linux-dmabuf/linux-dmabuf-unstable-v1.xml',
	'tablet-unstable-v2': dir_wp_base / 'unstable/tablet/tablet-unstable-v2.xml',
	'xdg-output-unstable-v1': dir_wp_base / 'unstable/xdg-output/xdg-output-unstable-v1.xml',
}

generated_protocols_sources = []

foreach base_file, xml_path: generated_protocols
	foreach output_type: [ 'client-header', 'private-code' ]
		if output_type == 'client-header'
			output_file = '@0@-client-protocol.h'.format(base_file)
		else
			output_file = '@0@-protocol.c'.format(base_file)
			if dep_scanner.version().version_compare('< 1.14.91')
				output_type = 'code'
			endif
		endif

		target = custom_target(
			'@0@ @1@'.format(base_file, output_type),
			command: [ prog_scanner, output_type, '@INPUT@', '@OUTPUT@' ],
			input: xml_path,
			output: output_file,
		)
		generated_protocols_sources += target
	endforeach
endforeach

wayland_info_src = [
	'wayland-info.c',
]

executable('wayland-info',
	wayland_info_src + generated_protocols_sources,
	include_directories: dir_inc,
	dependencies: [dep_wayland_client, dep_libdrm],
	install : true)
