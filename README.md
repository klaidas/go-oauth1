# Go-OAuth1.0
Golang package/ implementation example of OAuth1.0 Authentication Header/ Signature calculation (Twitter etc..)

To quickly import the package into your project:
> ```
>  go get github.com/ku00015/go-oauth1
> ```

Example usage: 
```Go
package main

import (
	"fmt"
	oauth1 "go-oauth1"
	"net/http"
)

func main() {
	method := http.MethodPost
	url := "https://api.twitter.com/1.1/statuses/update.json?include_entities=true"
	
	auth := oauth1.OAuth1{
		ConsumerKey: "xvz1evFS4wEEPTGEFPHBog",
		ConsumerSecret: "kAcSOqF21Fu85e7zjz7ZN2U4ZRhfV3WpwPAoE3Z7kBw",
		AccessToken: "370773112-GmHxMAgYyLbNEtIKZeRNFsMKPR9EyMZeS9weJAEb",
		AccessSecret: "LswwdoUaIvS8ltyTt5jkRh4J50vUPVVHtR2YPi5kE",
	}

	authHeader := auth.BuildOAuth1Header(method, url, map[string]string {
		"include_entities": "true",
		"status": "Hello Ladies + Gentlemen, a signed OAuth request!",
	})
	
	req, _ := http.NewRequest(method, url, nil)
	req.Header.Set("Authorization", authHeader)
	
	if res, err := http.DefaultClient.Do(req); err == nil {
		fmt.Println(res.StatusCode)
	}
}
```
