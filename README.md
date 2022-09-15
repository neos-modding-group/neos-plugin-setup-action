# neos-plugin-setup-action

This action sets up a build environment for Neos plugins. More specifically, it does the following:

1. Installs .NET version 6.0.x
2. Fetches the latest Neos version and installs it in `./neos_install`. So if you needed `FrooxEngine.dll`, it would be located in `./neos_install/Neos_Data/Managed/FrooxEngine.dll`.
3. Caches the Neos install for reuse in subsequent action runs

## Usage

Example where where `NeosModLoader.sln` expects a Neos install to exist on `$NeosPath`:

```yml
name: Test
on: [push, pull_request]

env:
  NeosPath: "${{ github.workspace }}/neos_install/"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: checkout NML
        uses: actions/checkout@v3
      - name: setup build environment
        uses: neos-modding-group/neos-plugin-setup-action@master
      - name: lint
        run: dotnet format --verbosity detailed --verify-no-changes ./NeosModLoader.sln
      - name: build
        run: dotnet build ./NeosModLoader.sln --configuration Release
```
