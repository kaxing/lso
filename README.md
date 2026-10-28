# LSO — Linux Subsystem for Omarchy

*Helping Linux hosts host happy Omarchy guests*

LSO makes it easy for Linux users to try out Omarchy. It's nothing like WSL and may feel like a `virsh` wrapper, but no one can stop us from naming it LSO :)

![LSO terminal interface](lso.png)

## Get started

Put `lso` on your `PATH`. You'll need a Linux host with KVM, libvirt, OVMF and `virt-viewer`.

```sh
lso install --check        # check host requirements
lso install                # create an instance and choose a username/password
lso desktop --fullscreen   # open the Omarchy desktop
```

Prefer a terminal?

```sh
lso                        # open an interactive guest shell
lso shell omarchy version
# 4.0.6-1
```

![Omarchy shell through LSO](lso-shell.png)

Or stream an individual app onto your host desktop:

```sh
lso app list
lso app firefox
```

App streaming requires `waypipe` on both host and guest; LSO does not install it automatically. The full desktop does not need it.

## Installation

LSO uses a supplied ISO, then checks `~/.lso/cache/`, then [downloads Omarchy 4.0.6](https://iso.omarchy.org/omarchy-4.0.6.iso) if needed. The download is roughly 6 GiB and requires `curl`. ISO files are checked for being non-empty, not cryptographically verified. Missing or empty supplied files fall back to the cache/download.

```sh
lso install --iso /path/to/omarchy.iso
```

Installation is headless by default and **does not upgrade the guest OS**. Instance files live under `~/.lso/<name>/`; the default name is `default`.

## Instances and commands

```sh
lso install --name work --resource low   # create a smaller named instance
lso list                                # list instances
lso -n work                             # open its shell
lso status -n work                      # show state and resource usage
lso stop -n work                        # shut it down
lso env -n work                         # show its file paths
```

Use `lso shell <command...>` for guest commands, not `lso <command>`. Unsupported options are rejected with a usage hint and exit code `2`; for example, `--full` suggests `--fullscreen`. See `lso --help` for all options.

## Contributing

Currently LSO is extensively tested on Ubuntu (24.04 host). Please feel free to open a PR to support more distros.

## License

[0BSD](LICENSE). Upstream projects, including Omarchy, retain their own licenses.
