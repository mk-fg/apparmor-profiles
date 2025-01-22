apparmor-profiles
=================

AppArmor profiles I use for binary or potentially complex/dangerous/exposed apps
like browsers, random electron and wine stuff, proprietary things, etc.

Repository URLs:

- https://github.com/mk-fg/apparmor-profiles
- https://codeberg.org/mk-fg/apparmor-profiles
- https://fraggod.net/code/git/apparmor-profiles

On the desktop, even confined to user's uid, such apps still get unwanted access
to a lot of things in $HOME and can read a lot of poorly-secured files on the system
(like /etc/passwd or some non-chmodded config), which is obviously undesirable,
and what AppArmor can help to fix.

Some profiles and abstractions are reused from upstreams like ubuntu, suse and
various misc other repos, but often found them too lax or bloated for specific
system (currently Arch Linux), allowing stuff like ``@{HOME}/** r``, so prefer to
use them just for reference, copying only obvious and safe access lines from there,
getting (or confirming) the rest from audit logs.

Main doc on rule syntax:
https://gitlab.com/apparmor/apparmor/wikis/AppArmor_Core_Policy_Reference

I use apparmor_init_ script (under "scripts" dir) to load these profiles with
some caching and "--override-policy-abi" option to avoid needing boilerplate
for it in every file - they are intended to always work together anyway.

.. _apparmor_init: scripts/apparmor_init

Important note
--------------

This is more of a "my configuration" repository, and profiles here are mostly
written in an ad-hoc fashion for my system, not to be generic fit for any linux
(or even app usage scenario) out there.

Plus I'm no security expert, so can - and do - miss some things, only making
sure that the most obvious bad things can't happen (or will trigger a warning),
not trying to build super-secure system or anything, thinking of it more like
basic hygeine than hardening against a dedicated attacker.

Therefore it might be wise to only use these profiles for reference
(e.g. to get the general idea where app needs access), and not as a drop-in config.

Some paths in profiles like @{HOME\_GIT} and @{SYS\_GIT} are specific to my
systems (configuration git repos), and can/should be removed or updated to some
other local paths.

See also
--------

- Flatpak, Snap, AppImage, Docker/Podman - one of the goals of these containers
  is security and isolation too, though usually not the primary one,
  but LSMs like AppArmor/SELinux can be added there too, to help with that.

- `Landlock LSM`_ - relatively new (2021) unprivileged-sandboxing LSM, kinda like
  AppArmor except you load profile in a wrapper or when starting the app itself,
  without needing uid=root or any fancy capabilities for it.

.. _Landlock LSM: https://landlock.io/
