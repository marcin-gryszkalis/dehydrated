# dehydrated

![](docs/logo.jpg)

This is a client for signing certificates with an ACME-server (currently only provided by Let's Encrypt) implemented as a relatively simple bash-script.

It uses the `openssl` utility for everything related to actually handling keys and certificates, so you need to have that installed.

Other dependencies are: cURL, sed, grep, mktemp (all found on almost any system, cURL being the only exception)

Current features:
- Signing of a list of domains
- Signing of a CSR
- Renewal if a certificate is about to expire or SAN (subdomains) changed
- Certificate revocation

Please keep in mind that this software and even the acme-protocol are relatively young and may still have some unresolved issues. Feel free to report any issues you find with this script or contribute by submitting a pull request.

## Getting started

For getting started I recommend taking a look at [docs/domains_txt.md](docs/domains_txt.md), [docs/wellknown.md](docs/wellknown.md) and the [Usage](#usage) section on this page (you'll probably only need the `-c` option).

Generally you want to set up your WELLKNOWN path first, and then fill in domains.txt.

**Please note that you should use the staging URL when experimenting with this script to not hit Let's Encrypt's rate limits.** See [docs/staging.md](docs/staging.md).

If you have any problems take a look at our [Troubleshooting](docs/troubleshooting.md) guide.

## Config

dehydrated is looking for a config file in a few different places, it will use the first one it can find in this order:

- `/etc/dehydrated/config`
- `/usr/local/etc/dehydrated/config`
- The current working directory of your shell
- The directory from which dehydrated was run

Have a look at [docs/examples/config](docs/examples/config) to get started, copy it to e.g. `/etc/dehydrated/config`
and edit it to fit your needs.

## Usage:

```text
Usage: ./dehydrated [-h] [command [argument]] [parameter [argument]] [parameter [argument]] ...

Default command: help

Commands:
 --version (-v)                   Print version information
 --register                       Register account key
 --account                        Update account contact information
 --check (-x)                     Check for certificate validity, no renewal is performed
 --cron (-c)                      Sign/renew non-existent/changed/expiring certificates
 --signcsr (-s) path/to/csr.pem   Sign a given CSR, output CRT on stdout (advanced usage)
 --revoke (-r) path/to/cert.pem   Revoke specified certificate
 --cleanup (-gc)                  Move unused certificate files to archive directory
 --help (-h)                      Show help text
 --env (-e)                       Output configuration variables for use in other scripts

Parameters:
 --accept-terms                   Accept CAs terms of service
 --full-chain (-fc)               Print full chain when using --signcsr
 --ipv4 (-4)                      Resolve names to IPv4 addresses only
 --ipv6 (-6)                      Resolve names to IPv6 addresses only
 --domain (-d) domain.tld         Use specified domain name(s) instead of domains.txt entry (one certificate!)
 --keep-going (-g)                Keep going after encountering an error while creating/renewing multiple certificates in cron mode
 --force (-x)                     Force renew of certificate even if it is longer valid than value in RENEW_DAYS
 --no-lock (-n)                   Don't use lockfile (potentially dangerous!)
 --lock-suffix example.com        Suffix lockfile name with a string (useful for with -d)
 --ocsp                           Sets option in CSR indicating OCSP stapling to be mandatory
 --privkey (-p) path/to/key.pem   Use specified private key instead of account key (useful for revocation)
 --config (-f) path/to/config     Use specified config file
 --hook (-k) path/to/hook.sh      Use specified script for hooks
 --out (-o) certs/directory       Output certificates into the specified directory
 --challenge (-t) http-01|dns-01  Which challenge should be used? Currently http-01 and dns-01 are supported
 --algo (-a) rsa|prime256v1|secp384r1 Which public key algorithm should be used? Supported: rsa, prime256v1 and secp384r1
```

## Donate

I'm having fun developing dehydrated, but it takes time, and time is money, at least that's what I've been told.

I will definitively continue developing dehydrated for free, but if you want to support me you can do so using the following ways:

### PayPal

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=23P9DSJBTY7C8)

### BitCoin

Send bitcoins to 12487bHxcrREffTGwUDnoxF1uYxCA7ztKK

### Server

I'm still planning on building a bigger testing-suite for dehydrated, it would be really cool to have a big(ish) server running
in a datacenter somewhere without having to pay for it... If you are a server provider and can offer me a (dedicated!) machine,
please contact me at `donations@dehydrated.de`.

### Other ways

I always like to play around with modern(ish) network and computer gear, 10G switches and stuff, modern ARM boards
(but please not that Raspberry Pi rubbish), tiny PCs for routing, etc.

If you have something that seems of value and that you don't need anymore feel free to contact me at
`donations@dehydrated.de`.

Also here is my [Amazon Wishlist](http://www.amazon.de/registry/wishlist/1TUCFJK35IO4Q) :)

