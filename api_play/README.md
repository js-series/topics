# Intro JS
## Working W/ APIs

<!-- toc -->

- [Link Structure](#link-structure)
- [Web Working](#web-working)
- [An Example API](#an-example-api)
  * [Exercise](#exercise)
- [Using Fetch](#using-fetch)
- [Promises](#promises)
  * [jQuery Request](#jquery-request)
  * [Forms](#forms)
- [Assessment](#assessment)
  * [Bonus](#bonus)
  * [SUPER BONUS?](#super-bonus)

<!-- tocstop -->

## Link Structure

![uri_description](uri_description.jpg)

## Web Working

What happens when you go to https://google.com...

* A thorough response: [Alex Explains](https://github.com/alex/what-happens-when)


At a high level you have the protocol "https" followed by the domain name "google.com" of the server and a resource path "/".

This gets turned into a dns IP lookup for `google.com`, something like `172.217.6.206`. Then after a connection is made to the server an HTTP request message is sent.

```
GET / HTTP/1.1
Host google.com

```

Google then responds back over the connection and sends it's html for the `/` resource.

```
HTTP/1.1 301 Moved Permanently
Location: https://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Tue, 28 Mar 2017 19:08:21 GMT
Expires: Thu, 27 Apr 2017 19:08:21 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 220
X-XSS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN
Alt-Svc: quic=":443"; ma=2592000; v="37,36,35"

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
```


Which tells the browser, go do this request all over again for the provided location,  `www.google.com`.

## An Example API

Let's go to the Pokemon API and give it a look.

If I want to request a Pokemon by **name**. I just add the name after `api/v2/pokemon`.

[FIND CHARMANDER](http://pokeapi.co/api/v2/pokemon/butterfree/)

```
http://pokeapi.co/api/v2/pokemon/butterfree
```

or some name

```
http://pokeapi.co/api/v2/pokemon/{name}
```


* What is the protocol of this request?
* What is the domain name?


`butterfree response`

```json
// http://pokeapi.co/api/v2/pokemon/butterfree

{
    "id": 12,
    "name": "butterfree",
    "base_experience": 178,
    "height": 11,
    "is_default": true,
    "order": 16,
    "weight": 320,
    "abilities": [{
        "is_hidden": true,
        "slot": 3,
        "ability": {
            "name": "tinted-lens",
            "url": "http://pokeapi.co/api/v2/ability/110/"
        }
    }],
    "forms": [{
        "name": "butterfree",
        "url": "http://pokeapi.co/api/v2/pokemon-form/12/"
    }],
    "game_indices": [{
        "game_index": 12,
        "version": {
            "name": "white-2",
            "url": "http://pokeapi.co/api/v2/version/22/"
        }
    }],
    "held_items": [{
        "item": {
            "name": "silver-powder",
            "url": "http://pokeapi.co/api/v2/item/199/"
        },
        "version_details": [{
            "rarity": 5,
            "version": {
                "name": "y",
                "url": "http://pokeapi.co/api/v2/version/24/"
            }
        }]
    }],
    "location_area_encounters": [{
        "location_area": {
            "name": "kanto-route-2-south-towards-viridian-city",
            "url": "http://pokeapi.co/api/v2/location-area/296/"
        },
        "version_details": [{
            "max_chance": 10,
            "encounter_details": [{
                "min_level": 7,
                "max_level": 7,
                "condition_values": [{
                    "name": "time-morning",
                    "url": "http://pokeapi.co/api/v2/encounter-condition-value/3/"
                }],
                "chance": 5,
                "method": {
                    "name": "walk",
                    "url": "http://pokeapi.co/api/v2/encounter-method/1/"
                }
            }],
            "version": {
                "name": "heartgold",
                "url": "http://pokeapi.co/api/v2/version/15/"
            }
        }]
    }],
    "moves": [{
        "move": {
            "name": "flash",
            "url": "http://pokeapi.co/api/v2/move/148/"
        },
        "version_group_details": [{
            "level_learned_at": 0,
            "version_group": {
                "name": "x-y",
                "url": "http://pokeapi.co/api/v2/version-group/15/"
            },
            "move_learn_method": {
                "name": "machine",
                "url": "http://pokeapi.co/api/v2/move-learn-method/4/"
            }
        }]
    }],
    "species": {
        "name": "butterfree",
        "url": "http://pokeapi.co/api/v2/pokemon-species/12/"
    },
    "sprites": {
        "back_female": "http://pokeapi.co/media/sprites/pokemon/back/female/12.png",
        "back_shiny_female": "http://pokeapi.co/media/sprites/pokemon/back/shiny/female/12.png",
        "back_default": "http://pokeapi.co/media/sprites/pokemon/back/12.png",
        "front_female": "http://pokeapi.co/media/sprites/pokemon/female/12.png",
        "front_shiny_female": "http://pokeapi.co/media/sprites/pokemon/shiny/female/12.png",
        "back_shiny": "http://pokeapi.co/media/sprites/pokemon/back/shiny/12.png",
        "front_default": "http://pokeapi.co/media/sprites/pokemon/12.png",
        "front_shiny": "http://pokeapi.co/media/sprites/pokemon/shiny/12.png"
    },
    "stats": [{
        "base_stat": 70,
        "effort": 0,
        "stat": {
            "name": "speed",
            "url": "http://pokeapi.co/api/v2/stat/6/"
        }
    }],
    "types": [{
        "slot": 2,
        "type": {
            "name": "flying",
            "url": "http://pokeapi.co/api/v2/type/3/"
        }
    }]
}
```

### Exercise

For each exercise record the response's movie Title and Description.

* What would the url look like to search for **Charmander**?


## Using Fetch

Fetch is the new experimental standard for easily making requests.

```javascript
fetch("http://pokeapi.co/api/v2/pokemon/butterfree")
```

Try the above and check the network tab.


```javascript
fetch("http://pokeapi.co/api/v2/pokemon/butterfree")
  .then(function (response) {
    // tell it to read the JSON.
    return response.json();
  })
  .then(function (data) {
    console.log(data);
  })
```


Alternatively you could also condense this a bit.


```javascript
fetch("http://pokeapi.co/api/v2/pokemon/butterfree")
  .then(function (response) {
    // read the JSON
    response.json().then(function (data) {
      // log the data
      console.log(data);
    });
  })
```


You might run into a CORS issue. To get around this you specify a mode of "cors".

```javascript
fetch("http://pokeapi.co/api/v2/pokemon/butterfree", { mode: "cors" })
```

* Console log your search data for a **Charmander**.


## Promises

You might have noticed the use of the `.then` on the end of the fetch. This is just an aysnc structure that allows you to control the flow of your program as it awaits some event.

This is not unlike how we specify functions to await and do something on some user interactions: click, hover, etc.

The async thing we are awaiting in this case is the request's response from Pokemon API. Then when we call `response.json()` we are waiting for the response to be finished parsing from **text** to **JSON**.


See MDN promises to learn more.


### jQuery Request

If you don't like the `fetch` feature or you want to not rely upon experimental features you can add jQuery.


Just find a CDN link for jQuery's source. Then just add the following:


```javascript
$.get("hhttp://pokeapi.co/api/v2/pokemon/butterfree").done(function (data) {
  console.log(data);
});
```

This is pretty cool because you just get access to the parsed data right away.

* Console log your search data for a **Charmander**.

### Forms

When using forms you will need to be clear about a few things

* Clicking a button on a form will submit
* Hitting enter will trigger a click on a submit button

When you submit a form the browser will look for **method** and **action** attributes to make a request with the form data.

This is troublesome! We do not want our nice little one page app to reload and chances are we have not specify any of those attributes.


Hence when we use forms we will listen for a submit event and have to **prevent the browsers default behavior**.

```javascript
document.querySelector("#myForm").addEventListener("submit", function (event) {
  // We stop the default behavior for this event.
  event.preventDefault();
});
```


## Assessment

Using your knowledge of APIs, events, and objects try the following in JS Bin or Codepen.

* Add a form to your site with an id of `searchName` for the  input field

  ```html
  <input id="searchName" type="text">
  ```

* When the form is submitted create a search request using the `searchName` and the `fetch` method.
  * Console log the response JSON
* Add jQuery to the project and rewrite your request to use `$.get`.
* Create a `#results` div on your page
* Set the HTML of the `#results` to the `name` and `id` (the pokemon number) of the result you get back from Pokemon API.
  * Wrap your result in a `h2` and `p` tags for the `name` and `id`.


### Bonus Assessment

* Alert the user and don't run the request if the `searchName` is empty!
* Display the Pokemon Weight and Height of each result
* Add each search to an array of `previousResults`
  * Add a div called `#previousResults`
  * Each time someone runs a new search **map** over the previousResults and display each with its `id`, `name`, `height`, and `weight`
* Add a new form `#filterPrevious` with a select tag for displaying the results in the following ways:
  * Search Order: the order they were searched in
  * Name: the alphabetical order of the previously searched Pokemon
  * Pokemon Number: the `id` of the previously searched Pokemeon

### SUPER BONUS?

* Style it up and add CSS to make it look cool!


### SOLUTION?

[solution](https://codepen.io/thedelmer/pen/owjbGp?editors=1111)
