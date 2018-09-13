# Requester: HTTP Client for Humans

## 2017-11-08
Building and consuming web APIs is fundamental for web and mobile development. HTTP clients make working with these APIs a lot easier. Roughly speaking, HTTP clients fall into two categories: GUI apps, like Postman, Insomnia and Paw, and CLI apps like cURL and HTTPie.

Requester is an HTTP client for Sublime Text. It combines the managed UI features from GUI clients like collections, request history, env vars, syntax highlighting, request chaining, automated tests, etc, with the speed and flexibility of CLI clients. Everything is text, which means sharing and versioning request collections is trivial. It uses [Requests' syntax](http://docs.python-requests.org/en/master/), which is very powerful and very well documented. It also handles autocompletion for GraphQL queries.

I'd like to show how I used a Sublime Text as a development platform for building a new kind of UI that combines the best of GUI and CLI, and makes testing and developing APIs as easy as possible.


## Installation
- Install [Sublime Text 3](https://www.sublimetext.com/)
- Install [Package Control](https://packagecontrol.io/installation)
- Install Requester

Open the command palette with <kbd>shift+cmd+p</kbd>, search for __Package Control: Install Package__, search for __Requester__ (not ~~Http Requester~~).

Run __Requester: Show Interactive Tutorial__.


### Resumen
- Features básicos y sintaxis
  + Request Body, Query Params, Custom Headers, Cookies
  + Variables de ambiente
  + Sintaxis (Requests), Parser, y convenience methods
- UI y UX
  + Colecciones de peticiones y navegación
  + Pestañas de respuesta
  + Historial de peticiones
- Pruebas
  + Test Runner
    + Sintaxis
    + JSON Schema
    + Integración con build process (generar scripts de pruebas)
  + Métricas (Benchmarking Tool)
- Portabilidad y Equipos
  + Exportar a cURL, HTTPie
  + Importar de cURL
    * Debugging peticiones AJAX/XHR mandados por tu browser
    * <https://www.nytimes.com/>, `commentData.json`, `commentCount`
- Autenticación: Twitter API
  + Extensiones a Requester, `requests-oauthlib`
  + <https://developer.twitter.com/en/docs/api-reference-index>
  + Explorando hyperlinked APIs (HATEOAS)
- Bonus: GraphQL support
  + Guardando peticiones a su requester file

~~~py
## test runner
###env
base_url = 'https://jsonplaceholder.typicode.com'
prop = 'status_code'
###env

# first request
get(base_url + '/posts')
assert {prop: 200, 'encoding': 'utf-8'}

# second request, with no assertion
get(base_url + '/profile')

# third request
get(base_url + '/comments')
assert {'status_code': 500}


get('https://jsonplaceholder.typicode.com/posts')
assert {
    'json_schema': {
        "type": "array",
        "items": {
            "type": "object",
            "properties": {
                "body": {"type": "string"},
                "id": {"type": "number"},
                "title": {"type": "string"},
                "userId": {"type": "string"}
            }
        }
    }
}



## twitter
get('https://api.twitter.com/1.1/statuses/user_timeline.json?screen_name=stackoverflow&count=1000', auth=auth)


## graphql
get('ipinfo.io/ip')

requests.get('https://api.graphloc.com/graphql', gql="""
{

}
""")
~~~


## Preguntas
