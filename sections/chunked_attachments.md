# Chunked Attachments

Instead of creating audio clips or private messages by sending a single monolithic request containing the audio & image attachments, it is possible to break up the upload data into separate requests. This is particularly useful in mobile apps where the data connection may be unreliable and/or slow.


You would normally perform `POST /audio_clips` containing :

```json
{
	"audio_clip": {
		"title": "foo",
		"uploaded_data": <AudioFileData>,
		"uploaded_image": <ImageFileData>
	}
}
```

Using chunked uploads, you would create a chunked attachment, receive an id in return, continue to update that attachment piece by piece, and then finish creating the audio clip, using the attachment id in place of the file data :

```json
{
	"audio_clip": {
		"title": "foo",
		"uploaded_data": {
			"chunked_attachment_id": 10001
		},
		"uploaded_image": {
			"chunked_attachment_id": 10002
		}
	}
}
```


### Creating chunked attachments:

`POST /attachments`
```json
{
	"attachment": {
		"size": 178182,
		"filename": "audio.flac",
		"chunk": <PartialFileData>,
		"chunk_offset": 0
	}
}
```

`size` should be the total size of the original file.  `chunk` is a multipart file consisting of a portion of the original file, and `chunk_offset` is the byte-offset of where this portion is taken from.

You should receive a 201 response with a Location header containing the newly-created attachment's id.

### Updating chunked attachments:

You can then continue to upload chunks to that attachment id:

`PUT /attachments/9812`
```json
{
	"attachment": {
		"chunk": <PartialFileData>,
		"chunk_offset": 10000
	}
}
```

`chunk` is a multipart file consisting of a new portion of the original file, and `chunk_offset` is the byte-offset of where this portion is taken from.

Once you have sent all the different chunks of the file, you can use the attachment id in `POST /audio_clips` or `POST /account/outbox`.

For verification purposes, it is useful to include a SHA1 hexdigested fingerprint of the entire file - eg:

```json
{
	"audio_clip": {
		"title": "foo",
		"uploaded_data": {
			"chunked_attachment_id": 10001,
			"fingerprint": "e4eef1707a21faea8f2a88c663e38a27b97b4b0a"
		},
}
```

If the `fingerprint` is present, we can then verify that all chunks are present and assembled correctly.
