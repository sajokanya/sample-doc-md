# Table of contents

* [Cirrus Sync Documentation](README.md)

## General

* [Changelog](changelog.md)
* [Getting started](getting-started.md)
* [Quick Setup](general/quick-setup.md)
* [Release Notes](general/release-notes.md)

## Users

* [User guide](user-guide/user-guide.md)

## Developers

* [Developer Guide](developer-guide/README.md)
  * [API Reference](developer-guide/api-reference.md)
  * [Configuration](developer-guide/configuration.md)
  * [Troubleshooting](developer-guide/troubleshooting.md)

***

* ```yaml
  type: builtin:openapi
  props:
    models: true
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: docs-test-gitbook-api
  ```
