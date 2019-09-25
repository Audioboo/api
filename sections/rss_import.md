# RSS Imports

RSS Imports are our recommended way to regularly upload new content to Audioboom from another system.

You'll need to publish an RSS feed conforming to the [RSS 2.0 specification](https://validator.w3.org/feed/docs/rss2.html).

# Supported tags

| Episode attribute                   | tag                                                                      |                                        |
|-------------------------------------|--------------------------------------------------------------------------|----------------------------------------|
| title                               | `//item/itunes:title`, `//item/title`                                    | required                               |
| audio import url                    | `//item/enclosure`, `//item/media:content` (with type=audio/mpeg or mp3) | required                               |
| image import url                    | `//item/enclosure`, `//item/media:content` (with type=image/*)           | required                               |
| guid                                | `//item/guid`                                                            | recommended to avoid duplicate imports |
| html description / text description | `//item/content:encoded`, `//item/description`, `//item/itunes:summary`  | optional                               |
| episodeNumber                       | `//item/itunes:episode`                                                  | optional                               |
| seasonNumber                        | `//item/itunes:season`                                                   | optional                               |
| episodeType                         | `//item/itunes:episodeType`                                              | optional                               |
| recorded_at                         | `//item/pubDate`                                                         | optional                               |


