# certbot-dns-powerdns
PowerDNS DNS Authenticator plugin for [Certbot](https://certbot.eff.org/).

This plugin is built from the ground up and follows the development style and life-cycle
of other `certbot-dns-*` plugins found in the [Official Certbot Repository](https://github.com/certbot/certbot).

#### Compatibility:
* PowerDNS Authoritative Server API
* PowerDNS-Admin API

## Installation
___NOTE__: This package is not currently published on PyPi. Waiting for [Pull Request](https://github.com/pan-net-security/certbot-dns-powerdns/pull/15) to be accepted upstream. In the meantime, please build and install manually._
```
$ git clone git@github.com:tmuncks/certbot-dns-powerdns.git
$ cd certbot-dns-powerdns
$ python3 -m build

$ sudo pip3 install certbot
$ sudo pip3 install ./dist/certbot_dns_powerdns-<version>-py2.py3-none-any.whl
```

<!--- commented out for when work is accepted upstream
```
pip install --upgrade certbot
pip install certbot-dns-powerdns
```
-->

Verify:

```
$ certbot plugins

* dns-powerdns
Description: Obtain certificates using a DNS TXT record (if you are using
PowerDNS for DNS.)
Interfaces: Authenticator, Plugin
Entry point: dns-powerdns = certbot_dns_powerdns.dns_powerdns:Authenticator
...
...
```

## Configuration
The credentials file e.g. `~/pdns-credentials.ini` should look like this:

```
dns_powerdns_api_url = https://api.mypowerdns.example.org
dns_powerdns_api_key = AbCbASsd!@34
```

## Usage
```
certbot ... \
        --authenticator dns-powerdns \
        --dns-powerdns-credentials /etc/letsencrypt/pdns-credentials.ini \
        certonly
```

## FAQ
#### Why such long name for a plugin?
This follows the upstream nomenclature: `certbot-dns-<dns-provider>`.

## Development
Create a virtualenv, install the plugin (`editable` mode),
spawn the environment and run the test:

```
virtualenv -p python3 .venv
. .venv/bin/activate
pip install -e .
docker-compose up -d
./test/run_certonly.sh test/pdns-credentials.ini
```

## License

Copyright (c) 2019 [DT Pan-Net s.r.o](https://github.com/pan-net-security)

Copyright (c) 2021 [Thomas M. Steenholdt](https://github.com/tmuncks)
