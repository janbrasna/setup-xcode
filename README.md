# setup-xcode
This action is intended to switch between pre-installed versions of Xcode for macOS images in GitHub Actions.

The list of all available versions can be found in [runner-images](https://github.com/actions/runner-images/blob/master/images/macos/macos-13-Readme.md#xcode) repository.

# Available parameters
| Argument                | Description              | Format    |
|-------------------------|--------------------------|--------------------|
| `xcode-version`           | Specify the Xcode version to use | - `latest` or<br> - `latest-stable` or<br> - [SemVer](https://semver.org/) string or<br> - `<semver>-beta` |

**Notes:**
- `latest-stable` points to the latest stable version of Xcode
- `latest` *includes* beta releases that GitHub actions has installed
- SemVer examples: `14`, `14.1`, `14.3.1`, `^14.3.0` (find more examples in [SemVer cheatsheet](https://devhints.io/semver))
- `-beta` suffix after SemVer will only select among beta releases that GitHub actions has installed
- If sets a specific version, wraps it to single quotes in YAML like `'12.0'` to pass it as string because GitHub trimmes trailing `.0` from numbers

# Usage

Set the latest stable Xcode version:
```yaml
jobs:
  build:
    runs-on: macos-latest
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: latest-stable
```

Set the latest Xcode version including beta releases:
```yaml
jobs:
  build:
    runs-on: macos-latest
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: latest
```

Set the specific stable version of Xcode:
```yaml
jobs:
  build:
    runs-on: macos-13
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: '14.3.1'
```

Set the specific beta version of Xcode:
```yaml
jobs:
  build:
    runs-on: macos-13
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: '15.0-beta'
```

# Outputs

The action sets the selected `version` and its `path` to the outputs for further reference:
```yaml
jobs:
  build:
    runs-on: macos-latest
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      id: setup_xcode
      with:
        xcode-version: 16
    - name: Echo selected Xcode values to environment variables
      run: |
        echo "XCODE_VERSION=${{ steps.setup_xcode.outputs.version }}" >> $GITHUB_ENV
        echo "XCODE_PATH=${{ steps.setup_xcode.outputs.path }}" >> $GITHUB_ENV
```

# License
The scripts and documentation in this project are released under the [MIT License](LICENSE)
