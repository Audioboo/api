## Audio Clips (Episodes) ##

### All audio clips ###

These return [paginated](https://github.com/audioboom/api/blob/master/sections/pagination.md) responses.

 * `GET /audio_clips`
  returns all audio clips in chronological order (most recent first)
 * `GET /audio_clips?find[query]=*query*`
  searches for audio clips matching the *query* plain-text search term.
  returns all audio clips in chronological order (most recent first)
 * `GET /audio_clips/featured`
  returns the editorially "featured" audio clips as appear on the web-site
 * `GET /audio_clips/popular`
  returns the most popular audio clips ordered by recent listens

### Tagged audio clips ###
This call will return a [paginated](https://github.com/audioboom/api/blob/master/sections/pagination.md) response.

 * `GET /tag/*tag*/audio_clips`
  returns all the audio clips tagged with the specified tag.


### Channel's clips ###

`GET /channels/*channel_id*/audio_clips` returns audio clips for that particular channel or podcast.


#### V2 Featured Feeds ####

When requesting with `Accept: application/json; version=2`, the following endpoints are available:

Retrieve all featured clips, across all categories:

  * `http://api.audioboom.com/audio_clips/category_featured`
  
  Categories can be explicitly requested by passing an array of their ids - eg `?category_ids[]=60&category_ids[]=70`

Retrieve all clips in featured channels:

  * `http://api.audioboom.com/audio_clips/channel_featured`
  
  Again, Categories can be explicitly requested by passing an array of their ids - eg `?category_ids[]=60&category_ids[]=70`

### Audio clip details ###

 * `GET /audio_clips/*audio_clip_id*`
  returns the details of the audio clip specified by *audio_clip_id*.

 * `GET /audio_clips/*audio_clip_id*.mp3`
  this will respond with a browser re-direct to the mp3 audio data for the audio clip specified by *audio_clip_id*

### Posting audio clips ###

`POST /account/audio_clips`

this will post an audio clip into the recent clips of the user linked to the OAuth access token used.

To post to a channel, you can use

`POST /channels/*channel_id*/audio_clips`

which will post an audio clip to the specified channel.

The same parameters are used for either endpoint:


 * `audio_clip[uploaded_data]` (required)
  The uploaded audio data as a multipart file, see [Audio Formats](https://github.com/audioboom/api/blob/master/sections/reference_index.md#audio-formats) and [File Uploads](https://github.com/audioboom/api/blob/master/sections/reference_index.md#file-uploads).

 * `audio_clip[uuid]` (recommended)
  A [universally unique identifier](http://en.wikipedia.org/wiki/Universally_unique_identifier), to aid the server in duplicate-detection.  The uuid must not contain spaces or a newline characters.

 * `audio_clip[uploaded_image]`
  The uploaded image data as a multipart file, see see [Image Formats](https://github.com/audioboom/api/blob/master/sections/reference_index.md#image-formats) and [File Uploads](https://github.com/audioboom/api/blob/master/sections/reference_index.md#file-uploads).

 * `audio_clip[title]` (required)
  The title for the audio clip.

 * `audio_clip[recorded_at]`
  The time that the clip was recorded, in "YYYY-MM-DD HH:MM:SS ±HHMM" format.

 * `audio_clip[description]`
  The plain-text description for the episode.  This is mutually exclusive with `audio_clip[episode_description_attributes]`.
  
 * `audio_clip[episode_description_attributes][html_description_source]`
  The description for the episode, as HTML.  This is mutually exclusive with `audio_clip[description]`.
  
 * `audio_clip[episode_description_attributes][summary]`
  The plain-text summary of the episode.  This is mutually exclusive with `audio_clip[description]`.


### Updating audio clips ###

You can update audio clips by sending a PUT request to the boo's location :

`PUT /audio_clips/*audio_clip_id*`

It accepts the same parameters as those shown in the creation method.

### Deleting audio clips ###

You can mark audio clips for deletion by sending a DELETE request to the boo's location :

`DELETE /audio_clips/*audio_clip_id*`
