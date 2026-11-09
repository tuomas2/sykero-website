# sykero.fi

Static HTML and CSS for the Sykerö Software website.

## Development with JailBee

This project is developed extensively using [JailBee](https://jailbee.gisgro.io/).
See the [JailBee prerequisites and setup documentation](https://jailbee.gisgro.io/docs/) for Linux and Incus requirements. From the host, initialize JailBee, build its base image, and create a development container:

```sh
jailbee init
jailbee base build
jailbee new dev
jailbee shell dev
```

Inside the container, start a local preview server:

```sh
python3 -m http.server 8000 --bind 0.0.0.0
```

In another host terminal, forward that container's preview port to the host:

```sh
jailbee port to-host 8000 dev --host-port auto
```

Open `http://127.0.0.1:<assigned-host-port>/` in a browser, using the host
port reported by the command. The committed
[configuration](.jailbee/config.yaml) provides Python; no build step or parent
repository is needed. Stop the preview with Ctrl-C when done.
Keep personal agent/IDE settings and credentials in JailBee's host-local config.
Commit inside the container, then run `jailbee git pull dev` on the host;
publish from the host, not the container.
