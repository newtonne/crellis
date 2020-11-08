<h1 align="center">
  Crellis
</h1>

<p align="center">
  <a href="LICENSE.md">
    <img alt="MIT License" src="https://img.shields.io/github/license/newtonne/crellis?color=%23525ddc&style=flat-square" />
  </a>

  <a href="https://github.com/roots/trellis/releases">
    <img alt="Release" src="https://img.shields.io/github/release/roots/trellis.svg?style=flat-square" />
  </a>

  <a href="https://circleci.com/gh/newtonne/crellis">
    <img alt="Build Status" src="https://img.shields.io/circleci/build/gh/newtonne/crellis?style=flat-square" />
  </a>

  <a href="https://twitter.com/rootswp">
    <img alt="Follow Roots" src="https://img.shields.io/twitter/follow/rootswp.svg?style=flat-square&color=1da1f2" />
  </a>
</p>

<p align="center">
  <strong>Ansible-powered LEMP stack for Craft 3.</strong>
  <br />
  Fork of Trellis, an Ansible-powered LEMP stack for WordPress
  <br />
  Built with ❤️
</p>

<p align="center">
  <a href="https://roots.io">Official Website</a> | <a href="https://roots.io/docs/trellis/master/installation/">Documentation</a> | <a href="CHANGELOG.md">Change Log</a>
</p>

## Supporting

**Trellis** (Crellis' upstream) is an open source project and completely free to use.

However, the amount of effort needed to maintain and develop new features and products within the Roots ecosystem is not sustainable without proper financial backing. If you have the capability, please consider donating using the links below:

<div align="center">

[![Donate via Patreon](https://img.shields.io/badge/donate-patreon-orange.svg?style=flat-square&logo=patreon")](https://www.patreon.com/rootsdev)
[![Donate via PayPal](https://img.shields.io/badge/donate-paypal-blue.svg?style=flat-square&logo=paypal)](https://www.paypal.me/rootsdev)

</div>

## Overview

Ansible playbooks for setting up a LEMP stack for Craft 3

- Local development environment with Vagrant
- High-performance production servers
- Zero-downtime deploys for your Craft sites

## What's included

Crellis will configure a server with the following and more:

- Ubuntu 18.04 Bionic LTS
- Nginx (with optional FastCGI micro-caching)
- PHP 7.4
- MariaDB (a drop-in MySQL replacement)
- SSL support (scores an A+ on the [Qualys SSL Labs Test](https://www.ssllabs.com/ssltest/))
- Let's Encrypt for free SSL certificates
- HTTP/2 support (requires SSL)
- Composer
- sSMTP (mail delivery)
- MailHog
- Memcached
- Fail2ban and ferm

## Documentation

Full documentation is available at [https://roots.io/docs/trellis/master/installation/](https://roots.io/docs/trellis/master/installation/).

## Requirements

Make sure all dependencies have been installed before moving on:

- [Virtualbox](https://www.virtualbox.org/wiki/Downloads) >= 4.3.10
- [Vagrant](https://www.vagrantup.com/downloads.html) >= 2.1.0

**Windows user?** [Read the Windows getting started docs](https://roots.io/docs/getting-started/windows/#working-with-trellis) for slightly different installation instructions.

## Installation

The recommended directory structure for a Crellis project looks like:

```bash
example.com/      # → Root folder for the project
├── crellis/      # → Your clone of this repository
└── site/         # → A Craft site ([Craft's directory structure](https://docs.craftcms.com/v3/directory-structure.html))
```

1. Create a new project directory:

```bash
$ mkdir example.com && cd example.com
```

2. Install Crellis:

```bash
$ git clone --depth=1 git@github.com:newtonne/crellis.git && rm -rf crellis/.git
```

3. Install Craft into the `site` directory:

```bash
$ composer create-project craftcms/craft site
```

## Local development setup

1. Configure your Craft sites in `group_vars/development/craft_sites.yml` and in `group_vars/development/vault.yml`
2. Ensure you're in the crellis directory: `cd crellis`
3. Run `vagrant up`

[Read the local development docs](https://roots.io/docs/trellis/master/local-development) for more information.

## Remote server setup (staging/production)

A base Ubuntu 18.04 (Bionic) server is required for setting up remote servers.

1. Configure your Craft sites in `group_vars/<environment>/craft_sites.yml` and in `group_vars/<environment>/vault.yml` (see the [Vault docs](https://roots.io/docs/trellis/master/vault/) for how to encrypt files containing passwords)
2. Add your server IP/hostnames to `hosts/<environment>`
3. Specify public SSH keys for `users` in `group_vars/all/users.yml` (see the [SSH Keys docs](https://roots.io/docs/trellis/master/ssh-keys/))

For remote servers, installing Ansible locally is an additional requirement. See the [docs](https://roots.io/docs/trellis/master/remote-server-setup/#requirements) for more information.

Provision the server:

```bash
$ ansible-playbook server.yml -e env=<environment>
```

[Read the remote server docs](https://roots.io/docs/trellis/master/remote-server-setup/) for more information.

## Deploying to remote servers

1. Add the `repo` (Git URL) of your Craft project in the corresponding `group_vars/<environment>/craft_sites.yml` file
2. Set the `branch` you want to deploy (defaults to `master`)

Deploy a site:

```bash
$ ./bin/deploy.sh <environment> <site>
```

Rollback a deploy:

```bash
$ ansible-playbook rollback.yml -e "site=<site> env=<environment>"
```

[Read the deploys docs](https://roots.io/docs/trellis/master/deployments/) for more information.

## Contributing

Contributions are welcome from everyone. We have [contributing guidelines](https://github.com/roots/guidelines/blob/master/CONTRIBUTING.md) to help you get started.

## Trellis sponsors

Help support our open-source development efforts by [becoming a patron](https://www.patreon.com/rootsdev).

<a href="https://kinsta.com/?kaid=OFDHAJIXUDIV"><img src="https://cdn.roots.io/app/uploads/kinsta.svg" alt="Kinsta" width="200" height="150"></a> <a href="https://k-m.com/"><img src="https://cdn.roots.io/app/uploads/km-digital.svg" alt="KM Digital" width="200" height="150"></a> <a href="https://carrot.com/"><img src="https://cdn.roots.io/app/uploads/carrot.svg" alt="Carrot" width="200" height="150"></a> <a href="https://www.c21redwood.com/"><img src="https://cdn.roots.io/app/uploads/c21redwood.svg" alt="C21 Redwood Realty" width="200" height="150"></a>

## Community

Keep track of development and community news.

- Participate on the [Roots Discourse](https://discourse.roots.io/)
- Follow [@rootswp on Twitter](https://twitter.com/rootswp)
- Read and subscribe to the [Roots Blog](https://roots.io/blog/)
- Subscribe to the [Roots Newsletter](https://roots.io/subscribe/)
- Listen to the [Roots Radio podcast](https://roots.io/podcast/)
