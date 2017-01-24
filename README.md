Splunk HEC Golang Library
=========================

[![Build Status](https://travis-ci.org/fuyufjh/splunk-hec-go.svg?branch=master)](https://travis-ci.org/fuyufjh/splunk-hec-go)

## Build

You need install [glide](https://github.com/Masterminds/glide) before build. To install all dependencies,

```bash
glide install

go build -o build/example ./example/main.go
```

## Example

```go
client := hec.NewCluster(
	[]string{"https://127.0.0.1:8088", "https://localhost:8088"},
	"00000000-0000-0000-0000-000000000000",
)
client.SetHTTPClient(&http.Client{Transport: &http.Transport{
	TLSClientConfig: &tls.Config{InsecureSkipVerify: true},
}})

event1 := hec.NewEvent("event one")
event1.SetTime(time.Now())
event2 := hec.NewEvent("event two")
event2.SetTime(time.Now().Add(time.Minute))

err := client.WriteBatch([]*hec.Event{event1, event2})
if err != nil {
	log.Fatal(err)
}
```

See `hec.go` for more usages.
