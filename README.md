# setup-xcode
This action is intended to switch between pre-installed versions of Xcode for macOS images in GitHub Actions.

The list of all available versions can be found in [runner-images](https://github.com/actions/runner-images/blob/master/images/macos/macos-13-Readme.md#xcode) repository.

# Available parameters
| Argument                | Description              | Format    |
|-------------------------|--------------------------|--------------------|
| `xcode-version`           | Specify the Xcode version to use | - `latest` or<br> - `latest-stable` or<br> - [SemVer](https://semver.org/) string or<br> - `<semver>-beta` |

**Notes:**
- `latest-stable` points to the latest stable version of Xcode
- `latest` *includes* beta releases that GitHub Actions has installed
- SemVer examples: `16`, `15.4`, `15.0.1`, `^15.2.0` (find more examples in [SemVer cheatsheet](https://devhints.io/semver))
- `-beta` suffix after SemVer will only select among beta releases that GitHub Actions has installed
- If setting a specific version, wrap it in single quotes `'16.0'` to pass the YAML value as string — numbers get rounded so the resulting "16" SemVer may provide different versions than you expect…
- SemVer preference for `15.0` will select `15.0.1` if available — use `15.0.0` to limit to that exact version
- Available Xcode builds differ across GitHub runner image and macOS versions, so make sure you use a value that can be found on the runner you're using (it can also change over time — in case you start getting errors the action will tell you what versions really are availble to you)

# Usage

Set the latest stable Xcode version:
```
jobs:
  build:
    runs-on: macos-latest
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: latest-stable
```

Set the latest Xcode version including beta releases:
```
jobs:
  build:
    runs-on: macos-latest
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: latest
```

Set the specific stable version of Xcode:
```
jobs:
  build:
    runs-on: macos-14
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: '15.0.1'
```

Set the specific beta version of Xcode:
```
jobs:
  build:
    runs-on: macos-15
    steps:
    - uses: maxim-lobanov/setup-xcode@v1
      with:
        xcode-version: '26.0-beta'
```
# License
The scripts and documentation in this project are released under the [MIT License](LICENSE)
