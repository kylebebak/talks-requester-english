# Requester: HTTP Client for Humans

## 2017-11-08
Building/consuming web APIs is fundamental to web and mobile development. HTTP clients make working with web APIs a lot easier. Roughly speaking, HTTP clients fall into two categories: GUI apps, like Postman, Insomnia and Paw, and CLI apps like cURL and HTTPie.

Requester is an HTTP client for Sublime Text. It combines the "managed UI" features from GUI clients like collections, request history, env vars, syntax highlighting, request chaining, etc, with the speed of CLI clients. Everything is text, so sharing and versioning request collections is trivial. It uses [Requests' syntax](http://docs.python-requests.org/en/master/), which is very nice and very well documented.

I'd like to show how you can use Sublime Text as a platform for building a new kind of UI that combines the best of GUI and CLI.


## Installation
- Get [Sublime Text 3](https://www.sublimetext.com/)
- Install [Package Control](https://packagecontrol.io/installation)
- Install __Requester__ (not ~~Http Requester~~)

Run __Requester: Show Interactive Tutorial__.


## Python Stuff
- Parser
  + Takes a string, such as a selection from a view, returns a list of all calls to `requests` in the string
- Eval and Exec
  + `exec` used to build an env dict from a string, which is sort of how `import` populates a variables dict from a Python module
  + the `exec`ed string is a concatenation of env block and env file
  + `eval` used to parse args passed to `requests.<http_method>`
  + this lets Requester modify, remove or add to args and kwargs before actually calling `requests`
- Requests run in parallel in a thread pool
- Syntax is [Requests' syntax](http://docs.python-requests.org/en/master/)


## UI and UX
- Request collections and navigation (fuzzy search!)
- Env vars
- Response tabs
- Request history (`ctrl+h`)

~~~py
###env
base_url = 'https://jsonplaceholder.typicode.com'
###env

# first request
get(base_url + '/comments')
assert {'status_code': 200, 'encoding': 'utf-8'}

# second request, with no assertion
post(base_url + '/posts')
~~~


## Portability and teams
-  It's text!
  + git, GitHub, etc
    * env vars can go in a git-ignored file
-  Export to cURL, HTTPie
-  Import from cURL
  + Debugging AJAX/XHR requests sent by your browser


## Bonuses  
- GraphQL support
- Test runner
- Benchmarking tool (like __ab__)
  + Test Runner


~~~py
get('ipinfo.io/ip')

requests.get('https://api.graphloc.com/graphql', gql="""
{
  getLocation(ip: "198.151.206.196") {
  }
}
""")
~~~


## Takeaways
- `eval` and `exec` have some cool uses
- Requests is a sweet library
- Build on top of existing libraries, as long as they're stable, and especially if they're well documented
- Using a text editor to build and run certain kinds of allows a new kind of UI
  + There ought to more UIs that mix of GUI and text
  
