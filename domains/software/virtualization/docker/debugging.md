---
layout: default
title: Docker Debugging
parent: Docker
nav_order: 1
---

# Debugging Docker
{: .no_toc }

## Using mitmproxy to output API calls
- check if mitmproxy is running

```
curl -x localhost:8080 http://mitm.it/cert/pem  # should print out a cert
```
- setup the mitmproxy

```
# on Ubuntu
MITM_CERT_PATH=/usr/local/share/ca-certificates/mitmproxy.crt
sudo cp ~/.mitmproxy/mitmproxy-ca-cert.cer "$MITM_CERT_PATH"
sudo chown root:root "$MITM_CERT_PATH"
sudo chmod 644 "$MITM_CERT_PATH"
sudo update-ca-certificates

# on Arch Linux
MITM_CERT_PATH=/etc/ca-certificates/trust-source/anchors/
sudo cp ~/.mitmproxy/mitmproxy-ca-cert.cer "$MITM_CERT_PATH"
sudo chown root:root "$MITM_CERT_PATH"
sudo chmod 644 "$MITM_CERT_PATH"
sudo trust extract-compat
```
- verify MITM root cert accepted

```
curl -x localhost:8080 https://sha256.badssl.com/
```
- remove certificate

```
sudo rm "$MITM_CERT_PATH"
sudo trust extract-compat
```
- Also see `man 8 update-ca-trust` and `trust --help`
- run `dockerd` with `HTTPS_PROXY` set

```
sudo HTTPS_PROXY=http://localhost:8080/ dockerd  # bash
```
- run `ducker pull ubuntu` and inspect `mitmproxy` output
- saving a `mitmproxy` flow

```
:save.file @all <location>
```

