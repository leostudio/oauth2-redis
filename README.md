# Redis Storage for [OAuth 2.0](https://github.com/go-oauth2/oauth2)

forked from [go-oauth2/redis](https://github.com/go-oauth2/redis), supported get by user id and remove by user id.

## Install

``` bash
$ go get -u -v github.com/Ankr-network/oauth2-redis
```

## Usage

``` go
package main

import (
	"github.com/go-redis/redis"
	oredis "github.com/Ankr-network/oauth2-redis"
	"gopkg.in/oauth2.v3/manage"
)

func main() {
	manager := manage.NewDefaultManager()
	
	tokenStore := oredis.NewRedisStore(&redis.Options{
		Addr: "127.0.0.1:6379",
		DB: 15,
	})
	// use redis token store
	manager.MapTokenStorage(tokenStore)

	// get token by user id
	// t, _ := tokenStore.GetByUID("test") // get token info by user id
	// _ := tokenStore.RemoveByUID("test") // remove access token and refresh token by uid

	// use redis cluster store
	// manager.MapTokenStorage(oredis.NewRedisClusterStore(&redis.ClusterOptions{
	// 	Addrs: []string{"127.0.0.1:6379"},
	// 	DB: 15,
	// }))
}
```