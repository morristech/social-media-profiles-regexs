# Regular Expressions to Match Social Media Profiles
This repository lists regular expressions to match and extract URLs of social media profiles. For simplicity URLs have to be filtered beforehand, i.e. the regular expression has to be executed on a single URL. To do this, you could use a regular expression matching valid URLs or use a specific library, for example JSOUP for Java.

## Twitter
    .*twitter\.com\/[A-z 0-9 _]+\/?
Allowed for usernames are alphanumeric characters and underscores. 

### Verification
Send request to page and check for username in answer (rate limit?)

## Github
    http(s)?:\/\/(www\.)?github\.com/[A-z 0-9 _ -]+
Exclude subdomains as these redirect to github pages sometimes.

    http(s)?:\/\/([A-z 0-9 - _]+)\.github\.(com|io)
Regex for pages like someuser.github.io.

### Verification
Use https://api.github.com/users/{user_login} (60 requests/hour unauthenticated)

## Linkedin
    http(s)?:\/\/([\w]+\.)?linkedin\.com\/in\/(A-z 0-9 _ -)\/?
Public URLs. (TODO: there are also linkedin.com/userxy profiles.

    http(s)?:\/\/([\w]+\.)?linkedin\.com\/pub\/[A-z 0-9 _ -]+(\/[A-z 0-9]+){3}\/?
Matches public profiles that need three keys(?) after the actual name.

### Verification
Check page for profile specific html (rate limit?)

## Facebook
    http(s)?:\/\/(www\.)?facebook\.com\/(A-z 0-9 _ - \.)\/?

Since Facebook redirects these URLs to all kinds of objects (user, pages, events, and so on), you have to verifiy that it's actually a user. See https://developers.facebook.com/docs/graph-api/reference/profile

### Verification
#### API
http://graph.facebook.com/v2.3/{{username}} gives the following result, if the user exists:

    {
        "error": {
        "message": "(#803) Cannot query users by their username ({{specified username}})",
        "type": "OAuthException",
        "code": 803
        }
    }

#### GET request
A GET request on an existing (but hidden) user with a randomly added point seems to redirect to the real username.

## TODO
* Verification checks (ideas first and maybe scripts at a later point)

I plan on adding the following social media profiles at the moment.
* facebook
* xing
* instagram
* google plus
* pinterest
* vimeo
* skype
* wordpress
* medium
* youtube
* stackoverflow
* bitbucket
 
Feel free to add any social media site you would like to find here!
