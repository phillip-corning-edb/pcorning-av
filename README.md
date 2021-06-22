# pcorning-av - Phil Corning's AVs

## from-source
Docker-based cluster with 2 Nodes.
After `./run` is executed it will be setup for BDR development and fully functional for BDR `make installcheck` tests.

**Before executing the `run` script:**
- The `~/.ssh/id_ed25519` github ssh key must be present in your user's home directory
- The `TPA_2Q_SUBSCRIPTION_TOKEN` must be set in your user's environment
- Edit the JSON config in the `run` script:
    - Set `user_info.name` and `user_info.email` for your GIT user (leave empty to skip)
    - Set `dev_branches` values to the desired environment GIT branches (leave empty to use defaults, see `hooks/post-deploy.yml`)
    - Set `run_pg_installcheck` to enable/disable postgres installcheck
    - Verify `make_num_threads` is set appropriately for your machine's CPU cores

**Use Notes:**
- `./run`
    - No arguments = Full cluster build (will destroy current cluster if already present)
    - Any argument = Rebuild (excutes `hooks/post-deploy.yml` only)
- Connect to nodes with `ssh -F ssh_config node#`
- All source is located in the `/opt/postgres/src` directory (also the postgres user's home directory)
- (Optional) Postgres installcheck is run during cluster setup to enable the BDR check, installcheck, and installcheck_local "make" options (Errors are ignored as they don't matter)
- The `/opt/postgres/src/NODE*_workspace.code-workspace` vscode Workspace is pre-configured to edit/build/install BDR (debugging does not currently work)
- Sometimes (Ubuntu) the `sysstat` service restart fails during `./run`, execute `./run` again if this happens

**TODO:**
- vscode: Get BDR debugging to work
- sysstat: Why does this fail sometimes?
