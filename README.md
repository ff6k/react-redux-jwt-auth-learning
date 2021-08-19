Note: This example is very out-of-date. It might point you in the right direction, but I plan to re-write it from scratch. I won't be accepting any PRs in the meantime. Sorry about that!

### Goal

This project is an learning project to show possibility authentication flow using [react](https://github.com/facebook/react), [redux](https://github.com/rackt/redux), [react-router](https://github.com/rackt/react-router), [redux-router](https://github.com/rackt/redux-router), and [JSON web tokens (JWT)](http://jwt.io/). It is based on the implementation of a [higher-order component](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750)
to wrap protected views and perform authentication logic prior to rendering them.

**Note:** The focus here is on the client-side flow. The server included in this example is for demonstration purposes only.
It contains some hard-coded API endpoints and is obviously not intended for any
kind of production environment.

---

### Running the Example Locally
````
1. git clone https://github.com/coolerwind/react-redux-jwt-auth-learning.git
2. npm install
3. export NODE_ENV=development
4. node server.js
````
Then visit `localhost:3000` in your browser.

---

### General Flow

The overall flow goes something like this:

1. The log in form dispatches an action creator which triggers a POST to the server
2. The server validates login credentials and returns a valid JWT or 401 Unauthorized response as needed
3. The original action creator parses the server response and dispatches success or failure actions accordingly
4. Success actions trigger an update of the auth state, passing along the token and any decoded data from the JWT payload
5. A higher-order authentication component receives the new auth state as props
6. If authentication was successful, the higher-order component renders its child component and passes the auth props down to it
7. Before mounting, the child fetches data from the server using the token it received from its parent wrapper