# WeChat Publishing

Use this step only when the user requests WeChat publication.

## Goal

Create a WeChat Official Account draft from the generated Markdown report.

## Recommended Behavior

1. Confirm WeChat credentials are configured.
2. Convert Markdown to WeChat-compatible HTML or the format required by the available publishing script.
3. Upload or reference the cover image according to the user's publishing setup.
4. Create a draft, not an immediate broadcast, unless the user explicitly asks to publish publicly.
5. Return the draft identifier or media identifier if the API provides one.

## Required Environment

See `references/configuration.md` for:

- `WECHAT_APP_ID`
- `WECHAT_APP_SECRET`
- `WECHAT_DEFAULT_COVER`
- `WECHAT_HTTP_PROXY`

## Safety

- Do not hardcode credentials.
- Do not include a personal QR code by default.
- Do not mass-send or publish publicly unless explicitly requested.
- If the WeChat API fails, keep the Markdown report and explain that draft creation was skipped.

## Integration Note

This skill does not require a specific publishing implementation. If the user's environment already has a Markdown-to-WeChat tool, use it. Otherwise, stop after generating the Markdown report and tell the user which configuration or script is missing.
