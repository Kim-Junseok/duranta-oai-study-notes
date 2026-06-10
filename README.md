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

Optional VS Code workspace file in the parent directory:

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
    ]
}
```
