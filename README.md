<h1 align="center">Web Hacking ToolKit</h1>

<p align="center">
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/actions">
		<img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/signedsecurity/web-hacking-toolkit/🎉%20CI%20to%20Docker%20Hub">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/issues?q=is:issue+is:open">
		<img alt="GitHub Open Issues" src="https://img.shields.io/github/issues-raw/signedsecurity/web-hacking-toolkit.svg">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/issues?q=is:issue+is:closed">
		<img alt="GitHub Closed Issues" src="https://img.shields.io/github/issues-closed-raw/signedsecurity/web-hacking-toolkit.svg">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/graphs/contributors">
		<img alt="GitHub contributors" src="https://img.shields.io/github/contributors/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/blob/master/LICENSE">
		<img alt="GitHub" src="https://img.shields.io/github/license/signedsecurity/web-hacking-toolkit">
	</a>
</p>

<p align="center">
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Automated build" src="https://img.shields.io/docker/automated/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Starts" src="https://img.shields.io/docker/stars/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Image Size" src="https://img.shields.io/docker/image-size/signedsecurity/web-hacking-toolkit/latest">
	</a>
</p>

A web hacking toolkit docker image with GUI applications support.

## Resources

* [Installation](#installation)
    * [Docker](#docker)
    * [Docker Compose](#docker-compose)
    * [Build from Source](#build-from-source)
* [GUI Support](#gui-support)
    * [Using SSH with X11 forwarding](#using-ssh-with-x11-forwarding)
* [Installed](#installed)
    * [Tools](#tools)
    * [Wordlists](#wordlists)

## Installation

### Docker

Pull the image from Docker Hub:

```bash
docker pull signedsecurity/web-hacking-toolkit
```

Run a container and attach a shell:

```bash
docker run \
	-it \
	--rm \
	--shm-size="2g" \
	--name web-hacking-toolkit \
	--hostname web-hacking-toolkit \
	-p 22:22 \
	-v $(pwd)/data:/root/data \
	signedsecurity/web-hacking-toolkit \
	/bin/bash
```
### Docker Compose

Docker-Compose can also be used.

```yaml
version: "3.9"

services:
    web-hacking-toolkit:
        image: signedsecurity/web-hacking-toolkit
        container_name: web-hacking-toolkit
        hostname: web-hacking-toolkit
        stdin_open: true
        shm_size: 2gb # increase shared memory size to prevent firefox from crashing
        ports:
            - "22:22" # exposed for GUI support sing SSH with X11 forwarding
        volumes:
            - ./data:/root/data
        restart: unless-stopped
```

Build and run container:

```bash
docker-compose up
```

Attach shell:

```bash
docker-compose exec web-hacking-toolkit /bin/bash
```

### Build from Source

Clone this repository and build the image:

```bash
git clone https://github.com/signedsecurity/web-hacking-toolkit.git && \
cd web-hacking-toolkit && \
make build-image
```

Run a container and attach a shell:

```bash
make run
```

## GUI Support

By default, no GUI tools can be run in a Docker container as no X11 server is available. To run them, you must change that. What is required to do so depends on your host machine. If you:

* run on Linux, you probably have X11
* run on Mac OS, you need Xquartz (`brew install Xquartz`)
* run on Windows, you have a problem

### Using SSH with X11 forwarding

Use X11 forwarding through SSH if you want to go this way. Run `start_ssh` inside the container to start the server, make sure you expose port 22 when starting the container: `docker run -p 127.0.0.1:22:22 ...`, then use `ssh -X ...` when connecting (the script prints the password).

## Installed
### Tools

| Category  | Name | Description |
| :-------- | :--- | :---------- |
| Discovery/DOMAIN | [Amass](https://github.com/OWASP/Amass) | In-depth Attack Surface Mapping and Asset Discovery |
| Utility/ANY | [anew](https://github.com/tomnomnom/anew) | A tool for adding new lines to files, skipping duplicates |
| Discovery/PARAM| [Arjun](https://github.com/s0md3v/Arjun) | HTTP parameter discovery suite. |
| Army-Knife/PROXY | [Burp Suite Community](https://portswigger.net/burp) | The BurpSuite Project  community edition. |
| Utility/HTTP | [curl](https://github.com/curl/curl) | A command line tool and library for transferring data with URL syntax, supporting HTTP, HTTPS, FTP, FTPS, GOPHER, TFTP, SCP, SFTP, SMB, TELNET, DICT, LDAP, LDAPS, MQTT, FILE, IMAP, SMTP, POP3, RTSP and RTMP. libcurl offers a myriad of powerful features |
| Discovery/DNS | [dnsx](https://github.com/projectdiscovery/dnsx) | dnsx is a fast and multi-purpose DNS toolkit allow to run multiple DNS queries of your choice with a list of user-supplied resolvers. |
| Discovery/FUZZ | [ffuf](https://github.com/ffuf/ffuf) | Fast web fuzzer written in Go |
| Discovery/DOMAIN | [findomain](https://github.com/Edu4rdSHL/findomain) | The fastest 
| Browser | [firefox](https://www.mozilla.org/en-US/firefox/new/) | Safe and easy web browser from Mozilla |and cross-platform subdomain enumerator, do not waste your time. |
| Utility/SHOT | [gowitness](https://github.com/sensepost/gowitness) | mag gowitness - a golang, web screenshot utility using Chrome Headless |
| Misc | [html-tool](https://github.com/tomnomnom/hacks/tree/master/html-tool) | Take URLs or filenames for HTML documents on stdin and extract tag contents, attribute values, or comments |
| Utility/HTTP | [httpx](https://github.com/projectdiscovery/httpx) | httpx is a fast and multi-purpose HTTP toolkit allow to run multiple probers using retryablehttp library, it is designed to maintain the result reliability with increased threads. |
| Discovery/PORT | [masscan](https://github.com/robertdavidgraham/masscan) | TCP port scanner, spews SYN packets asynchronously, scanning entire Internet in under 5 minutes. |
| Discovery/PORT | [naabu](https://github.com/projectdiscovery/naabu) | A fast port scanner written in go with focus on reliability and simplicity. Designed to be used in combination with other tools for attack surface discovery in bug bounties and pentests |
| Discovery/PORT | [nmap](https://github.com/nmap/nmap) | Nmap - the Network Mapper. Github mirror of official SVN repository. |
| Army-Knife/SCAN | [nuclei](https://github.com/projectdiscovery/nuclei) | Nuclei is a fast tool for configurable targeted scanning based on templates offering massive extensibility and ease of use. |
| Discovery/PORT | [ps.sh](https://github.com/enenumxela/ps.sh) | A wrapper around tools used for port scanning(nmap, naabu & masscan), the goal being reducing scan time, increasing scan efficiency and automating the workflow. |
| Discovery/DOMAIN | [sigsubfind3r](https://github.com/signedsecurity/sigsubfind3r) | A subdomain discovery tool - it gathers a list of subdomains passively using various online sources. |
| Discovery/URL | [sigurlfind3r](https://github.com/signedsecurity/sigurlfind3r) | A passive reconnaissance tool for known URLs discovery - it gathers a list of URLs passively using various online sources. |
| Army-Knife/SCAN | [sigurlscann3r](https://github.com/signedsecurity/sigurlscann3r) | A web application attack surface mapping tool. It takes in a list of urls then performs numerous probes |
| Discovery/DOMAIN | [subdomains.sh](https://github.com/enenumxela/subdomains.sh) | A wrapper around for subdomains gathering tools (amass, subfinder, findomain & sigsubfind3r) to increase gathering efficiency and automating the workflow. |
| Discovery/DOMAIN | [subfinder](https://github.com/projectdiscovery/subfinder) | Subfinder is a subdomain discovery tool that discovers valid subdomains for websites. Designed as a passive framework to be useful for bug bounties and safe for penetration testing. |
| Utility/Terminal | [tmux](https://github.com/tmux/tmux) | tmux is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a single screen. tmux may be detached from a screen and continue running in the background, then later reattached |
| Utility/URL | [urlx](https://github.com/enenumxela/urlx) | A go(golang) utility for URLs parsing & pull out bits of the URLS. |
| Utility/Editor | [vim](https://www.vim.org/) | A highly configurable text editor built to make creating and changing any kind of text very efficient. |
| Discovery/Tech | [wappalyzer](https://github.com/aliasio/wappalyzer) | Wappalyzer identifies technologies on websites, such as CMS, web frameworks, ecommerce platforms, JavaScript libraries, analytics tools and more. |
| Utility/HTTP | [wuzz](https://github.com/asciimoo/wuzz) | Interactive cli tool for HTTP inspection |

### Wordlists

| Wordlist | Description |
| :------- | :---------- |
| [SecLists](https://github.com/danielmiessler/SecLists)  | SecLists is the security tester's companion. It's a collection of multiple types of lists used during security assessments, collected in one place. List types include usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, and many more. |
| [jhaddix](https://gist.github.com/jhaddix) / [content_discovery_all.txt](https://gist.github.com/jhaddix/b80ea67d85c13206125806f0828f4d10) | a masterlist of content discovery URLs and files (used most commonly with gobuster) |
