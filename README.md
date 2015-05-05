# linux-surfacepro3
Arch Linux package to compile the Linux kernel with patches designed to improve user experience on the Surface Pro 3.

This is based on the offical Linux kernel package provided by Arch Linux at: https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux .

This AUR package adds the following patches to the official Linux kernel package:
 - Battery patch from linked mailing list in comment #18 of https://bugzilla.kernel.org/show_bug.cgi?id=90161 (will be in linux-4.1).
 - Camera patch from https://github.com/nuclearsandwich/surface3-archlinux/issues/12 (patch from `colorprint`)
 - Buttons and Wakeup patches from http://bugzilla.kernel.org/show_bug.cgi?id=84651 (patches from Chen Yu, comments #56 and #57)
 - Multitouch patches* from https://gist.github.com/felipeota/afb5f510f5b315f8bed8 . 
   (an X11 configuration file is also placed in `/etc/X11/xorg.conf.d/` in order to enable right click). Using these
   patches prevents the `caps lock` indicator led from working properly. See the footnote below for how to disable
   these patches if this is prohibitive for you.

\* The multitouch patches add two-finger scrolling support. I'm not sure how
   these patches affect touchpad support under Wayland (since Mesa 10.5.1, Weston will not start on the Surface Pro 3 https://bugs.freedesktop.org/show_bug.cgi?id=89689). 
   If you want to disable this patch, change line 48 of PKGBUILD to: `multitouch='n'`. If disabled, the Xorg
   configuration will not be copied to `/etc/X11/xorg.conf.d/` .

## Building

You will need to have imported gpg keys for the Linux kernel maintainers:

For Linus Torvalds (the major release key):

	gpg --recv-keys 79BE3E4300411886

For Greg Kroah-Hartman's key (the stable patch release key):

	gpg --recv-keys 38DBBDC86092693E 

Then, to build the package, simply run (as usual):

	makepkg

