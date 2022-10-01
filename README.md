# eturnal STUN/TURN Server

<p align="left">
    <img src="hello-eturnal.png"
        height="180">

[![CI](https://github.com/processone/eturnal/actions/workflows/ci.yml/badge.svg)][1]

[eturnal][2] is a modern, straightforward STUN and TURN server. For
authentication, the mechanism described in the [REST API for Access to TURN
Services][3] specification is implemented. The server can easily be tested [in a
Linux shell][4] or [using Docker][5]. For a persistent installation, see the
following section.

## Installation

> _Note:_ Running eturnal in **container environments** such as Docker or
> Kubernetes is described on a [separate documentation][6] page.

On **APT-based** Linux distributions, run:

    sudo apt install extrepo
    sudo extrepo enable eturnal
    sudo apt update
    sudo apt install eturnal

On **DNF-based** Linux distributions, run:

    sudo dnf config-manager --add-repo https://eturnal.net/eturnal.repo
    sudo dnf install eturnal
    sudo systemctl --now enable eturnal

On **YUM-based** Linux distributions, run:

    sudo yum-config-manager --add-repo https://eturnal.net/eturnal.repo
    sudo yum install eturnal
    sudo systemctl --now enable eturnal

On SUSE Linux Enterprise and openSUSE systems, [distribution repositories][7]
can be used instead. On other Linux systems, the binary release can be installed
as [described][8] in the reference documentation. For Windows, an installer is
[available][9]. On other platforms, eturnal is [built from source][10].

## Configuration

The eturnal server is configured by editing the `/etc/eturnal.yml` file. This
file uses the (indentation-sensitive!) [YAML][11] format. For TURN relaying to
work, you'll have to specify the [shared authentication][3] `secret` and (if
autodetection fails) also the `relay_ipv4_addr` option, which should be set to
the server's _external_ IPv4 address. As an example, a configuration for
offering STUN and TURN services on port 3478 (UDP and TCP) might look like
this:

```yaml
eturnal:
  secret: "long-and-cryptic"     # Shared secret, CHANGE THIS.
  relay_ipv4_addr: "203.0.113.4" # The server's public IPv4 address.
  relay_ipv6_addr: "2001:db8::4" # The server's public IPv6 address (optional).
```

A more detailed, commented [example configuration][12] is shipped with the
eturnal server.

## Running eturnal

On Linux systems, the eturnal server is usually invoked by [systemd][13]. For
non-systemd platforms, example [init][14] and [OpenRC][15] scripts are shipped
below the `etc` directory.

For controlling eturnal, the `eturnalctl` command can be used; see:

    eturnalctl help

## Logging

If eturnal was started by systemd, log files are written into the
`/var/log/eturnal` directory by default. In order to log to the [journal][16]
instead, the `log_dir` option can be set to `stdout` in the configuration file.

## Documentation

For a detailed description of eturnal's configuration options and the
`eturnalctl` tool, see the [reference documentation][17]. For notable changes
between eturnal releases, see the [change log][18].

## Feedback/Support

Please use [our issue tracker][19] for bug reports and feature requests. Feel
free to (ab)use it for usage questions as well. If you happen to be using
[XMPP][20], you could also join our public room
`eturnal@conference.process-one.net`. Otherwise, just use the [web client][21].
As an alternative, there's an `#eturnal` channel [on Slack][22].

 [1]: https://github.com/processone/eturnal/actions/workflows/ci.yml
 [2]: https://eturnal.net/
 [3]: https://tools.ietf.org/html/draft-uberti-behave-turn-rest-00
 [4]: https://github.com/processone/eturnal/blob/master/QUICK-TEST.md
 [5]: https://github.com/processone/eturnal/blob/master/docker-k8s/QUICK-TEST.md
 [6]: https://eturnal.net/documentation/code/docker.html
 [7]: https://software.opensuse.org/download/?package=eturnal&project=devel:languages:erlang
 [8]: https://eturnal.net/documentation/#Installation
 [9]: https://eturnal.net/windows/
[10]: https://github.com/processone/eturnal/blob/1.10.1/INSTALL.md
[11]: https://en.wikipedia.org/wiki/YAML
[12]: https://github.com/processone/eturnal/blob/1.10.1/config/eturnal.yml
[13]: https://www.freedesktop.org/software/systemd/man/systemctl.html
[14]: https://github.com/processone/eturnal/blob/1.10.1/scripts/eturnal.init
[15]: https://github.com/processone/eturnal/blob/1.10.1/scripts/eturnal.openrc
[16]: https://www.freedesktop.org/software/systemd/man/systemd-journald.service.html
[17]: https://eturnal.net/documentation/
[18]: https://github.com/processone/eturnal/blob/1.10.1/CHANGELOG.md
[19]: https://github.com/processone/eturnal/issues
[20]: https://xmpp.org
[21]: https://eturnal.net/chat/
[22]: https://erlef.org/slack-invite/erlanger
