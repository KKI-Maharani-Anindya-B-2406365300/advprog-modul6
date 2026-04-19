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

# Commit 2 Reflection Notes

In this step, the server was improved so it not only reads the browser request, but also sends back a valid HTTP response containing an HTML page. As a result, the browser is now able to render content instead of showing an error.
Inside the updated `handle_connection`, the request is still read line by line using `BufReader`. After that, the server loads the HTML file using `fs::read_to_string` and prepares a response that includes a status line, headers, and the HTML body. The `Content-Length` header is used to inform the browser about the size of the response body.
The response is then converted into bytes and sent through the `TcpStream`, allowing the browser to display the page correctly.
This step shows that a web server must return a properly formatted HTTP response, not just receive requests, in order for the browser to render content successfully.

![Commit 2 screen capture](/assets/images/commit2.png)

