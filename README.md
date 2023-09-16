# Runit services

This is a collection of user services for [runit](http://smarden.org/runit/)
and a script to manage them.

## Usage

Symlink services into `$USVDIR`, by default `$XDG_CONFIG_HOME/services` or `~/.config/services`.

You need to call `runsvdir` on the directory you symlink the services to.
I like to do this in my shell login scripts such as `.bash_profile` or `.bash_login`:

```
# Start DBus session
[[ -z "$DBUS_SESSION_BUS_ADDRESS" ]] && eval "$(dbus-launch --sh-syntax)"

# Run user services
export USVDIR="${XDG_CONFIG_HOME:-${HOME}/.config}/service"
[[ -z "$(pgrep -f "runsvdir $USVDIR")" ]] && runsvdir "$USVDIR" &
```

This specific snippet requires `pgrep` which is installed with the `procps-ng` package on Void Linux.
A DBus session bus is required before launching the Pipewire service.

Finally, use the `usv` script to manage services, for example `usv restart pipewire`.

## See also

- [madand/runit-services](https://github.com/madand/runit-services)
