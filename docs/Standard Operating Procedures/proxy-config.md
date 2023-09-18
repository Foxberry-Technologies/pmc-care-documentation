# Internal Proxy Routing with Dante

This guide will help you set up an internal proxy server using Dante on two Ubuntu servers. The goal is to route all internet traffic from Server 1 through Server 2.

## Prerequisites

1. Two Ubuntu servers (Server 1 and Server 2).
2. SSH access to both servers.
3. Basic knowledge of Linux command line.

## Server 2 (Proxy Server) Setup

### Step 1: Update the Server

Update the server's packages to the latest versions:

```bash
sudo apt update
sudo apt upgrade
```

### Step 2: Install Dante

Install the Dante SOCKS proxy server on Server 2:

```bash
sudo apt install dante-server
```

### Step 3: Configure Dante

Edit the Dante configuration file:

```bash
sudo nano /etc/danted.conf
```

Replace the content of the file with the following configuration:

First of all use the `ifconfig` command to find out the internal and external interfaces.
In the below case `lo` was internal and `ens5` was external.

```plaintext
internal: lo port = 1080
external: ens5

socksmethod: username none

user.privileged: root
user.unprivileged: nobody

client pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    log: connect disconnect
}

socks pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    protocol: tcp udp
}
```

Save and exit the editor (Ctrl+O, Enter, Ctrl+X).

### Step 4: Restart Dante

Restart the Dante service to apply the new configuration:

```bash
sudo systemctl restart danted
```

Ensure Dante starts on boot:

```bash
sudo systemctl enable danted
```

## Server 1 (Client) Setup

### Step 1: Install Dante Client

Install the Dante client (socksify) on Server 1:

```bash
sudo apt install dante-client
```

### Step 2: Configure Dante Client

Edit the Dante client configuration file:

```bash
sudo nano /etc/dante.conf
```

Add the following lines, replacing `proxy_server_ip` with Server 2's IP address:

```plaintext
logoutput: syslog
internal: eth0 port = 1080
external: proxy_server_ip
method: username
user.privileged: proxyuser
user.unprivileged: nobody
client pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    log: connect disconnect
}
```

Save and exit the editor (Ctrl+O, Enter, Ctrl+X).

### Step 3: Route Traffic Through Proxy in Server 1

To route specific network traffic through the proxy, add new environment variables `HTTP_PROXY` and `HTTPS_PROXY` in `Server 1`

    $ sudo vi /etc/environment

Add the below two lines

    # /etc/environment
    ...
    HTTPS_PROXY:socks://proxy_server_ip:1080
    HTTP_PROXY:socks://proxy_server_ip:1080
    

## Confirming Proxy Setup

To confirm that the proxy setup is working, monitor Dante logs on Server 2:

```bash
grep danted /var/log/syslog
```

Review the logs for any errors or warnings. If necessary, adjust your configuration and restart Dante.

## Saving Firewall Rules (Server 2)

To allow incoming connections on port 1080, add an `iptables` rule:

```bash
sudo iptables -A INPUT -p tcp --dport 1080 -j ACCEPT
```

## Saving Firewall Rules (Server 1)

For Ubuntu 18.04 and earlier, save `iptables` rules:

```bash
sudo iptables-save > /etc/iptables/rules.v4
```

For Ubuntu 20.04 and later:

Ubuntu has transitioned to using nftables instead of iptables, so you might need to use different commands and methods to save your firewall rules. Here's an example:

Save your current nftables rules to a file:

    sudo nft list ruleset > /etc/nftables.conf

To load the saved rules during boot, you can add the following line to your systemd service file (e.g., /etc/systemd/system/apply-firewall-rules.service). Create the service file if it doesn't exist:


    [Unit]
    Description=Apply firewall rules at boot

    [Service]
    ExecStart=/usr/sbin/nft -f /etc/nftables.conf

    [Install]
    WantedBy=multi-user.target

Save the file, then enable and start the service:

```bash
sudo systemctl enable apply-firewall-rules.service
sudo systemctl start apply-firewall-rules.service
```

This will apply your nftables rules during boot.

Remember to adjust the instructions based on your specific Ubuntu version and firewall setup. If you're unsure which method to use or have further questions, please provide more details about your Ubuntu version, and I can offer more specific guidance.

## Conclusion

With this setup, Server 1's internet traffic is routed through Server 2, acting as a Dante SOCKS proxy server. Ensure your firewall rules, configurations, and applications are correctly set up to enjoy the benefits of the internal proxy routing.

---

Please note that this guide provides a comprehensive overview of setting up an internal proxy with Dante. Adjust the configurations as needed to match your specific network setup and requirements.
