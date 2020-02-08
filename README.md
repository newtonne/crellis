# Crellis
[![Release](https://img.shields.io/github/release/roots/trellis.svg?style=flat-square)](https://github.com/roots/trellis/releases)
[![Build Status](https://img.shields.io/circleci/build/gh/newtonne/crellis?style=flat-square)](https://circleci.com/gh/newtonne/crellis)

Ansible playbooks for setting up a LEMP stack for Craft 3. This is a fork of [Trellis](https://github.com/roots/trellis), which does the same thing for WordPress.

- Local development environment with Vagrant
- High-performance production servers
- Zero-downtime deploys for your Craft sites

## What's included

Crellis will configure a server with the following and more:

* Ubuntu 18.04 Bionic LTS
* Nginx (with optional FastCGI micro-caching)
* PHP 7.3
* MariaDB (a drop-in MySQL replacement)
* SSL support (scores an A+ on the [Qualys SSL Labs Test](https://www.ssllabs.com/ssltest/))
* Let's Encrypt for free SSL certificates
* HTTP/2 support (requires SSL)
* sSMTP (mail delivery)
* MailHog
* Memcached
* Fail2ban and ferm

## Documentation

Full documentation is available at [https://roots.io/trellis/docs/](https://roots.io/trellis/docs/).

## Requirements

Make sure all dependencies have been installed before moving on:

* [Virtualbox](https://www.virtualbox.org/wiki/Downloads) >= 4.3.10
* [Vagrant](https://www.vagrantup.com/downloads.html) >= 2.1.0

**Windows user?** [Read the Windows getting started docs](https://roots.io/getting-started/docs/windows-development-environment-trellis/) for slightly different installation instructions.

## Installation

The recommended directory structure for a Crellis project looks like:

```shell
example.com/      # → Root folder for the project
├── crellis/      # → Your clone of this repository
└── site/         # → A Craft site ([Craft's directory structure](https://docs.craftcms.com/v3/directory-structure.html))
```

See a complete working example in the [roots-example-project.com repo](https://github.com/roots/roots-example-project.com).



1. Create a new project directory:
```plain
$ mkdir example.com && cd example.com
```
2. Install Crellis:
```plain
$ git clone --depth=1 git@github.com:newtonne/crellis.git && rm -rf crellis/.git
```
3. Install Craft into the `site` directory:
```plain
$ composer create-project craftcms/craft site
```

## Local development setup

1. Configure your Craft sites in `group_vars/development/craft_sites.yml` and in `group_vars/development/vault.yml`
2. Ensure you're in the crellis directory: `cd crellis`
3. Run `vagrant up`

[Read the local development docs](https://roots.io/trellis/docs/local-development-setup/) for more information.

## Remote server setup (staging/production)

A base Ubuntu 18.04 (Bionic) server is required for setting up remote servers.

1. Configure your Craft sites in `group_vars/<environment>/craft_sites.yml` and in `group_vars/<environment>/vault.yml` (see the [Vault docs](https://roots.io/trellis/docs/vault/) for how to encrypt files containing passwords)
2. Add your server IP/hostnames to `hosts/<environment>`
3. Specify public SSH keys for `users` in `group_vars/all/users.yml` (see the [SSH Keys docs](https://roots.io/trellis/docs/ssh-keys/))

For remote servers, installing Ansible locally is an additional requirement. See the [docs](https://roots.io/trellis/docs/remote-server-setup/#requirements) for more information.

Provision the server:
```bash
$ ansible-playbook server.yml -e env=<environment>
```

[Read the remote server docs](https://roots.io/trellis/docs/remote-server-setup/) for more information.

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

[Read the deploys docs](https://roots.io/trellis/docs/deploys/) for more information.

## Contributing

Contributions are welcome from everyone. We have [contributing guidelines](https://github.com/roots/guidelines/blob/master/CONTRIBUTING.md) to help you get started.

## Trellis sponsors

Help support our open-source development efforts by [becoming a patron](https://www.patreon.com/rootsdev).

<a href="https://kinsta.com/?kaid=OFDHAJIXUDIV"><img src="https://cdn.roots.io/app/uploads/kinsta.svg" alt="Kinsta" width="200" height="150"></a> <a href="https://k-m.com/"><img src="https://cdn.roots.io/app/uploads/km-digital.svg" alt="KM Digital" width="200" height="150"></a> <a href="https://scaledynamix.com/"><img src="https://cdn.roots.io/app/uploads/scale-dynamix.svg" alt="Scale Dynamix" width="200" height="150"></a>

## Community

Keep track of development and community news.

* Participate on the [Roots Discourse](https://discourse.roots.io/)
* Follow [@rootswp on Twitter](https://twitter.com/rootswp)
* Read and subscribe to the [Roots Blog](https://roots.io/blog/)
* Subscribe to the [Roots Newsletter](https://roots.io/subscribe/)
* Listen to the [Roots Radio podcast](https://roots.io/podcast/)
