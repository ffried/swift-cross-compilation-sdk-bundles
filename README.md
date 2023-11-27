# Swift Cross-compilation SDK bundles

Stores cross compilation sdk bundles aligned with Swift releases.
A release is created for each Swift release. The assets on the release contain the SDK bundles.

The bundles are created using the [Swift SDK Generator](https://github.com/apple/swift-sdk-generator) tool.

To install a (existing) bundle, use the following GitHub action:

```yaml
- uses: ffried/swift-cross-compilation-sdk-bundles/actions/setup@main
  id: install-sdk
  with:
    swift-version: 5.9.1
    host-os: macos # must be macos
    host-os-version: 13
    host-arch: x86_64 # or arm64
    target-os: ubuntu
    target-os-version: '22.04'
    target-arch: x86_64 # or arm64
```

The output named `sdk-bundle-name` can be used for running builds with the SDK:

```yaml
- name: Build using SDK
  env:
    SDK_BUNDLE: ${{ steps.install-sdk.outputs.sdk-bundle-name }}
  run: swift build --experimental-swift-sdk "${SDK_BUNDLE}"
```
