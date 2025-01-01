# IR-DNS-Proxy

A simple solution to bypass Iran sanctions without changing the DNS settings on the whole system.

The problem this repository solves is that it sets up DNS bypassing proxies on an HTTP proxy, so you don't have to route your entire system through a specific DNS. This helps protect your privacy and security.

## Usage

### Clone the repository
```bash
git clone 
```

and then change directory to the repository directory:
```bash
cd ir-dns-proxy
```

### Load Docker image
```bash
docker image load -i tinyproxy.dockerimage
```

### Run Container

When you start the container, a tinyproxy will run inside it and listen on **port `8888`** on your host system **(acting as an HTTP Proxy).**

You can use this port in your `web browsers` (with a proxy switcher extension), in the `terminal`, with [`proxychains`](https://github.com/haad/proxychains), **or anywhere that supports an HTTP proxy.**

Run this command for start the container:

```bash
docker compose up -d
```

## Use in Terminal
```bash
export http_proxy='http://localhost:8888'    
export https_proxy='http://localhost:8888'
```

## Use in APT

This command will create a file named `90-proxy` in the `/etc/apt/apt.conf.d` directory and configure the proxy settings within it. After running this command, your APT connections will operate without restrictions. :)

```bash
echo -e 'Acquire::http::Proxy "http://localhost:8888/";\nAcquire::https::Proxy "http://localhost:8888/";' | sudo tee /etc/apt/apt.conf.d/90-proxy
```

## Use in Web Browsers
You can use the proxy in web browsers with extensions. In Firefox and Google Chrome, you can use [`FoxyProxy`](https://chromewebstore.google.com/detail/foxyproxy/gcknhkkoolaabfmlnjonogaaifnjlfnp?hl=en&pli=1) or other similar plugins.

**Don't forget** to set up an HTTP proxy profile in these extensions with the following settings:

- IP: **localhost**
- Port: **8888**

## Change DNS Provider
You can change the DNS provider to different nameservers.

To do this, edit the `docker-compose.yml` file and in the `dns` section, add the nameservers you want. Remember to comment out or delete any existing nameservers.


```yaml
dns:
  - 8.8.8.8
  - 8.8.4.4

  #- 10.202.10.202
  #- 10.202.10.102
```

And then, restart the conatiner with new settings:
```bash
docker compose up -d
```


### Buy me a coffee
If you'd like, you can buy me a coffee! ;)

[BuyMeACoffee](buymeacoffee.com/mohsenparandvar) :coffee: