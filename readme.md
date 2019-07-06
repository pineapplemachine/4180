# 4180

[![MIT License][license-image]][license] [![Build Status][travis-image]][travis-url] [![NPM version][npm-version-image]][npm-url]

4180 is a minimal, robust, zero-dependency JavaScript package for writing and
parsing CSV files, pursuant to [RFC 4180](https://tools.ietf.org/html/rfc4180),
written in [TypeScript](https://www.typescriptlang.org/).

4180 natively supports parsing and writing string data either eagerly or lazily,
as well as via [NodeJS streams](https://nodejs.org/api/stream.html#stream_readable_pipe_destination_options).

[license-image]: http://img.shields.io/badge/license-MIT-blue.svg
[license]: https://github.com/pineapplemachine/strtime-js/blob/master/LICENSE

[travis-url]: https://travis-ci.org/pineapplemachine/4180
[travis-image]: https://travis-ci.org/pineapplemachine/4180.svg?branch=master

[npm-url]: https://www.npmjs.com/package/4180
[npm-version-image]: https://badge.fury.io/js/4180.svg

## API Documentation

You can read the full API documentation at [**docs/index.html**](docs/index.html).

## Installation

You can install 4180 with the package manager of your choice. For example,

```
npm install 4180
```

You can then import and use the module like so:

``` js
const csv = require("4180");
```

``` js
import * as csv from "4180";
```

## Example Usage

``` js
const assert = require("assert").strict;
const fs = require("fs");

const csv = require("4180");

// My table containing very important data
const data = [
    ["Continent", "Country", "Capital"],
    ["Africa", "Egypt", "Cairo"],
    ["Africa", "Morocco", "Rabat"],
    ["Asia", "China", "Beijing"],
    ["Asia", "Japan", "Tokyo"],
    ["Australia", "Australia", "Canberra"],
    ["Europe", "Britian", "London"],
    ["Europe", "Finland", "Helsinki"],
    ["North America", "Cuba", "Havana"],
    ["North America", "United States", "Washington"],
    ["South America", "Brazil", "Brasilia"],
    ["South America", "Ecuador", "Quito"],
];

// Write my data as a CSV file
const path = __dirname + "/basic-usage.csv";
fs.writeFileSync(path, csv.write(data));

// Load the data back from my CSV file
const content = fs.readFileSync(path, "utf8");
const parsedRows = csv.parse(content).rows();

// Parsed data is equivalent to the written data
assert.deepEqual(parsedRows, data);
```

## Configuration

When parsing or writing CSV data, the library accepts an options object,
either as the second argument to **parse**, **write**, or **stream**, or
as the sole argument to the **Parser** or **Writer** constructor.

The CSV Parser class recognizes these configuration options:

``` js
const myCsvParser = new csv.Parser({
    separator: ",", // Column value separator character
    quote: "\"", // Column escaping/quoting character
});
```

The CSV Writer class recognizes these configuration options:

``` js
const myCsvWriter = new csv.Writer({
    separator: ",", // Column value separator character
    quote: "\"", // Column escaping/quoting character
    newline: "\r\n", // Row separator string, normally either "\n" or "\r\n"
    quoteAll: false, // Escape/quote all columns regardless of necessity
});
```
