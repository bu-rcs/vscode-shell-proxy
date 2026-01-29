# Setup for the BU SCC

## Create an SSH config file
- Create a new file in a directory on your computer, you can call it anything you like but something like `qrsh_scc.conf` is recommended. 
- In that file create entries for the different type of interactive jobs you want to run. Any of the login nodes can be
chosen, although as usual scc4 requires you to be on the campus network or be connecting via the VPN. Here is an example
for a 1 core job with the specified project, and another for a 4-core job with a GPU. The qrsh/qsub options are passed using
the `-q` flag to the `vscode-shell-proxy.py` script, with the options placed in quotes:
```
Host scc-1-core
    HostName scc2.bu.edu
    User your_username
    RemoteCommand vscode-shell-proxy.py -q="-P your_project"

Host scc-1-gpu
    HostName scc2.bu.edu
    User your_username
    RemoteCommand vscode-shell-proxy.py -q="-P your_project -l gpus=1 -l gpu_c=8.0 -pe omp 4"
```

## Remote-SSH config
- Open VS Code on your compute. Install the extension called `Remote-SSH`.
- Open the Command Palette via the key combo:  `Ctrl + Shift + P` on Windows, `Cmd + Shift + P` on Mac.
- Type in `Remote-SSH:Settings` and click to open it.
- Change some options:
  - In the `Config File` section put the path to the SSH config file you just created, e.g. on Windows it'll be something like: `C:\Users\your_username\qrsh_scc.conf`
  - Increase the `Connect Timeout` option to a reasonably large value. 600 seconds is suggested. This is the maximum time spent waiting for the queue to launch your interactive job.
  - Check the box for `Enable Remote Command`.
  - Verify that these boxes are also checked: `Enable Dynamic Forwarding`, `Use Local Server`.
  - If there are any entries in the `Remote Platform` section remove them.


## Connect to an SCC Compute Node
- In the lower left of the VS Code window click the connection icon.
- Choose `Connect to Host   Remote-SSH`, then choose the typeof job that you configured in your
SSH configuration file. In the above example, the choices are `scc-1-core` and `scc-1-gpu`.
- When prompted, enter your BU password.
- Wait for the job to be scheduled, and when it is ready go ahead and start using VS Code!

  


