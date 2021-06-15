# pcorning-av - Phil Corning's AVs

## from-source
Docker-based cluster with 2 Nodes.
After `./run` is executed it will be setup for BDR development and fully functional for BDR `make installcheck` tests.

**Before executing the `run` script:**
- The `~/.ssh/id_ed25519` GITHUB SSH key must be present in your user's home directory
- The `TPA_2Q_SUBSCRIPTION_TOKEN` must be set in your user's environment
- Edit the variables at the top of `hooks/post-deploy.yml`:
    - Set `user_info.name` and `user_info.email` for your GIT user
    - Set `*.git_ref` values to the desired environment GIT branches
    - Set `run_pg_installcheck` to enable/disable postgres installcheck

**Use Notes:**
- `./run`
    - No arguments = Full cluster build (will destroy current cluster if already present)
    - Any argument = Rebuild (excutes `hooks/post-deploy.yml` only)
- Connect to nodes with `ssh -F ssh_config node*`
- Configure vscode to use the `ssh_config` file to connect to node(s)
- All source is located in the `/opt/postgres/src` directory
- (Optional) Postgres installcheck is run during cluster setup to enable the BDR check, installcheck, and installcheck_local "make" options (Errors are ignored as they don't matter)
- The `/opt/postgres/src/NODE*_workspace.code-workspace` vscode Workspace is pre-configured to edit/build/install BDR (debugging does not currently work)
- Sometimes (Ubuntu) the `sysstat` service restart fails during `./run`, execute again if this happens

**TODO:**
- `hooks/post-deploy.yml`
    - `make_opt.num_threads` doesn't seem to work
    - Move the user/branch variables somewhere else, so they don't need to be edited
- vscode: Get BDR debugging to work
- sysstat: Why does this fail sometimes?
