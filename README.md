# `nixos-networkmanager-profiles`

Declarative NetworkManager 👌

Shoutout to [@Shou](https://github.com/Shou) as this was fully his idea.

## Usage

I suggest using `nmtui` or `nm-connection-editor` to write the `*.nmconnection`
file (look in `/etc/NetworkManager/system-connections`) then converting that to Nix
attributes like so:

```nix
# /etc/nixos/configuration.nix

{ ... }: {

  imports = [
    (import (builtins.fetchTarball https://github.com/jmackie/nixos-networkmanager-profiles/archive/master.tar.gz))
  ];

  networking.networkmanager.profiles = {
    "home-wifi" = {
      connection = {
        id = "home-wifi";
        uuid = "<your-uuid-here>";
        type = "wifi";
        permissions = "";
      };
      wifi = {
        mac-address-blacklist = "";
        mode = "infrastructure";
        ssid = "Home Wi-Fi";
      };
      wifi-security = {
        auth-alg = "open";
        key-mgmt = "wpa-psk";
        psk = "<password>";
      };
      ipv4 = {
        dns-search = "";
        method = "auto";
      };
      ipv6 = {
        addr-gen-mode = "stable-privacy";
        dns-search = "";
        method = "auto";
      };
    };
  };
}
```
