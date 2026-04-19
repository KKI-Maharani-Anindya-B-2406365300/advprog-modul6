# Commit 1 Reflection Notes

In this step, the program was updated to handle browser connections using the `handle_connection` function. Previously, the server only accepted TCP connections and printed a simple message. Now, it is able to read and display the HTTP request sent by the browser.
Flow inside `handle_connection`:
1. `TcpStream` receives the connection from the browser
2. `BufReader` wraps the stream to make the request easier to read line by line
3. `.lines()` reads each line of the HTTP request
4. `.map(|result| result.unwrap())` takes the actual text from each line
5. `.take_while(|line| !line.is_empty())` stops reading when it reaches an empty line, which marks the end of the HTTP headers
6. `.collect()` stores all request lines into a vector
7. `println!` displays the request in a readable format
This step shows that browser requests are sent as structured HTTP text, and the server must correctly read and interpret them before generating a response