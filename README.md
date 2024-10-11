# uh-recon

The "Uh-Recon" tools for pre-engagement reconnaissance. 

*Might* be ready for you? See [bugs.txt](https://github.com/diemastermonkey/uh-recon/blob/main/bugs.txt)

## Synopsis
Tools used by the Unhackers team in pre-engagement reconnaisance and related tasks. 

Using Shodan  queries as a starting point, these gather various enrichment 
and summary data into "collections" stored in named subdirectories.
Additionally, they help lower Shodan API use by low-key caching data.

This is functionality of interest to pen testers, bug hunters, security researchers - hackers. 
And we're here to share!

Features:
* Abstracts Shodan CLI for noobish users
* Creates/enriches/refreshes recon data into subdirectories
* Easy-bakes the data for minimum downstream fuss
* Decreases API use by updating only after N days
* Minimal dependencies beyond Shodan CLI

Un-Features:
* Documented mostly in code
* Kinda hot mess (cleanup active)
* No log/data rotation/purge features yet

Requirements:
* Shodan CLI for your platform
* Shodan [API Key](https://account.shodan.io/)
* bash, grep, sed, awk, Python, Perl
* [Nrich](https://gitlab.com/shodan-public/nrich)

## Installation and Setup

1. Clone the repository (`/opt/` is a good place for it)

```console
gad@ghost:~$ cd /opt
gad@ghost:/opt$ git clone https://github.com/diemastermonkey/uh-recon.git
```

2. Enter your [Shodan API key](https://account.shodan.io/) in `shodan-api-key.txt`

```console
gad@ghost:/opt$ cd uh-recon
gad@ghost:/opt/uh-recon$ echo 'RWFzdGVyIGVnZ3Mgb24gdGhlIG1lbnU' > shodan-api-key.txt
```

3. Verify your key is working with `./uh-shodan-init

```console
gad@ghost:/opt/uh-recon$ ./uh-shodan-init
./uh-shodan-init : Initializing Shodan API w/key in shodan-api-key.txt ...
./uh-shodan-init : ...Successfully initialized
```

## Usage

1. Create a text file with search parameters for each collection, one per line
2. Run (or `cron`) the `./uh-recon-run` script, passing your hitlist
3. Profit

```console
gad@ghost:~$ cd /opt/uh-recon
gad@ghost:/opt/uh-recon$ cat > mylist.txt
country:us state:ca port:3389 administrator
country:us state:ca city:irvine port:80 login
^C

gad@ghost:/opt/uh-recon$ ./uh-recon-run

./uh-recon-run <file_with_recon_parameters>

gad@ghost:/opt/uh-recon$ ./uh-recon-run mylist.txt

./uh-shodan-init : Initializing Shodan API w/key in shodan-api-key.txt ...
./uh-shodan-init : ...Successfully initialized
./uh-recon-shodan-query country:us state:ca city:irvine port:80 login
./uh-recon-shodan-query : Keeping stored results < 24h old
./uh-recon-shodan-query : Contents in uh_recon_us_ca_3389_administrator
./uh-recon-shodan-query : Exiting
(...)
```

## Outputs

### Output Directories
Directories are named for their search parameters. All associated output is stored inside. 

For the query `country:us state:ca city:irvine port:3389`, this directory will be created (or updated):
```console
uh_recon_us_ca_irvine_3389/
```

### Output Files
For the query `country:us state:ca city:irvine port:3389`, the following files will be generated:
```console
uh_recon_us_ca_irvine_3389/uh_recon_shodan_us_ca_irvine_3389.domains.txt
uh_recon_us_ca_irvine_3389/uh_recon_shodan_us_ca_irvine_3389.info.txt
uh_recon_us_ca_irvine_3389/uh_recon_shodan_us_ca_irvine_3389.ip.port.txt
uh_recon_us_ca_irvine_3389/uh_recon_shodan_us_ca_irvine_3389.nrich.txt
uh_recon_us_ca_irvine_3389/uh_recon_shodan_us_ca_irvine_3389.raw.txt
uh_recon_us_ca_irvine_3389/uh_recon_shodan_us_ca_irvine_3389.stats.txt
```

Here's what each of the files contain:
* ...info.txt: Metadata about the search, parameters, and tools used
* ...stats.txt: The output of Shodan's "stats" command for this search
* ...nrich.txt: Output of Nrich provided with your search results 
* ...domains.txt: Listing and count of domains in search results
* ...ip.port.txt: Listing of only IPs and ports, one per line
* ...raw.txt: Complete raw output of your Shodan search

It will also create "...dirs.txt" and "...txt.log" files, useful for debugging/etc.

## Components
These follow a very Unix-philosophy approach: Small, simple tools that mostly do one thing, stitched as needed. Some are so simple they might not truly warrant a script, but this model minimizes overhead for quick expansion later. 

Most support both input files and pipes. More are in the works.

* [gad-frequency-count](https://github.com/diemastermonkey/uh-recon/blob/main/gad-frequency-count): How many of each in a list of things
* [gad-unescape](https://github.com/diemastermonkey/uh-recon/blob/main/gad-unescape): URLs etc in, plain text out
* [uh-recon-ip-lookup](https://github.com/diemastermonkey/uh-recon/blob/main/uh-recon-ip-lookup): Add host names to list of IPs
* [uh-recon-ip-to-nrich](https://github.com/diemastermonkey/uh-recon/blob/main/uh-recon-ip-to-nrich): Get Nrich results for list of IPs
* [uh-recon-raw-to-domains](https://github.com/diemastermonkey/uh-recon/blob/main/uh-recon-raw-to-domains): Domains only
* [uh-recon-run](https://github.com/diemastermonkey/uh-recon/blob/main/uh-recon-run): The main "run my recon" script
* [uh-recon-run-bg](https://github.com/diemastermonkey/uh-recon/blob/main/uh-recon-run-bg): Helper for logging, tailing
* [uh-recon-shodan-query](https://github.com/diemastermonkey/uh-recon/blob/main/uh-recon-shodan-query): Executes Shodan queries
* [uh-shodan-init](https://github.com/diemastermonkey/uh-recon/blob/main/uh-shodan-init): Inits Shodan API access
* [uh-shodan-to-ip-port](https://github.com/diemastermonkey/uh-recon/blob/main/uh-shodan-to-ip-port): IPs, ports only
* [uh-shodan-to-ip-services-domain](https://github.com/diemastermonkey/uh-recon/blob/main/uh-shodan-to-ip-services-domain): IPs, services by domain
* [uh-shodan-url-to-query](https://github.com/diemastermonkey/uh-recon/blob/main/uh-shodan-url-to-query): Shodan Search URI in, CLI syntax out
  

## Bugs
*So* many: [bugs.txt](https://github.com/diemastermonkey/uh-recon/blob/main/bugs.txt)

## License and Acknowledgements

Created by [Unhackers](https://unhackers.net/).

Licensed under the [GNU Lesser General Public License v3.0](LICENSE).
