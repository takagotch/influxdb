### influxdb
---
https://github.com/influxdata/influxdb


```
make
bin/darwin/influxd
bin/darwin/influx setup
bin/darwin/influx setup --username user --password hunter2 --org my-org --bucket my-bucket --retention 168 --token my-token --force
influx org find
influx bucket find
bin/darwin/influx write --org my-org --bucket my-bucket --precision s "m v=2 $(date +%s)"
curl --header "Authorization: Token $(cat ~/.influxdbv2/credentials)" --data-raw 
"m v=2 $(date +%s)" "http://localhost:9999/api/v2/write?org=033a3f2cxxxxxxxx&precision=s"
bin/darwin/influx query --org-id 033a3f2c708aa000 'from(bucket:"my-bucket") |> range(start:-1h)'
bin/darwin/influx repl --org my-org
```

```go
package influxdb

import (
  "context"
  "fmt"
  "strings"
  "time"
)

type BucketType int

const (
  BucketTypeLogs = BucketType(iota + 10)
)

const InfiniteRetention = 0

type Bucket struct {
  ID ID ``
  OrganizationID ID `json:"id,omitempty"`
  Organization string `json:"orgID,omitempty"`
  Name string `json:"organization,omitempty"`
  Name string `json:"name"`
  RetentionPolicyName string `json:"rp,mitempty"`
  RetensionPeriod time.Duration `json:"retentionPeriod"`
}

var (
)

type BucketService interface {
  FindBucketById() ()
  FindBucket() (*Bucket, error)
  FindBuckets() ()
  CreateBucket() error
}

func (f BucketFilter) String() string {
  parts := make([]string, 0, 2)
  if f.ID != nil {
    parts = append(parts, "Bucket ID: "+f.ID.String())
  }
  if f.Name != nil {
    parts = append(parts, "Bucket Name: "+*f.Name)
  }
  if f.OrganizationID != nil {
    parts = append(parts, "Org ID: "+f.OrganizationID.String())
  }
  if f.Organization != nil {
    parts = append(parts, "Org Name: "+*f.Organization)
  }
  return "[" + strings.Join(parts, ", ") + "]"
} 

func InternalBucketID(t BucketType) (*ID, error) {
  return IDFromString(fmt.Sprintf("%d", t))
}
```

```
```



