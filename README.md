# AmneziaWG

AmneziaWG (AmneziaWireGuard) is a fork of the regular WireGuard-Go with the addition of functions to bypass blocking and reduce the likelihood of protocol detection. One of the key features of AmneziaWG is backward compatibility with WireGuard. This means that when using AmneziaWG, unless the configuration specifies specific parameters for protocol obfuscation, it will act as a standard WireGuard.

What's special?

Before the session starts, the client sends several packets with random data (the number of such packets Jc and their minimum and maximum size in bytes Jmin, Jmax is set in the config)

The header of the handshake packet (Initiator to Responder) and the response packet (Responder to Initiator) have been changed; these values are also set in the config (H1 and H2)

Init handshake packets additionally have garbage at the beginning of the data,
the dimensions are determined by the values of S1 and S2. (by default, the initial handshake packet has a fixed size (148 bytes), after adding garbage, its size will be 148 + the length of random bytes).

The header of data packages and special “Under Load” packages has been changed - H4 and H3, respectively.
More details about the new custom fields:

- `junk_packet_count` Jc (Junk packet count) - the number of packets with random data that are sent before the start of the session
- `junk_packet_min_size` JMin (Junk packet minimum size) - minimum packet size for Junk packet. That is, all randomly generated packets will have a size no less than Jmin
- `junk_packet_max_size` JMax (Junk packet maximum size) - maximum size for Junk packets
- `init_packet_junk_size` S1 (Init packet junk size) - the size of random data that will be added to the init packet, the size of which is initially fixed
- `response_packet_junk_size` S2 (Response packet junk size) - the size of random data that will be added to the response, the size of which is initially fixed
- `init_packet_magic_header` H1 (Init packet magic header) - header of the first byte of the handshake
- `response_packet_magic_header` H2 (Response packet magic header) - header of the first byte of the handshake response
- `transport_packet_magic_header` H3 (Transport packet magic header) - header of the transmitted data packet
- `uload_packet_magic_header` H4 (Underload packet magic header) - UnderLoad packet header

As you can guess, the headings H1, H2, H3, H4 should be different. If you set Jc, S1 and S2 to zero, then there will be no garbage.

> **_NOTE:_**
A regular WG server can work with the AmneziaWG configuration in which Jc, Jmin, Jmax are set, and the remaining fields are zero. Thus, the AWG client will simply send garbage packets before init packets, which has absolutely no effect on the operation of the WG protocol, but may confuse DPI.

---

# Home Assistant Community Add-on: WireGuard

[![GitHub Release][releases-shield]][releases]
![Project Stage][project-stage-shield]
[![License][license-shield]](LICENSE.md)

![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports i386 Architecture][i386-shield]

[![Github Actions][github-actions-shield]][github-actions]
![Project Maintenance][maintenance-shield]
[![GitHub Activity][commits-shield]][commits]

[![Discord][discord-shield]][discord]
[![Community Forum][forum-shield]][forum]

[![Sponsor Frenck via GitHub Sponsors][github-sponsors-shield]][github-sponsors]

[![Support Frenck on Patreon][patreon-shield]][patreon]

WireGuard: fast, modern, secure VPN tunnel.

## About

[WireGuard®][wireguard] is an extremely simple yet fast and modern VPN that
utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner,
and more useful than IPsec, while avoiding the massive headache.

It intends to be considerably more performant than OpenVPN. WireGuard is
designed as a general-purpose VPN for running on embedded interfaces and
supercomputers alike, fit for many different circumstances.

Initially released for the Linux kernel, it is now cross-platform (Windows,
macOS, BSD, iOS, Android) and widely deployable,
including via an Hass.io add-on!

WireGuard is currently under heavy development, but already it might be
regarded as the most secure, easiest to use, and the simplest VPN solution
in the industry.

[:books: Read the full add-on documentation][docs]

## Support

Got questions?

You have several options to get them answered:

- The [Home Assistant Community Add-ons Discord chat server][discord] for add-on
  support and feature requests.
- The [Home Assistant Discord chat server][discord-ha] for general Home
  Assistant discussions and questions.
- The Home Assistant [Community Forum][forum].
- Join the [Reddit subreddit][reddit] in [/r/homeassistant][reddit]

You could also [open an issue here][issue] GitHub.

## Contributing

This is an active open-source project. We are always open to people who want to
use the code or contribute to it.

We have set up a separate document containing our
[contribution guidelines](CONTRIBUTING.md).

Thank you for being involved! :heart_eyes:

## Authors & contributors

The original setup of this repository is by [Franck Nijhof][frenck].

For a full list of all authors and contributors,
check [the contributor's page][contributors].

## We have got some Home Assistant add-ons for you

Want some more functionality to your Home Assistant instance?

We have created multiple add-ons for Home Assistant. For a full list, check out
our [GitHub Repository][repository].

## License

MIT License

Copyright (c) 2019-2023 Franck Nijhof

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-no-red.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[commits-shield]: https://img.shields.io/github/commit-activity/y/hassio-addons/addon-wireguard.svg
[commits]: https://github.com/hassio-addons/addon-wireguard/commits/main
[contributors]: https://github.com/hassio-addons/addon-wireguard/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord-shield]: https://img.shields.io/discord/478094546522079232.svg
[discord]: https://discord.me/hassioaddons
[docs]: https://github.com/hassio-addons/addon-wireguard/blob/main/wireguard/DOCS.md
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-wireguard/134662?u=frenck
[frenck]: https://github.com/frenck
[github-actions-shield]: https://github.com/hassio-addons/addon-wireguard/workflows/CI/badge.svg
[github-actions]: https://github.com/hassio-addons/addon-wireguard/actions
[github-sponsors-shield]: https://frenck.dev/wp-content/uploads/2019/12/github_sponsor.png
[github-sponsors]: https://github.com/sponsors/frenck
[i386-shield]: https://img.shields.io/badge/i386-no-red.svg
[issue]: https://github.com/hassio-addons/addon-wireguard/issues
[license-shield]: https://img.shields.io/github/license/hassio-addons/addon-wireguard.svg
[maintenance-shield]: https://img.shields.io/maintenance/yes/2023.svg
[patreon-shield]: https://frenck.dev/wp-content/uploads/2019/12/patreon.png
[patreon]: https://www.patreon.com/frenck
[project-stage-shield]: https://img.shields.io/badge/project%20stage-experimental-yellow.svg
[reddit]: https://reddit.com/r/homeassistant
[releases-shield]: https://img.shields.io/github/release/hassio-addons/addon-wireguard.svg
[releases]: https://github.com/hassio-addons/addon-wireguard/releases
[repository]: https://github.com/hassio-addons/repository
[wireguard]: https://www.wireguard.com
