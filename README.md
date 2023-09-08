# Fake Headers for rust
This is create from python fake_headers

## Usage
```rust
fn main() {
    
    let random_browser = random_browser();
    let random_os = random_os();

    let headers = Headers {
        browser: random_browser,
        os: random_os,
        headers: false,
    };

    let generated_headers = headers.generate();

    println!("{:?}", generated_headers);
}
```