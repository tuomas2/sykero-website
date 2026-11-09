# sykero.fi

Static HTML and CSS for the Sykerö Software website.

## Development with JailBee

This project is developed extensively using [JailBee](https://jailbee.gisgro.io/).
See the [JailBee prerequisites and setup documentation](https://jailbee.gisgro.io/docs/) for Linux and Incus requirements. From the host, initialize JailBee, build its base image, and create a development container:

```sh
jailbee init
jailbee base build
jailbee new dev
jailbee tmux dev
```

Development normally happens with Claude Code inside the container. Before
creating it, enable `agents.claude.enabled` and `agents.claude.autostart`
in your host's `~/.config/jailbee/global.yaml`; `jailbee tmux dev` then attaches to
the session running Claude. Ask Claude to make changes and run the project's
builds and tests.

The committed [configuration](.jailbee/config.yaml) provides Python;
no build step or parent repository is needed.
Keep personal agent/IDE settings and credentials in JailBee's host-local config.
Commit inside the container, then run `jailbee git pull dev` on the host;
publish from the host, not the container.

## Local preview

Inside the container, run `python3 -m http.server 8000 --bind 0.0.0.0`.
On the host, run `jailbee port to-host 8000 dev --host-port auto`, then open
`http://127.0.0.1:<assigned-host-port>/` using the reported host port.
Stop the preview with Ctrl-C when done.
