EXPERIMENT 9 - USER AUTHENTICATION WEB APPLICATION

This project provides a two-card Register/Login page similar to the supplied reference image.
It uses HTML, CSS and JavaScript for the interface, with Node.js, Express, MongoDB,
bcrypt and JWT for backend authentication.

FOLDER STRUCTURE
Experiment_9_Web_Authentication/
  server.js
  package.json
  .env.example
  .gitignore
  README.txt
  public/
    index.html
    style.css
    app.js

SETUP
1. Extract the ZIP and open this folder in VS Code.
2. Open Terminal > New Terminal in this folder.
3. Run: npm install
4. Copy .env.example and name the copy .env.
5. Generate a secret using:
   node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
6. Put the generated string after JWT_SECRET= in .env.
7. Set MONGO_URI to your local MongoDB or MongoDB Atlas connection string.
8. Run: npm start
9. Open: http://localhost:3000

HOW TO USE
1. Enter an email address and password (at least 8 characters) in Register.
2. Click Register. The server validates the input, hashes the password with bcrypt,
   and saves the user in MongoDB.
3. Enter the same email and password in Login.
4. The server compares the password with the stored hash and returns a JWT.
5. The browser sends the JWT to GET /profile using the Authorization: Bearer header.
6. The protected profile appears after successful verification.
7. Click Logout to remove the token from this browser tab.

API ROUTES
POST /register  Register a user
POST /login     Log in and receive an expiring JWT
GET  /profile   Protected route requiring a valid Bearer token
POST /logout    Logout acknowledgement; client removes its token

TEST CASES
- Valid registration: 201 Created.
- Missing input / invalid email / password under 8 characters: 400 Bad Request.
- Duplicate email: 409 Conflict.
- Valid login: JWT token returned.
- Wrong email or password: 401 Unauthorized.
- Profile without token: 401 Unauthorized.
- Profile with invalid or expired token: 401 Unauthorized.
- Profile with valid token: user email is returned.

SECURITY NOTES
The JWT expires after one hour. This project uses a stateless Bearer token held in
sessionStorage for this classroom demonstration. Logout removes it from this tab,
but does not invalidate a copied token on the server. Immediate revocation requires
a server-side token revocation strategy. Use HTTPS in production, protect .env,
and never upload real secrets to GitHub.