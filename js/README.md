# Asciidoctor Tabs

An Asciidoctor.js extension that adds a tabs block to the AsciiDoc syntax.

## Install

This package depends on the `asciidoctor` package (>= 2.2.0, < 3.0.0), but doesn't declare it as a dependency.
Therefore, you must install that package when installing this one.

```console
$ npm i asciidoctor @asciidoctor/tabs
```

## Syntax

```asciidoc
[tabs]
====
Tab A:: Contents of tab A.

Tab B::
+
Contents of tab B.

Tab C::
+
--
Contents of tab C.

Contains more than one block.
--
====
```

You may choose to extend the block delimiter length from the typical 4 characters to 6 in order to avoid conflicts with any example blocks inside the tab block (or just as a matter of style).

```asciidoc
[tabs]
======
Tab A::
+
====
Example block in Tab A.
====

Tab B:: Just text.
======
```

## Usage

### CLI

```console
$ npx asciidoctor -r @asciidoctor/tabs document-with-tabs.adoc
```

The `asciidoctor` command automatically registers the tabs extension when the package is required.

### API

There are two ways to use the extension with the Asciidoctor.js API.
In either case, you must require the Asciidoctor.js module (`asciidoctor`) before requiring this one.

You can call the exported `register` method with no arguments to register the extension as a global extension.

```js
const Asciidoctor = require('asciidoctor')()

require('@asciidoctor/tabs').register()

Asciidoctor.convertFile('document-with-tabs.adoc', { safe: 'safe' })
```

Or you can pass a registry instance to the `register` method to register the extension with a scoped registry.

```js
const Asciidoctor = require('asciidoctor')()

const registry = Asciidoctor.Extensions.create()
require('@asciidoctor/tabs').register(registry)

Asciidoctor.convertFile('document-with-tabs.adoc', { extension_registry: registry, safe: 'safe' })
```

You can also require `@asciidoctor/tabs/extensions` to access the `Extensions` class.
Attached to that object are the `Block`, `Docinfo.Style`, and `Docinfo.Behavior` extension classes.
You can use these classes to register a bespoke tabs extension.

## Copyright and License

Copyright (C) 2018-present Dan Allen (OpenDevise Inc.) and the individual contributors to this project.
Use of this software is granted under the terms of the MIT License.
