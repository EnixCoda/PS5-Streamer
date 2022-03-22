# PS5 Streamer

This project can stream from PS5 to any platform without extra hardware except one that can run docker, e.g. PC or raspberry pi.

It is composed of 2 services:

- dnsmasq

    Based on [jpillora/dnsmasq](https://github.com/jpillora/docker-dnsmasq), I updated default configuration to use `114.114.114.114` as the default DNS and added rules for redirecting PS5 streaming data to nginx-rtmp service.

- nginx-rtmp

    This is used to receive rtmp video stream from PS5 and output to rtmp clients.

## Usage
[Checkout Wiki / 使用教程](https://github.com/EnixCoda/PS5-Streamer/wiki/%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B) (it is in Chinese!)

## Build
This project's file structure is extremely simple. You can build your own images very easily if you know basic usages of docker.

## License
MIT
