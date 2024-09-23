# uh-recon

The "Uh-Recon" tools for pre-engagement reconnaissance. PROBABLY NOT READY FOR YOU YET.

## Synopsis
Tools used by the Unhackers team in pre-engagement reconnaisance and related tasks. 

Using Shodan  queries as a starting point, these gather various enrichment 
and summary data into "collections" stored in named subdirectories.
Additionally, they limit query API use by refreshing data at most 
once per day (soon to be configurable).

This functionality overlaps with those of interest to pen testers, 
bug hunters, security researchers. And you're welcome to them!

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
* BASH, grep, sed, awk
* Python, Perl
* [Nrich](https://gitlab.com/shodan-public/nrich)

## Installation

```console
$ git clone https://github.com/diemastermonkey/uh-recon.git
```

## Usage

## Bugs

## License and Acknowledgements

Created by [Unhackers](https://unhackers.net/).
Licensed under the [GNU Lesser General Public License v3.0](LICENSE).

The Kit

  -

The Bugs
  
  So many, see bugs.txt

Configuration

  Pending

Execution

  Pending

Outputs

  Pending


