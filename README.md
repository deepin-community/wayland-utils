wayland-info
============

`wayland-info` is a utility for displaying information about the Wayland
protocols supported by a Wayland compositor.

It can be used to check which Wayland protocols and versions are advertised
by the Wayland compositor.

`wayland-info` also provides additional information for a subset of Wayland
protocols it knows about, namely Linux DMABUF, presentation time, tablet and
XDG output protocols.

An example output is:

```
$ wayland-info
interface: 'wl_drm',                                     version:  2, name:  1
interface: 'wl_compositor',                              version:  4, name:  2
interface: 'wl_shm',                                     version:  1, name:  3
	formats: XRGB8888 ARGB8888
interface: 'wl_output',                                  version:  2, name:  4
	x: 0, y: 0, scale: 1,
	physical_width: 310 mm, physical_height: 170 mm,
	make: 'AUO', model: '0x123d',
	subpixel_orientation: unknown, output_transform: normal,
	mode:
		width: 1920 px, height: 1080 px, refresh: 60.049 Hz,
		flags: current preferred
[...]
```

`wayland-info` uses the Wayland protocol only and only shows features
that the compositor implements via Wayland protocols.

Building
========

`wayland-info` is built using [Meson](https://mesonbuild.com/) and depends
on [Wayland](https://gitlab.freedesktop.org/wayland/wayland) and
[wayland-protocols](https://gitlab.freedesktop.org/wayland/wayland-protocols).

	$ git clone https://gitlab.freedesktop.org/wayland/wayland-utils.git
	$ cd wayland-utils
	$ meson build/ --prefix=...
	$ ninja -C build/ install
	$ cd ..

Running
=======

`wayland-info` does not accept any command line option.

	$ wayland-info

Reporting issues and contributing
=================================

`wayland-info` is hosted on
[freedesktop.org's GitLab instance](https://gitlab.freedesktop.org/wayland/wayland-utils).
It uses the same contributing guidelines as the Wayland project, please refer
to [Wayland's contributing document](https://gitlab.freedesktop.org/wayland/wayland/-/blob/main/CONTRIBUTING.md)
for more information.

Credit
======

The code base of `wayland-info` is identical to `weston-info` and therefore
all credits for `wayland-info` go to the authors and contributors of
`weston-info`.

Because `weston-info` is a generally useful tool, even outside of weston,
and gives interesting information on any Wayland compositor, this is basically
a standalone version of `weston-info` as found in
[weston](https://gitlab.freedesktop.org/wayland/weston/) repository.
