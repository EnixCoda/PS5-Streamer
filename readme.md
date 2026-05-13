# PS5 Streamer

This project can stream your PS5 game play as a RTMP stream. So that you can stream it to 3rd party platforms like Bilibili.

It is composed of 2 services:

- dnsmasq

    Based on Alpine Linux with [webproc](https://github.com/jpillora/webproc) for the web UI. Configured to use `114.114.114.114` as the default DNS and includes rules for redirecting PS5 streaming data to the nginx-rtmp service.

- nginx-rtmp

    This is used to receive rtmp video stream from PS5 and output to rtmp clients.

## Architecture

```
                        ┌─────────────────────────────────────────────────┐
                        │            Host Machine (192.168.1.5)           │
                        │                                                 │
  ┌──────┐  DNS query   │  ┌───────────────────────────┐                  │
  │      │ ────────────►│  │          dnsmasq          │                  │
  │      │◄─────────────│  │       (port 53 UDP)       │                  │
  │      │ 192.168.1.5  │  │                           │                  │
  │ PS5  │  (hijacked)  │  │ contribute.live-video.net │                  │
  │      │              │  │       → 192.168.1.5       │                  │
  │      │              │  └───────────────────────────┘                  │
  │      │  RTMP stream │  ┌───────────────────────────┐                  │
  │      │ ────────────►│  │        nginx-rtmp         │                  │
  │      │  :1935       │  │        (port 1935)        │       pull       │
  └──────┘              │  │                           │ (port 1935 rtmp) │
                        │  │       stats: :8081        │────────────────────► OBS ──► Bilibili
                        │  └───────────────────────────┘                  │
                        └─────────────────────────────────────────────────┘
```
## Requirement

[Docker](https://www.docker.com/) (you can run it on your streaming PC)

## Usage

[Checkout Wiki / 使用教程](https://github.com/EnixCoda/PS5-Streamer/wiki/%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B) (it is in Chinese!)

## License
MIT
