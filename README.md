# mailrelay

`mailrelay` is a simple mail relay that can take unauthenticated SMTP emails (e.g. over port 25) and relay them to authenticated, TLS-enabled SMTP servers. Plus it's easy to configure.

## Use case

Some older appliances such as scanners, multi-function printers, RAID cards or NAS boxes with monitoring, can only send email without any authentication or encryption over port 25. `mailrelay` can send those emails to your Gmail, Fastmail or other provider.

Run `mailrelay` on a local PC and set your device (e.g. scanner) to send mail to that PC.

`mailrelay` is written in Go, and can be compiled for any Go supported platform including Linux, MacOS, Windows.

## Example (Linux)

On local PC (192.168.1.54) create file `/etc/mailrelay.json` with contents:

/etc/mailrelay.json

```json
{
    "smtp_server":   "smtp.fastmail.com",
    "smtp_port":     465,
    "smtp_username": "username@fastmail.com",
    "smtp_password": "secretAppPassword",
    "local_listen_ip": "0.0.0.0",
    "local_listen_port": 2525
}
```

Run `mailrelay`,

```Bash
./mailrelay
```

Default location for configuration file is `/etc/mailrelay.json` but can be changed via `--config` flag. For example,

```bash
mailrelay --config=/home/myname/mailrelay.json
```

Configure your scanner or other device to send SMTP mail to server `192.168.1.54:2525`. Each email will be relayed to `smtp.fastmail.com` using the credentials above, including any file attachments.

