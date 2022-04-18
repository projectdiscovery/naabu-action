<h1 align="center">
  <img src="https://github.com/projectdiscovery/naabu/blob/master/static/naabu-logo.png" alt="naabu" width="200px">
  <br>
</h1>

<h4 align="center"><a href="https://github.com/projectdiscovery/naabu-action">Naabu Action</a> makes it easy to orchestrate <a href="https://github.com/projectdiscovery/naabu">naabu</a> with GitHub Action.</h4>



Example Usage
-----

**GitHub Action running naabu on list of hosts**

```yaml
      - name: 💥 Naabu - Port Scanner
        uses: projectdiscovery/naabu-action@main
        with:
          list: hosts.txt
```

**GitHub Action running naabu with custom port scan**

```yaml
      - name: 💥 Naabu - Port Scanner
        uses: projectdiscovery/naabu-action@main
        with:
          list: hosts.txt
          ports: "80,443"
```

**Example workflow** - `.github/workflows/naabu.yml`


```yaml
name: 💥 Naabu - Port Scanner

on:
    schedule:
      - cron: '0 0 * * *'
    workflow_dispatch:

jobs:
  naabu-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-go@v3
        with:
          go-version: 1.17

      - name: 💥 Naabu - Port Scanner
        uses: projectdiscovery/naabu-action@main
        with:
          list: hosts.txt

      - name: GitHub Workflow artifacts
        uses: actions/upload-artifact@v2
        with:
          name: naabu.log
          path: naabu.log
```


Available Inputs
------

| Key      | Description                                      | Required |
|----------|--------------------------------------------------|----------|
| `list`   | List of hosts to perform port scan               | true     |
| `ports`  | Ports to scan for (default - Top 100)            | false    |
| `rate`   | Rate of port scan probes                         | false    |
| `output` | File to save output result (default - naabu.log) | false    |
| `json`   | Write results in JSON format                     | false    |
| `flags`  | Additional naabu CLI flags to use                | false    |
