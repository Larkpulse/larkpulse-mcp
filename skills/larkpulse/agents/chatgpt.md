# ChatGPT media transport

For images generated or attached in the current conversation:

- Use `upload_media`.
- Pass the conversation image as `file`.
- Do not pass local filesystem paths (`/mnt/data`, `file://`, filenames, raw file ids).
- Do not use `url` for conversation images.
- Do not use presigned uploads or HTTP PUT.
- Use the returned `media_url` for the subsequent post action.
- If the host cannot resolve the image into `file`, ask the user to attach it.
- If upload fails, stop; never silently save a text-only version.
