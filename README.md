# TCL Requests

Simple wrapper for tcl `http::geturl`


https://www.tcl.tk/man/tcl8.6.13/TclCmd/http.htm

## Usage

```tcl

package require requests


# import all commands, ex. get,post,etc..
namespace import ::requests::all::* 

# or import only requests new-request url-encode quote-string config Request Response
namespace import ::requests::* 

set resp [get http://myapp.com/json]

# convert to tcl dict
puts [$resp json]

set resp [post http://myapp.com/json -json {{"x": 1, "y": 2}}]

puts [$resp status]

set req [Request new] ;# or [Request new]
$req url http://myapp.com
set resp [get -req $req]

get http://app.com -- -header {x y} 

# use http with cmd
requests get http://app.com -- -header {x y} 


#use request



```

Use `--` to pass values to `http::geturl`


### Doc

* `::requests::get {url {headers keyvallist} args}` 
* `::requests::options {url {headers keyvallist} args}`
* `::requests::post {url payload {headers keyvallist} args}`
* `::requests::put {url payload {headers keyvallist} args}`
* `::requests::patch {url payload {headers keyvallist} args}`
* `::requests::delete {url payload {headers keyvallist} args}`
* `::requests::request {args}`
* `::requests::new-request` Create new `::requests::Request`
* `::requests::url-encode {keyvallist}`  wrapper for `::http::formatQuery`
* `::requests::quote-string {string}`  wrapper for `::http::quoteString`
* `::requests::config {args}` wrapper for `::http::config`

Requests cmd

* `::requests::requests do {args}` same of `request`
* `::requests::requests get {url {headers keyvallist} args}` 
* `::requests::requests options {url {headers keyvallist} args}`
* `::requests::requests post {url payload {headers keyvallist} args}`
* `::requests::requests put {url payload {headers keyvallist} args}`
* `::requests::requests patch {url payload {headers keyvallist} args}`
* `::requests::requests delete {url payload {headers keyvallist} args}`

Gereral args

* `-debug` default false
* `-url` url
* `-progress` callback request progress
* `-method` http method
* `-body` body 
* `-json` body as json, set content-type to application/json
* `-timeout` timeout milliseconds
* `-content-type` set content-type
* `-header` keyval `{k v}`
* `-headers` keyvallist `{{k v} {x y}}`
* `-req` accepts a `::requests::Request`
* `--` send args directly to `::http::geturl`


### ::requests::Request

Methods:

* `prop {args}` get or ser prop
* `url {string}` set url
* `body {string}` set body
* `method {string}` set verb method
* `json {json data}` set body with json data
* `header {keyval}` set header
* `headers {keyvallist}` set headers
* `content-type {string}` set content-type

The `::requests::Request new` accept all args of session `Request args`. You can use `::requests::new-request` too.

### ::requests::Response

* `prop {string}` get prop by name
* `encoding` get encoding
* `status` get http status (eg. 200, 404)
* `status-text` ok,eof,error,timeout,reset
* `status-code` get http status (eg. HTTP/1.1 200)
* `text` get bodys tring
* `body` get bodys tring
* `length` get body size
* `content-type` get content-type
* `url` get url
* `headers` get headers keyvallist
* `json` get body as json (dict)
* `header {string}` get header by name