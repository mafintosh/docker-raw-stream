# docker-raw-stream

Decode/encode a docker raw stream

```
npm install docker-raw-stream
```

## Usage

docker raw streams multiplexes stdout/stderr to a single stream

``` js
var raw = require('docker-raw-stream')
var request = require('request')

var decode = raw.decode()

// forward the output to stdio
decode.stdout.pipe(process.stdout)
decode.stderr.pipe(process.stderr)

request.post('http://docker-host:2375/containers/f7f65a63a595/attach?stderr=1&stdout=1&stream=1').pipe(decode)
```

You can also use it encode a stream to the docker raw stream format

``` js
var encode = raw.encode()

// forward stdin to the stdout channel
process.stdin.pipe(encode.stdout)

encode.pipe(someWritableStream)
```

## License

MIT