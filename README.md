# uh-recon

The "Uh-Recon" tools for pre-engagement reconnaissance. 

PROBABLY NOT READY FOR YOU YET.

## Synopsis
Tools used by the Unhackers team in pre-engagement reconnaisance and related tasks. 

Using Shodan  queries as a starting point, these gather various enrichment 
and summary data into "collections" stored in named subdirectories.
Additionally, they help lower Shodan API use by low-key caching data.

This is functionality of interest to pen testers, bug hunters, security researchers - hackers. 
And we're here to share!

Features:
* Abstracts Shodan CLI for noobish users
* Creates/refreshes recon data into subdirectories
* Enriches with nrich and other tools
* Easy-bakes data so no fuss for other tools
* Decreases API use, updating only after N days
* Minimal dependencies beyond Shodan CLI

Un-Features:
* Documented mostly in code
* Kinda hot mess (cleanup active)
* No log/data rotation/purge features yet

Requirements:
* Shodan CLI for your platform
* Shodan API Key
* bash, grep, sed, awk, Python, Perl
* [Nrich](https://gitlab.com/shodan-public/nrich)

## Installation and Setup

1. Clone the repository (/opt/ is a good place)

```console
$ git clone https://github.com/diemastermonkey/uh-recon.git
```

2. Enter your Shodan API key in `shodan-api-key.txt`
3. Verify your key is working with `./uh-shodan-init

## Usage

1. Create a text file with search parameters for each colleciton, one per line
2. Run (or `cron`) the `./uh-recon-run` script, passing your hitlist
3. Profit

```console
gad@ghost:~$ cd /opt/uh-recon
gad@ghost:/opt/recon$ cat > mylist.txt
country:us state:ca port:3389 administrator
country:us state:ca city:irvine port:80 login
^C

gad@ghost:/opt/recon$ ./uh-recon-run
# Run hitlist in bg to a log so you can tail it
# Requires "$0-bg" script
# 2024/gad

./uh-recon-run <file_with_recon_parameters>

gad@ghost:/opt/recon$ ./uh-recon-run mylist.txt

gad@ghost:/opt/recon$ cat hitlist_sample.txt.log
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
Directories are named for their search parameters, and all related outputs are stored therein. 

For the query `country:us state:ca city:irvine port:3389`, this directory will be created (or updated):
```
*uh_recon_us_ca_irvine_3389*/
```

### Output Files
For the query `country:us state:ca city:irvine port:3389`, the following files will be generated:
```
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

## Components
(Coming soon: List of all scripts and what and why)

## Bugs
So, so many, see [bugs.txt](https://github.com/diemastermonkey/uh-recon/blob/main/bugs.txt)

## License and Acknowledgements

Created by [Unhackers](https://unhackers.net/).

Licensed under the [GNU Lesser General Public License v3.0](LICENSE).
