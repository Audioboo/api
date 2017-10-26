## Comments ##

### Fetch an audio clip's comments (V1 API) ###

 * GET /audio_clips/*audio_clip_id*/comments
 
Returns a paginated list of the comments on the given audio clip.


### Add a comment (V1 API) ###

 * POST /audio_clips/*audio_clip_id*/comments
 
Creates a comment from the authenticated user

 * `comment[body]` (required)
 Text for the comment body

### Delete a comment (V1 API) ###

 * DELETE /audio_clips/*audio_clip_id*/comments/*comment_id*
 
Deletes a comment from the authenticated user
