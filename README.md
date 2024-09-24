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
* Decreases API use, updating after N days
* Includes example output directory/logs/etc

Un-Features:
* Minimal dependencies beyond Shodan CLI
* Still documented mostly in code
* Still a mess (but cleanup is active)
* No cleanup/log/data rotation features at all

Requirements:
* Shodan CLI for your platform
* Shodan API Key
* bash, grep, sed, awk
* Python, Perl
* [Nrich](https://gitlab.com/shodan-public/nrich)

## Installation

```console
$ git clone https://github.com/diemastermonkey/uh-recon.git
```

## Usage

```console
$ echo 'Usage coming soon!'
```

## Outputs
(List all outputs and what and why)

### Output Directories
(Describe how they're generated)

For the query `country:us state:ca city:irvine port:3389`, this directory will be created (or updated):
```
uh_recon_us_ca_irvine_3389
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
* ...info.txt: Metadata about the search, parameters, tools, etc
* ...stats.txt: The output of Shodan's "stats" command for this search
* ...domains.txt: Listing and count of domains in search results
* ...ip.port.txt: Listing of only IPs and ports, one per line
* ...nrich.txt: Output of Nrich provided with your search results
* * ...raw.txt: Complete raw output of your Shodan search

## Components
(Coming soon: List of all scripts and what and why)

## Bugs
Soo many, see [bugs.txt](https://github.com/diemastermonkey/uh-recon/blob/main/bugs.txt)

## License and Acknowledgements

Created by [Unhackers](https://unhackers.net/).

Licensed under the [GNU Lesser General Public License v3.0](LICENSE).
