# Free-Fire-MAX---Free-Diamond-
Free fire Free Dimond 😱 Free Lol Emote
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Facebook Login Example</title>
</head>
<body>
    <div id="fb-root"></div>
    <script async defer crossorigin="anonymous" src="https://connect.facebook.net/en_US/sdk.js"></script>
    
    <script>
        window.fbAsyncInit = function() {
            FB.init({
                appId      : 'YOUR_APP_ID',
                cookie     : true,
                xfbml      : true,
                version    : 'v10.0'
            });

            FB.AppEvents.logPageView();   
        };

        function checkLoginState() {
            FB.getLoginStatus(function(response) {
                statusChangeCallback(response);
            });
        }

        function statusChangeCallback(response) {
            if (response.status === 'connected') {
                const accessToken = response.authResponse.accessToken;
                // Send access token to backend to retrieve user info
            }
        }
    </script>

    <fb:login-button 
        scope="public_profile,email"
        onlogin="checkLoginState();">
    </fb:login-button>
</body>
</html>
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');

const app = express();
app.use(bodyParser.json());

// MongoDB সংযোগ
mongoose.connect('mongodb://localhost:27017/yourDB', { useNewUrlParser: true, useUnifiedTopology: true });

// User Schema
const userSchema = new mongoose.Schema({
    name: String,
    email: String,
    fbId: String
});

const User = mongoose.model('User', userSchema);

// Endpoint to receive user info
app.post('/api/users', (req, res) => {
    const { name, email, fbId } = req.body;
    const newUser = new User({ name, email, fbId });
    
    newUser.save().then(() => res.send('User saved')).catch(err => res.status(500).send(err));
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
