Releasing
=========

To make a release of wayland-utils, follow these steps.

1. Update the first stanza of `meson.build` to the intended version.

   Then commit your changes:

	$ RELEASE_NUMBER="x.y.z"
	$ RELEASE_NAME="[alpha|beta|RC1|RC2|official|point]"
	$ git status
	$ git commit meson.build -s -m "build: bump to version $RELEASE_NUMBER for the $RELEASE_NAME release"
	$ git push

2. Run the `release.sh` script to generate the tarballs, sign and upload them,
   and generate a release announcement template.  This script can be obtained
   from the Wayland repository:

   https://gitlab.freedesktop.org/wayland/wayland/-/blob/main/release.sh

3. Compose the release announcements.  The script will generate a *-x.y.z-announce.eml
   file with a list of changes and tags.  Prepend these with a human-readable
   listing of the most notable changes.

4. PGP sign the release announcement and send it to
   <wayland-devel@lists.freedesktop.org>.

5. Update `releases.html` in wayland.freedesktop.org with links to tarballs and
   the release email URL.

   Once satisfied:

	$ git commit -am "releases: add ${RELEASE_NUMBER} release"
	$ git push

For x.y.0 releases, also create the release series x.y branch.  The x.y branch
is for bug fixes and conservative changes to the x.y.0 release, and is where we
create x.y.z releases from.  Creating the x.y branch opens up master for new
development and lets new development move on.  We've done this both after the
x.y.0 release (to focus development on bug fixing for the x.y.1 release for a
little longer) or before the x.y.0 release (like we did with the 1.5.0 release,
to unblock master development early).

	$ git branch x.y [sha]
	$ git push origin x.y

The master branch's `meson.build` version should always be (at least) x.y.90,
with x.y being the most recent stable branch.  The stable branch's `meson.build`
version is just whatever was most recently released from that branch.

For stable branches, we commit fixes to master first, then `git cherry-pick -x`
them back to the stable branch.
