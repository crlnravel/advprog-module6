# Tutorial Module 6 AdvProg - Concurrency

Name: Carleano Ravelza Wongso
NPM: 2306213022

## Commit 1 Reflection Notes

The function `handle_connection` processes an incoming TCP connection from a client.
This function takes a TcpStream as a parameter, representing the connection between the server and the client.

```rust
let buf_reader = BufReader::new(&mut stream);
```

The line above is used to improve efficiency by reading the incoming data in chunks, rather than one byte at a time.
This is done by wrapping the TcpStream in a BufReader.

```rust
let http_request: Vec<_> = buf_reader
    .lines()
    .map(|result| result.unwrap())
    .take_while(|line| !line.is_empty())
    .collect();
```

The lines above are used to read the incoming data line by line.
The `take_while` method is used to stop reading when an empty line is encountered, which indicates the end of the request.
Then, it collects the lines into a vector of strings.

After all of the parsing done, it prints the received request to the console.

## Commit 2 Reflection Notes

### Screenshot in Browser

![Commit 2 screen capture](/assets/images/commit2.png)

## Commit 3 Reflection Notes

The refactored code improves clarity, maintainability, and scalability by eliminating duplication. Instead of repeating response logic inside if-else, it assigns status_line and filename first, then processes the response once. This makes it easier to extend (e.g., adding more endpoints) and improves readability by separating response selection from response formatting and sending.

### Screenshot in Browser

![Commit 3 screen capture](/assets/images/commit3.png)

## Commit 4 Reflection Notes

When we open 127.0.0.1/sleep, the server pauses for 10 seconds before responding because of this line:

```rust
thread::sleep(Duration::from_secs(10));
```

This means the entire thread handling the request is blocked for 10 seconds. Now, if we try to access 127.0.0.1/ in another browser window before the sleep request is done, it will also be delayed. This happens because Rust’s TcpListener::incoming() processes connections sequentially in a single thread.

## Commit 5 Reflection Notes

This commit upgrades the server to a multi-threaded approach, allowing it to handle up to four requests concurrently. Previously, a request to /sleep blocked all other clients, causing delays. With this change, slow requests no longer affect others, significantly improving response times and scalability. It also reinforces key concepts in thread pool management and thread safety in Rust.
