# audioBoom Categories

**Version 2 API** - you should use `Accept: application/json; version=2` when making these requests

Posts and channels are categorized into different areas. You can obtain lists of them via the Categories API.  The categories are organized hierarchically via a parent_id field, with an "Everything" category at the top level.

Get Categories
----
Returns a list of categories used on audioBoom:

`GET /categories` :

```json
{
  {
    "body": [
    {
      "id": 63,
      "title": "Business",
      "description": "Insight analysis tips and tricks ",
      "parent_id": 98,
      "priority": 0,
      "square_image_url": "http://d15mj6e6qmt1na.cloudfront.net/i/10711101"
    },
    {
      "id": 66,
      "title": "Comedy",
      "description": "Listen for laughs",
      "parent_id": 98,
      "priority": 0,
      "square_image_url": "http://d15mj6e6qmt1na.cloudfront.net/i/10749503"
    },
    {
      "id": 67,
      "title": "Culture",
      "description": "Feed your mind",
      "parent_id": 98,
      "priority": 0,
      "square_image_url": "http://d15mj6e6qmt1na.cloudfront.net/i/10711109"
    },
    ...
```



Show category contents
----

`GET /categories/<id>` Returns all channels and audio clips within the given category.

`GET /categories/<id>/boos` Returns all audio clips within the given category.
  
`GET /categories/<id>/boos/featured` Returns all featured audio clips within the given category.
  
`GET /categories/<id>/boos/channel_featured` Returns all audio clips in featured channels within the given category.
  
`GET /categories/<id>/channels` Returns all channels within the given category.
  
`GET /categories/<id>/channels/featured` Returns all featured channels within the given category.