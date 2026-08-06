## About

GitHub Action to scan .Net artifacts into a Lineai server using the Lineai .Net Agent (`lineaipublic.azurecr.io/lineai_dotnet`).


### Example

```yaml
name: lineai-scan

on:
  push:
    branches: [ "integration" ]
  pull_request:
    branches: [ "integration" ]
  workflow_dispatch:
    
jobs:
  lineai-scan:
    name: Perform Lineai Scan
    environment: Lineai Scan Env
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v4
      - name: Run the Lineai Scan
        uses: lineai-intelligence/lineai-dotnet-agent-github-action@v1
        with:
          lineai_host: ${{ vars.LINEAI_HOST }}
          agent_uuid: ${{ vars.AGENT_UUID }}
          agent_password: ${{ secrets.AGENT_PASSWORD }}
          application_name: MyApplication
          scan_space: default
          include_filter: com.example
          namespace_filter: com.example
```


## Customizing


| Name                      | Type    | Description                                                                                                                                                                                             |
|---------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `lineai_host`             | String  | The host address of the Lineai instance without the "/codelogic/ui/" part.                                                                                                                              |
| `agent_uuid`              | String  | The UUID of the Agent in Lineai.                                                                                                                                                                        |
| `agent_password`          | String  | The password for the agent.                                                                                                                                                                             |
| `application_name`        | String  | The Application node to create that will be the parent of all objects found in the scan.                                                                                                                | 
| `scan_space`              | String  | The name of the scan space that the data will be saved to. If specified, a ScanSpace with this name will be created if not found. If not specified, information will be saved to the default ScanSpace. | 
| `scan_path`               | String  | Path to the file or directory to scan. Must start with /github/workspace/. Defaults to /github/workspace.                                                                                              |
| `include_filter`          | String  | Include file path filters (comma-separated). Passed as --include.                                                                                                                                       |
| `exclusion_filter`        | String  | Exclude file path filters. Passed as --exclude / -x.                                                                                                                                                    |
| `namespace_filter`        | String  | Namespace include filter(s), comma-separated. Passed as --namespace.                                                                                                                                      |
| `database_identities`     | String  | Database identity or connection target(s) for remote SQL parse. Passed as --database.                                                                                                                   |
| `force_rescan`            | boolean | Forces the agent to rescan already scanned artifacts.                                                                                                                                                   |
| `expunge_scan_sessions`   | boolean | Instruct the server to delete all other scan sessions created by this agent and its configuration after the current scan session has completed successfully. Defaults to false.                         |
