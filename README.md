

## Steps to Reproduce

Install proto globally:
```sh
bash <(curl -fsSL https://moonrepo.dev/install/proto.sh)
```

Setup shell:
```sh
$ proto setup

│ SUCCESS
│ Successfully installed proto to ~/.proto/bin/proto!
│ Need help? Join our Discord https://discord.gg/qCh9MEynv2
```

Now from the root of the repo, install toolchain:
```sh
$ proto install
bun

│ SUCCESS
│ Installed bun in 0s!
```

`bun` points to shim:
```sh
$ which bun
~/.proto/shims/bun
```

Run package.json `repro` script. The script just prints out whether it is being
run under Bun or not. The script contains a `#!/usr/bin/env node` shebang,
which can be overriden via the `--bun` flag.

| Command | Expected | Actual |
| ----- | ----- | ----- |
| `bun repro` | `Got Bun? false` | `Got Bun? false` |
| `bun --bun repro` | `Got Bun? true` | `Got Bun? false` |
| `~/.proto/bin/bun repro` | `Got Bun? false` | `Got Bun? false` |
| `~/.proto/bin/bun --bun repro` | `Got Bun? true` | `Got Bun? true` |

So the behavior and results are different when running `bun` via the shim vs.
the original executable.
