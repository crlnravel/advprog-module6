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
