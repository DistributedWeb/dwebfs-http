# DWebFs Http

Serve a [dwebfs](https://github.com/distributedweb/dwebfs) archive over HTTP. For an example of use, see [dweb.haus](https://github.com/juliangruber/dweb.haus).

[![Travis](https://api.travis-ci.org/joehand/dwebfs-http.svg)](https://travis-ci.org/joehand/dwebfs-http)

## Usage

DWebFs-http returns a function to call when you receive a http request:

```js
var server = http.createServer().listen(8000)
server.on('request', hyperdriveHttp(archive))
```

Supports manifest options in `dweb.json`:

* `web_root` - change directory to serve on index
* `fallback_page` - fallback for 404 errors

### Setup

To use dwebfs-http you will need to:

* Create your own http server
* Setup your dwebfs archive
* For remote archives, connect to the swarm

## API

DWebFs works with many archives/feeds or a single archive.

#### Options

- `exposeHeaders` - If set to `true`, dwebfs-http will add custom `DWebFs-` HTTP headers to directory listing requests (default: `false`):
  ```http
  DWebFs-Key: de2a51bbaf8a5545eff82c999f15e1fd29637b3f16db94633cb6e2e0c324f833
  DWebFs-Version: 4
  ```
- `live` - If set to `true` will reload a directly listing if the archive receives updates.
- `footer` - Add a footer to your HTML page. Automatically adds archive version number to footer.

### URL Format

DWebFs-http responds to any URL with a specific format. If the URL does cannot be parsed, it will return a 404.

* Get archive listing: `http://archive-example.com/`
* Get file from archive: `http://archive-example.com/filename.pdf`

If a directory in the archive contains an `index.html` page that file is returned instead of the directory listing. If you'd like to view files use a query string:

* View files: `http://archive-example.com/?viewSource=true`


## CLI

There is also a CLI that can be used for demo + testing. Pass it a dweb link or a path to an existing dweb folder:

```
node cli.js <dweb-key>
node cli.js /path/do/existing/dweb
```
