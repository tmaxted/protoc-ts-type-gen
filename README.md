# protoc-ts-type-gen

> Protoc Plugin for generating TypeScript Declarations from Protocol Buffer schema.

This repository contains a [protoc](https://github.com/google/protobuf) plugin that generates TypeScript declarations
(`.d.ts` files) that match the JavaScript output of `protoc --js_out=import_style=commonjs,binary`.

This plugin is tested and written using TypeScript 2.7.

This repository is forked from https://github.com/improbable-eng/ts-protoc-gen/

## Installation / Usage

As a prerequisite, download or install `protoc` (the protocol buffer compiler) for your platform from the [github releases page](https://github.com/google/protobuf/releases) or via a package manager (ie: [brew](http://brewformulas.org/Protobuf), [apt](https://www.ubuntuupdates.org/pm/protobuf-compiler)).

For the latest stable version of the ts-protoc-gen plugin:

```bash
npm install protoc-ts-type-gen
```

Run protoc and reference this library as a plugin:

```bash
protoc \
    --plugin="protoc-gen-ts=node_modules/" \
    --ts_out="${OUT_DIR}" \
    com/igtimi/*.proto \
    com/yachtbot/*.proto
```

## Gotchas

By default the google-protobuf library will use the JavaScript number type to store 64bit float and integer values; this can lead to overflow problems as you exceed JavaScript's `Number.MAX_VALUE`. To work around this, you should consider using the `jstype` annotation on any 64bit fields, ie:

```proto
message Example {
  uint64 bigInt = 1 [jstype = JS_STRING];
}
```
