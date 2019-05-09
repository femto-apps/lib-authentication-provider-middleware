# lib-authentication-provider-middleware
This is authentication middleware for an authentication provider. 

### Architecture

#### Example Usage

```javascript
const Auth = require('@femto-apps/authentication-provider-middleware')

const local = Auth.register({
    serialise: () => {}, // serialise a user on login
    deserialise: () => {}, // deserialise a user on page load
    authenticate: () => {}, // authenticate a user when logging on
    logout: () => {} // (optional?) unauthenticate a user when logging out
})

// Required to handle deserialisation of session information
app.use(Auth.initialise())

// Only required if you want persistant sessions, not needed
// for e.g. APIs
app.use(Auth.session())

// An endpoint to authenticate users
app.get('/login',
    auth.authenticate(local)
        .then(user => {
            console.log(`Logged in as ${user}`)
        })
)

```