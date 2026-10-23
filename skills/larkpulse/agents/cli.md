# CLI media transport

For Cursor, Claude Code, OpenClaw, Hermes, and other agents that can make outbound HTTP:

- Omit `file` on `upload_media`.
- If the image is already at a public https URL, call `upload_media` with `url`.
- If you hold a local file and can HTTP PUT:
  1. Call `create_media_upload` with `file_name`, `file_type` (e.g. `image/png`, `video/mp4`, or `application/pdf` for a LinkedIn carousel), and `file_size`.
  2. PUT the raw bytes to the returned `upload_url` with the **same** `Content-Type` as `file_type`:

     ```bash
     curl -X PUT --upload-file ./photo.png -H "Content-Type: image/png" "<upload_url>"
     ```

  3. Call `finalize_media` with the returned `key` and the same `file_type`.
- Use the returned `media_url` on `save_draft` / `publish_post` / `schedule_post` / `add_to_category`.
- If ingest fails, stop; never silently save a text-only version.
