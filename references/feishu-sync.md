# Feishu/Lark Sync

Use this step only when the user requests Feishu or Lark document sync.

## Goal

Insert the generated Markdown report into a configured Feishu/Lark document or wiki page.

## Required Environment

Feishu/Lark sync requires `lark-cli` to be installed and authenticated in the local environment. If `lark-cli` is not installed, install it first according to the official Lark/Feishu CLI documentation, then run the login command in the Authentication section.

See `references/configuration.md` for:

- `FEISHU_DOC_URL`
- `LARK_CLI_PATH`
- `LARK_CLI_IDENTITY`
- `FEISHU_INSERT_MODE`
- `FEISHU_TARGET_BLOCK_ID`

## Recommended Flow

1. Check that `lark-cli` is installed and authenticated.
2. Verify `FEISHU_DOC_URL` is configured.
3. Choose insert behavior:
   - `append`: safest default, adds the report to the end.
   - `insert_before`: useful for latest-first documents; requires a target block ID.
   - `insert_after`: useful for inserting below a fixed heading; requires a target block ID.
4. Run the update command with the generated Markdown file.
5. Confirm the response indicates success.

## Example Commands

Use these as patterns and substitute environment values.

```bash
"$LARK_CLI_PATH" docs +update \
  --doc "$FEISHU_DOC_URL" \
  --mode append \
  --markdown "@./ai-news-YYYY-MM-DD.md" \
  --as "${LARK_CLI_IDENTITY:-user}"
```

For latest-first insertion:

```bash
"$LARK_CLI_PATH" docs +update \
  --doc "$FEISHU_DOC_URL" \
  --mode insert_before \
  --start-block-id "$FEISHU_TARGET_BLOCK_ID" \
  --markdown "@./ai-news-YYYY-MM-DD.md" \
  --as "${LARK_CLI_IDENTITY:-user}"
```

## Authentication

If authentication has expired, ask the user to log in locally:

```bash
lark-cli auth login --domain all
```

Then retry the sync.

## Safety

- Do not include private document URLs in the skill.
- Do not overwrite a whole document unless the user explicitly requests it.
- Prefer `append` when the document structure is unknown.
- If sync fails, keep the Markdown report and report the failed command stage.
