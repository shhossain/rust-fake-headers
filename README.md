# Fake Headers for rust
This is created from python `fake_headers` module. It generates random user-agent and other headers for your http requests.

## Usage
```rust
use fake_headers::Headers;
use reqwest::header::HeaderMap;

fn main() {

    let fheaders = Headers {
        browser: 'chrome', # `chrome`, `firefox` or `opera`
        os: `win`, # `win`, `linux` or `mac`
        headers: true,
    };

    let generated_headers = fheaders.generate();
    println!("{:?}", generated_headers);

    // or get random header
    let random_header = Headers::default().generate();
    println!("{:?}", random_header);

    // add headers to reqwest
    let mut headers = reqwest::header::HeaderMap::new();
    for (key, value) in random_header {
        let header_name = reqwest::header::HeaderName::from_bytes(key.as_bytes()).unwrap();
        let header_value = reqwest::header::HeaderValue::from_str(&value).unwrap();
        headers.insert(header_name, header_value);
    }

    let client = reqwest::Client::builder()
        .default_headers(headers)
        .build()
        .unwrap();

    let res = client.get("https://httpbin.org/headers").send().unwrap();
    println!("{:?}", res.text().unwrap());
}
```