# systemd

## Prerequisites

Obtain bot token from [@BotFather](https://t.me/BotFather)

## Instructions

1. Download a tarball of a preffered vesion

```bash
wget https://github.com/momai/tg-captcha-bot/archive/refs/tags/v.1.2.1.tar.gz
tar -xavf v.1.2.1.tar.gz
```

2. Build the binary and place it in `$PATH`

```bash
cd tg-captcha-bot-v.1.2.1/
make
mv bot /usr/local/bin/tg-captcha-bot
```
> Run `CGO_ENABLED=0 make` if you would like to build the binary for another host

3. Move bot's config to needed path

```bash
mkdir -p /etc/tg-captcha-bot
cp config.toml help_message.txt /etc/tg-captcha-bot/
```

4. Create systemd unit file `/etc/systemd/system/tg-captcha-bot.service`

```bash
[Unit]
Description=tg-captcha-bot
Wants=network-online.target
After=network-online.target

[Service]
Environment="TGTOKEN=your_token"
Environment="CONFIG_PATH=/etc/tg-captcha-bot"
Type=simple
ExecStart=/usr/local/bin/tg-captcha-bot

Restart=always
RestartSec=3s

[Install]
WantedBy=multi-user.target
```

5. Reload configuration and restart service

```bash
systemctl daemon-reload
systemctl restart tg-captcha-bot.service
```

6. Check service status

```bash
systemctl status tg-captcha-bot.service
```

7. Check logs

```bash
journalctl -u tg-captcha-bot.service
```

8. Add the bot to your supergroup and give it administrator privileges
