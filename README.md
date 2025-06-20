# setup-powershell-yaml

This GitHub Action will download, install, and cache the [powershell-yaml](https://github.com/cloudbase/powershell-yaml) module from [PowerShell Gallery](https://www.powershellgallery.com/packages/powershell-yaml).

## Usage

See [action.yml](action.yml)

```yaml
uses: jimmymcpeter/setup-powershell-yaml@v1
with:
  # Version to setup. Latest version is setup if not specified. Setting a version will be fastest.
  # See https://www.powershellgallery.com/packages/powershell-yaml
  version: ""
```

**Basic:**

```yaml
- name: Setup powershell-yaml
  uses: jimmymcpeter/setup-powershell-yaml@v1
  with:
    version: "0.4.12"

- name: Use powershell-yaml
  id: parse-yaml
  shell: pwsh
  run: |
    $data = "hello: world"
    $yml = ConvertFrom-Yaml -Yaml "$data"
    $json = ConvertTo-Yaml -JsonCompatible -Data $yml;
    echo "json_out=$json" >> $ENV:GITHUB_OUTPUT

- name: Use the JSON
  shell: pwsh
  env:
    HELLO: ${{ fromJSON(needs.parse-yaml.outputs.json_out).hello }}
  run: |
    echo "Hello ${{ env.HELLO }}!"
```
