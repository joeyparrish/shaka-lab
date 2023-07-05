# Shaka Lab Consolidated Build Instructions - Linux

If you haven't yet prepared an installer, please read
[Installer Prep](installer-prep.md).

Please refer to [Devices](devices.md) for any hardware-specific pre-install
setup and for a list of packages for this device.


## OS Installation

1. Insert the flash drive into the new Linux device and power it on.
2. Enter the boot menu (press F11 on Topaz 2).
3. Select the USB drive (may say "UEFI") and then "Ubuntu...amd64" or
   "Ubuntu...arm64" as appropriate.
4. Select "boot in normal mode".
5. At the GRUB boot menu, highlight "Try or Install Ubuntu Server".
6. **Topaz 2 only**: Default kernel parameters may cause issues with the
   monitor.
   1. Press `e` to edit kernel parameters for boot.
   2. Move the cursor to the line that begins with `linux` and append
      `nomodeset`.
   3. Press F10 to boot with the modified parameters.
7. **Not Topaz 2**: press enter to boot with default parameters.
8. If prompted to update the installer, select "update to the new installer".
   The latest installers will remember extra kernel parameters used to boot the
   installer, so that they get used to boot the target system as well.
9. For "type of install", select "Ubuntu Server".
10. Leave the default of "use entire disk".
11. Select "done".
12. Leave "your name" blank.
13. Set "your server's name":
    1. For `shaka-lab-gateway`, use the short hostname "gateway".  This is
       under Active Directory's character limit on device names.
    2. For all other devices, use the assigned name of the device (e.g.
       `shaka-test-linux`).
14. Set username and password:
    1. Inside Google: Set username and password to those stored in the
       Google-internal password manager under "Shaka Lab Default Login".
    2. Outside Google: Set your preferred username and password


## Setup

1. **Topaz 2 only**: Edit /etc/netplan/00-installer-config.yaml, and add
   `optional: true` to the configuration of `enp47s0`.  This will speed up
   booting when only one interface is used, by telling the system that the
   second interface is not needed for the `network-online` target to be reached
   in systemd.  Without this change, there is a long delay of several minutes
   before anyone can log in.
2. Upgrade all packages by running:
   ```sh
   sudo apt update && sudo apt -y upgrade
   ```
3. Set up access to the Shaka Lab packages by running these commands:
   ```sh
   curl -L https://shaka-project.github.io/shaka-lab/public.key | \
       sudo tee /etc/apt/trusted.gpg.d/shaka-lab.asc
   echo deb https://shaka-project.github.io/shaka-lab/ stable main | \
       sudo tee /etc/apt/sources.list.d/shaka-lab.list
   sudo apt update
   ```
4. Before installing the `shaka-lab-gateway-client` packages, choose an Active
   Directory password.
   1. Inside Google: Use the password stored in the Google-internal password
      manager under "Shaka Lab Active Directory Password".
   2. Outside Google: Choose the same password you used to set up Active
      Directory on your gateway.
5. Run the following command to pre-configure the shaka-lab-gateway-client
   package and its dependencies, replacing `AD_PASS` with your AD password:
   ```sh
   cat << EOF | sudo debconf-set-selections
   nslcd	nslcd/ldap-reqcert	select	never
   nslcd	nslcd/ldap-uris	string	ldaps://localhost
   nslcd	nslcd/ldap-base	string	dc=lab,dc=shaka
   libnss-ldapd	libnss-ldapd/nsswitch	multiselect	passwd, group, shadow
   shaka-lab-gateway-client shaka-lab-gateway-client/active_directory_password string AD_PASS
   EOF
   ```
6. Special setup for `shaka-lab-gateway`:
   1. Before installing the `shaka-lab-gateway` packages, choose an Active
      Directory password.
      1. Inside Google: Use the password stored in the Google-internal password
         manager under "Shaka Lab Active Directory Password".
      2. Outside Google: Choose the same password you used to set up Active
         Directory on your gateway.
   2. Run the following command to pre-configure the shaka-lab-gateway package and
      its dependencies, replacing:
      1. `AD_PASS` with your AD password
      2. `LAN_IFACE` with your LAN interface (ours is `enp47s0`)
      3. `WAN_IFACE` with your WAN interface (ours is `enp45s0`)
      4. `LAN_NET` with your LAN network (ours is `172.31.187.0/24`)
      5. `LAN_IP` with your gateway's LAN IP (ours is `172.31.187.1`)
      6. `LAN_IP` with your LAN's router (ours is `172.31.187.254`)
      7. `DHCP_START` with the start of your LAN's DHCP range (ours is
         `172.31.187.10`)
      8. `DHCP_END` with the end of your LAN's DHCP range (ours is
         `172.31.187.99`)
      ```sh
      cat << EOF | sudo debconf-set-selections
      krb5-config krb5-config/default_realm string
      iptables-persistent iptables-persistent/autosave_v4 boolean false
      iptables-persistent iptables-persistent/autosave_v6 boolean false
      nslcd	nslcd/ldap-reqcert	select	never
      nslcd	nslcd/ldap-uris	string	ldaps://localhost
      nslcd	nslcd/ldap-base	string	dc=lab,dc=shaka
      libnss-ldapd	libnss-ldapd/nsswitch	multiselect	passwd, group, shadow
      shaka-lab-gateway shaka-lab-gateway/lan_interface string LAN_IFACE
      shaka-lab-gateway shaka-lab-gateway/wan_interface string WAN_IFACE
      shaka-lab-gateway shaka-lab-gateway/lan_network string LAN_NET
      shaka-lab-gateway shaka-lab-gateway/lan_ip string LAN_IP
      shaka-lab-gateway shaka-lab-gateway/lan_router string LAN_ROUTER
      shaka-lab-gateway shaka-lab-gateway/dhcp_start string DHCP_START
      shaka-lab-gateway shaka-lab-gateway/dhcp_end string DHCP_END
      shaka-lab-gateway shaka-lab-gateway/active_directory_password string AD_PASS
      shaka-lab-gateway-client shaka-lab-gateway-client/active_directory_password string AD_PASS
      EOF
      ```
   3. Populate the `devices` section of
      `/etc/total-perspective-vortex/config.yaml` with the device names, IPs
      and ethernet addresses (`mac:`) of the devices you want static
      allocations for.
      **TODO(joeyparrish)**: This config isn't backed up for the Shaka team
      inside Google, which is complicated by the isolated lab environment.
      Create a revision-control solution for this, then document it here.
7. Special setup for `shaka-test-linux`:
   1. Get an ACME DNS API token from Google Domains for the lab domain (ours is
      `shakalab.rocks`):
      1. Log into Google Domains
      2. Click the domain
      3. Click "Security"
      4. Find "ACME DNS API" and click "Create token"
      5. Copy the token to your clipboard
   2. Run the following command to pre-configure the shaka-lab-certs package,
      replacing:
      1. `DNS_ZONE` with your lab domain (`shakalab.rocks` for us)
      2. `GOOGLE_DOMAINS_TOKEN` with your DNS API token from above
      3. `CERT_HOST` with the hostname for your certs (`karma.shakalab.rocks`
         for us)
      ```sh
      cat << EOF | sudo debconf-set-selections
      shaka-lab-certs shaka-lab-certs/dns_zone string DNS_ZONE
      shaka-lab-certs shaka-lab-certs/google_domains_token password GOOGLE_DOMAINS_TOKEN
      shaka-lab-certs shaka-lab-certs/cert_host string CERT_HOST
      EOF
      ```
   3. Run the following command to pre-configure the shaka-lab-github-runner
      package, replacing:
      1. `REPO_URL` with the URL of your Shaka Player repo (ours is
         `https://github.com/shaka-project/shaka-player`)
      2. `ACCESS_TOKEN` with a GitHub personal access token of a repo admin,
         generated with `repo` permissions
      ```sh
      cat << EOF | sudo debconf-set-selections
      shaka-lab-github-runner shaka-lab-github-runner/scope select repo
      shaka-lab-github-runner shaka-lab-github-runner/scope_name string REPO_URL
      shaka-lab-github-runner shaka-lab-github-runner/access_token password ACCESS_TOKEN
      shaka-lab-github-runner shaka-lab-github-runner/labels string self-hosted-selenium
      shaka-lab-github-runner shaka-lab-github-runner/number_of_runners string 16
      EOF
      ```
8. For each package in the list for this machine, run:
   ```sh
   sudo apt -y install PACKAGE-NAME-GOES-HERE
   ```
9. If installing `shaka-lab-node`:
   1. Edit `/etc/shaka-lab-node-config.yaml` to configure this node's browsers.
   2. Restart the service:
      ```sh
      sudo systemctl restart shaka-lab-node
      ```
