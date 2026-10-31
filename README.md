# Era HTTP (`github.com/era-lang-official/http`)

Fast HTTP 1.1 request/response parser, wire formatter, router, and client library for Era.

## Installation

Add to your `era.mod`:
```
require (
    github.com/era-lang-official/http v1.0.0
)
```

## Usage

```era
import "github.com/era-lang-official/http";

fn main() {
    // 1. Parsing wire request
    let raw = "GET /users?status=active HTTP/1.1\r\nHost: localhost\r\n\r\n";
    let req = parse_request(raw).unwrap();
    println(req.method); // "GET"
    println(req.query_param("status".to_string()).unwrap()); // "active"

    // 2. Generating wire response
    let resp = Response::json("{\"status\": \"ok\"}")
        .with_header("Server".to_string(), "Era-Native".to_string());
    println(resp.to_wire());

    // 3. Client fetch
    let client_resp = get(":8080".to_string(), "/api/status".to_string());
}
```

