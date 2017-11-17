## Image sizing

Clients can include one or more `image_size_hint` parameters to request different image sizes from the API.  This parameter can be included in most API requests.

For example, `image_size_hint[thumb]=100x100` will return both the original image, and the nearest image we can supply that's 100x100.  Not every size is supported, so the resulting size may not exactly match the requested one.


### Example

`GET http://api.audioboom.com/audio_clips?image_size_hint[thumb]=100x100`

```json
{
  "window": 60,
  "version": 200,
  "timestamp": 1424868012,
  "body": {
    "audio_clips": [
    {
      "id": 2928902,
      "title": "Wayne Shields Greater Manchester Fire ",
      "urls": {
        "detail": "http://audioboom.com/boos/2928902-wayne-shields-greater-manchester-fire",
        "high_mp3": "http://audioboom.com/boos/2928902-wayne-shields-greater-manchester-fire.mp3",
        "image": "http://d15mj6e6qmt1na.cloudfront.net/i/13151373",
        "images": {
          "thumb": {
            "width": 150,
            "height": 148,
            "url": "http://d15mj6e6qmt1na.cloudfront.net/i/13151373/150x150"
          }
        },
      },
    },
...
```

The 'thumb' name is defined by the client, and just used to name the resulting image structure in the response.  For example, you could ask for `image_size_hint[mini]=10x10&image_size_hint[maxi]=1000x1000`, which would give an `images` structure like : 

```json
"images": {
  "mini": {
    "width": 50,
    "height": 50,
    "url": "http://d15mj6e6qmt1na.cloudfront.net/i/13151373/50x50"
  },
  "maxi": {
    "width": 500,
    "height": 500,
    "url": "http://d15mj6e6qmt1na.cloudfront.net/i/13151373/500x500"
  }
}
```

## Version 2 differences

Note that the image structure returned when hitting V2 APIs is somewhat different than in V1.

By default the V2 API responds with the 'original' URL:

```json
"profile_image": {
   "original": "https://d15mj6e6qmt1na.cloudfront.net/i/9746510"
}
```

if you include an image hint (eg `image_size_hint[mini]=10x10`), you'll see the additional images defined within the same structure:

```json
"profile_image": {
   "original": "https://d15mj6e6qmt1na.cloudfront.net/i/9746510",
   "mini": "https://d15mj6e6qmt1na.cloudfront.net/i/9746510/50x50"
}
```


## Geometry strings

A variety of formats are supported for the geometry string (the `10x10` part of `image_size_hint[foo]=10x10`).

If the size is suffixed with '<', we'll return the largest size that is still smaller than the given size.  Otherwise, we'll find the smallest image that is larger than the given size.  The height can be excluded, in which case the result will just be constrained on width, with it's natural height for the image aspect ratio.

By default, images are returned in their natural aspect ratio.  You can also request a size of `100x100/c`, which will scale the image to 100x100, keeping its aspect ratio and filling the result - this will keep the cropped image centered.
