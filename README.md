# duranta-oai-study-notes

Minimal study notes workspace for the Duranta OpenAirInterface RAN/UE repository.

## Clone

Create one parent directory and clone both repositories side by side:

```bash
mkdir ran-code
cd ran-code

git clone --branch develop https://github.com/duranta-project/openairinterface5g.git duranta-openairinterface5g
git clone https://github.com/Kim-Junseok/duranta-oai-study-notes.git duranta-oai-study-notes
```

Expected layout:

```text
ran-code/
├── duranta-openairinterface5g/
├── duranta-oai-study-notes/
└── ran-code.code-workspace
```

Create `ran-code.code-workspace` in the parent directory:

```json
{
    "folders": [
        {
            "path": "duranta-openairinterface5g",
            "name": "duranta-openairinterface5g"
        },
        {
            "path": "duranta-oai-study-notes",
            "name": "duranta-oai-study-notes"
        }
    ],
    "settings": {
        "cmake.useCMakePresets": "always",
        "cmake.configureOnOpen": false,
        "C_Cpp.default.configurationProvider": "",
        "C_Cpp.default.compileCommands": "${workspaceFolder:duranta-openairinterface5g}/cmake_targets/ran_build/vscode-intellisense/compile_commands.json",
        "C_Cpp.default.includePath": [
            "${workspaceFolder:duranta-openairinterface5g}",
            "${workspaceFolder:duranta-openairinterface5g}/nfapi/oai_integration"
        ],
        "C_Cpp.default.compilerPath": "/usr/bin/gcc",
        "C_Cpp.default.cStandard": "gnu11",
        "C_Cpp.default.cppStandard": "gnu++17",
        "C_Cpp.default.intelliSenseMode": "linux-gcc-x64",
        "C_Cpp.errorSquiggles": "enabled",
        "C_Cpp.intelliSenseEngine": "default",
        "C_Cpp.default.browse.path": [
            "${workspaceFolder:duranta-openairinterface5g}",
            "${workspaceFolder:duranta-openairinterface5g}/nfapi/oai_integration"
        ]
    }
}
```

Open it with:

```bash
code ran-code.code-workspace
```

## Packages

Install the code-reading and local-simulation package set:

```bash
cd duranta-oai-study-notes
sudo apt-get update
sudo apt-get install -y $(grep -vE "^\s*(#|$)" requirements.txt)
```

This package list intentionally avoids SDR-specific dependencies such as UHD/USRP drivers.

## IntelliSense

Most include-path red lines in VS Code disappear after CMake generates `compile_commands.json` for the Duranta checkout.

From the parent directory:

```bash
cmake \
  -S duranta-openairinterface5g \
  -B duranta-openairinterface5g/cmake_targets/ran_build/vscode-intellisense \
  -G Ninja \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
  -DAUTO_DOWNLOAD_ASN1C=ON \
  -DASN1C_EXEC= \
  -DASN1C_EXEC_PATH= \
  -DCPM_SOURCE_CACHE=duranta-openairinterface5g/cmake_targets/ran_build/cpm-cache
```

The expected file is:

```text
duranta-openairinterface5g/cmake_targets/ran_build/vscode-intellisense/compile_commands.json
```

After it exists, run these VS Code commands:

```text
Developer: Reload Window
C/C++: Reset IntelliSense Database
```

A full SDR build is not required just to resolve headers like `PHY/defs_gNB.h`. Some generated headers may still require building generator targets later, but the first step is the CMake configure above.
