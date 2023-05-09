# `home-monitoring`

Configuration and tools to manage my home monitoring systems.

It will monitor a number of things for us:

- Internet connection: looking at upload and download speeds, but
  also the quality of the connection
- Unifi network infrastructure: (hopefully) filling some gaps in the
  capabilities of the Unifi management software
- Solar power generation: how much is our solar array generating, how
  much are we using/exporting, and so on

## Getting started

Everything is put together using [Docker
Compose](https://docs.docker.com/compose/), so you should just be able
to run:

```
docker compose up
```

Then open:

- [Grafana](http://localhost:3000/)
- [Prometheus](http://localhost:9090)

### Can't use Docker Compose?

For environments where Docker Compose won't work (for example, because
you're running a really old Mac as a server), you can run it in Vagrant
with Virtualbox like so:

```
vagrant up
```

A few things to note:
- The Vagrantfile is currently only tested in Virtualbox, and only does
  things like setting the VM's hostname using Virtualbox specific code.
- The VM is set to use bridges networking, so it will present itself a
  first-class device on your network. It assumes, however, that it
  should bridge to a network interface called `en0: Ethernet`, which you
  may not be.
- None of this has been tested outside my target machine, so may break.

## Running in the background on macOS

If you want to run this monitoring system all the time on a Mac that
operates as a server, the easiest thing to do is launch the Vagrant VM
as a macOS LaunchAgent.

To do that, you'll need to:

1. [Enable passwordless NFS mounting](https://developer.hashicorp.com/vagrant/docs/synced-folders/nfs#root-privilege-requirement)
2. Install the LaunchAgent (assuming you're in this directory):

```shell
ln -s `pwd`/macOS-LaunchAgent.plist ~/Library/LaunchAgents/com.stevemarshall.StartHomeMonitoring.plist
launchctl load ~/Library/LaunchAgents/com.stevemarshall.StartHomeMonitoring.plist
```

NB: We're currently assuming your `vagrant` is installed in
`/opt/vagrant/bin`, which mine is on the target machine, but isn't on
another. I'm not sure how to make LaunchAgents handle that for now.
