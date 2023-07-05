# Base installation

Follow the README.md. 

On top, might need to update the /etc/subuid and /etc/subgid with the line:

```txt
waelti:165536:65536
```

See: https://serverfault.com/q/1107086

# Intellisense configuration

> This follows the steps presented here: https://medium.com/@dcat52/vs-code-intellisense-inside-an-apptainer-container-2526380a4673 

Setup ssh by creating a `.shh/config` file with content (replace the *USERNAME* with yours): 
```txt
Host mrs_container~*
  RemoteCommand singularity shell /home/USERNAME/git/mrs/mrs_singularity/images/mrs_uav_system.sif
  RequestTTY yes

Host localhost mrs_container~localhost
  HostName 127.0.0.1
  User USERNAME
```

Install the `Remote - SSH` extension in VSCode and switch to the `Pre-release` version. Then, open the settings with `Ctrl+Shift+P` and add these lines to the settings (JSON):
```json
{
    ...,
    "remote.SSH.serverInstallPath": {
        "mrs_container~localhost": "~/.vscode-container/mrs_container",
        "ss23_container~localhost": "~/.vscode-container/ss23_container"
    },
    "remote.SSH.enableRemoteCommand": false,
    "remote.SSH.useLocalServer": true
}
```

Now, just clicking the `><` button (bottom left) and connecting to the host should work. 

To enable apps with the remote session, go to the extension pane and click `Install in SSH: ...` to enable them. 

The C/C++ standard may be modified in the `c_cpp_properties.json` file to: 
```json
"cStandard": "c17",
"cppStandard": "c++23",
```