# uh-recon

The "Uh-Recon" tools for pre-engagement reconnaissance. PROBABLY NOT READY FOR YOU YET.

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
* BASH, grep, sed, awk
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
(Coming soon: List of all outputs and what and why)

## Components
(Coming soon: List of all scripts and what and why)

## Bugs
Soo many, see [bugs.txt](https://github.com/diemastermonkey/uh-recon/blob/main/bugs.txt)

## License and Acknowledgements

Created by [Unhackers](https://unhackers.net/).

Licensed under the [GNU Lesser General Public License v3.0](LICENSE).
