# s22su/dnsmasq

This is a lightweight image for [Dnsmasq][dnsmasq].

# Usage examples

Mounting configuration in `docker-compose.yaml`:

```yaml
version: '3'
services:
  dns:
    image: s22su/dnsmasq
    restart: always
    volumes:
      - ./dnsmasq.conf:/etc/dnsmasq.conf
    ports:
      - '127.0.0.1:53:53/udp'
    cap_add:
      - NET_ADMIN
```

Overriding command in `docker-compose.yaml`:

```yaml
version: '3'
services:
  dns:
    image: s22su/dnsmasq
    restart: always
    ports:
      - '127.0.0.1:53:53/udp'
    command:
      - --log-queries
      - --log-facility=-
      - --no-resolv
      - --address=/my-site.test/127.0.0.1
      - --address=/other-site.test/127.0.0.1
    cap_add:
      - NET_ADMIN
```

# Publishing new version

```shell
docker login --username
docker buildx build --platform linux/amd64,linux/arm64 --push -t s22su/dnsmasq:latest -t s22su/dnsmasq:alpine-<version>-dnsmasq-<version> .
```

[dnsmasq]: https://thekelleys.org.uk/dnsmasq/doc.html
