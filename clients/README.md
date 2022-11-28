# Instructions for participants

## Slicing

To calculate the bill, you need to consider the tax of the country from which the order came from and the reduction.


## Coding
1. To be able to play, you will need to start an HTTP server in your local machine. Many servers are already available in this directory, you only need to clone this repository and pick will. Otherwise, you can create your own HTTP server. You **don't have to install any HTTP server** like Tomcat, Apache, ngnix, the clients are themserves HTTP servers.
2. The facilitator will start a central server which will send requests to each participant's server. Since the facilitator communicates the URL for the server dashboard, go there and register your local server with your local IP address and the port under your HTTP server is listening on (URL example: http://\<you IP address\>:\<port for your local HTTP server\>/)
3. The central server will start sending orders to your local client like this:

    ```
    POST /order HTTP/1.1
    {
        "prices": [65.6,27.26,32.68],
        "quantities": [6,8,10],
        "country": "IE",
        "reduction":"STANDARD"
    }
    ```

4. Your job is to calculate the amount of the received orders and answer with a JSON object bill, i.e.: `{ "total": 1000.0 }` (the server checks responses using two decimal digits of precision, so, i. e., 10.1234 and 10.12 are equal).
5. Your score will be shown in the dashboard
6. The server will send you feedback based on what you have responded. So check if your local HTTP server already handles POST /feedback and, *if not, implement it, otherwise you will not be able to figure out what is going on with your responses*. Here is an example of a feedback the central server can send to you:

    ```
    POST /feedback HTTP/1.1
    {
        "type": "ERROR",
        "content": "The field \"total\" in the response is missing."
    }
    ```

## Game rules

If your answer match the expected bill, then congratulations: you earned the amount of the bill!

If you answer a total that does not match the expected bill, you will be charged with 50% of the amount of the right bill.

Your answer will be ignored if one of these conditions are met:
- your server is unreachable
- you responded with HTTP code 404
