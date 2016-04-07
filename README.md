# httptor
Use tor with http.DefaultClient

Install with:

```
go get github.com/yansal/httptor
```

Start tor. On OS X it is something like:
```
brew up
brew install tor
tor
```

Add a blank import to the program:

```
import _ "github.com/yansal/httptor"
```

Check that it works with:

```
package main

import (
	"io"
	"log"
	"net/http"
	"os"

	_ "github.com/yansal/httptor"
)

func main() {
	resp, err := http.Get("https://check.torproject.org/api/ip")
	if err != nil {
		log.Fatal(err)
	}
	defer resp.Body.Close()
	if _, err := io.Copy(os.Stdout, resp.Body); err != nil {
		log.Fatal(err)
	}
}
```
