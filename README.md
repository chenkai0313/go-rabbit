# go-rabbit
rabbit 方法封装

### 使用
```
go get github.com/chenkai0313/go-rabbmit
```

#### 使用事例
```
package main

import (
	"encoding/json"
	"fmt"
	 "rabbmit"
)

func main() {
	var client rabbit.MsgClient
	var err error
	err = client.ConnectToBroker("addr")
	if err != nil {
		panic("rabbit connect error")
	}
	defer client.Close()
	type Queue struct {
		ProductId int32 `json:"product_id"`
	}
	queue := Queue{ProductId: 1}
	queueJson, _ := json.Marshal(queue)
	exchangeName := "test"
	exchangeType := "fanout"
	queueName := "test"

	err = client.Publish(queueJson, exchangeName, exchangeType, queueName)
	if err != nil {
		fmt.Println("err", err)
	}
}


```
