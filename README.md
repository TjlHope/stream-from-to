stream-from-to [![Build Status](https://travis-ci.org/alanshaw/stream-from-to.png)](https://travis-ci.org/alanshaw/markdown-pdf) [![Dependency Status](https://david-dm.org/alanshaw/stream-from-to.png)](https://david-dm.org/alanshaw/stream-from-to)
===
Utility for piping to/from a stream from a variety of sources to a variety of destinations.

Pass stream-from-to a [through](https://npmjs.org/package/through) stream and it'll give you back an object that simplifies the constructon of source and destination streams for piping to/from the thorugh stream.

Usage
---

```javascript
var streamft = require("stream-from-to")
  , through = require("through")

// Through stream that converts markdown to HTML
var mdToHtml = through()

streamft(mdToHtml).from.path("/path/to/doc.md").to.path("/path/to/doc.html", function (er) {
    if (er) return console.error(er)
    // Done!
})
```

API
---

### from.path(path, opts)

Create a readable stream from `path` and pipe to the through stream. `path` can be a single path or array of paths.

### from.string(string)

Create a readable stream from `string` and pipe to the through stream. `string` can be a single string or array of strings.

### concat.from.path(paths, opts)

Create and concatinate readable streams from `paths` and pipe to the through stream.

### concat.from.string(strings, opts)

Create and concatinate readable streams from `strings` and pipe to the through stream.

### to.path(path, cb)

Create a writeable stream to `path` and pipe output from the through stream to it. `path` can be a single path, or array of output paths if you specified an array of inputs. The callback function `cb` will be invoked when data has finished being written.

### to.buffer(opts, cb)

Create a [concat-stream](https://npmjs.org/package/concat-stream) and pipe output from the through stream to it. The callback function `cb` will be invoked when the buffer has been created.

### to.string(opts, cb)

Create a [concat-stream](https://npmjs.org/package/concat-stream) and pipe output from the through stream to it. The callback function `cb` will be invoked when the string has been created.