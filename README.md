# WebSearch Link Limit

Adds SearXNG web search results to LLM prompts, with a Link Limiter for the links the model receives in tool calls. This is a SearXNG-only fork of the WebSearch extension.

## Source

Only [SearXNG](https://github.com/searxng/searxng) is supported. Enter the base URL of your instance (private or public) in the settings. Optionally add a preferences string from SearXNG - preferences - COOKIES - Copy preferences hash.

## How to use

1. Make sure you use the latest version of SillyTavern (staging branch preferred).
2. Install the extension via the "Download Extensions & Assets" menu, or extract it into `SillyTavern/public/scripts/extensions/third-party/Extension-WebSearch-LinkLimit`.
3. Open the "WebSearch Link Limit" extension settings, set your SearXNG URL, and enable the extension.
4. Search results are added to the prompt as you chat. **Only user messages trigger the search.**
5. To include search results more organically, wrap search queries with single backticks: ```Tell me about the `latest Ryan Gosling movie`.``` will produce a search query `latest Ryan Gosling movie`.
6. Optionally, configure the settings to your liking.

## Settings

### General

1. Enabled - toggles the extension on and off.
2. Cache Lifetime - how long (in seconds) search results are cached. Default = one week.

### Prompt Settings

1. Prompt Budget - the maximum size of the inserted text, in characters (not tokens).
2. Insertion Template - how the result gets inserted. Supports `{{query}}` and `{{text}}`.
3. Injection Position - before/after the system prompt, or in-chat at a depth.

### Search Activation

1. Use Function Tool - lets the model call `WebSearchLL` and `VisitLinksLL`. Requires a Chat Completion API with tool calling enabled. **Disables all other activation methods when on.**
2. Use Backticks - activates search with words in single backticks.
3. Use Trigger Phrases - activates search with trigger phrases.
4. Use Regex - activates search when the user message matches a regex rule.
5. Trigger Phrases and Max Words - phrases that start a search, and the maximum words per query. A message starting with a period is ignored.

### Page Scraping

1. Visit Links - extract text from result pages and save it as a file attachment.
2. Visit Count - how many links are visited per query.
3. Visit Domain Blacklist - domains that are never visited, one per line.
4. File Header and Block Header - templates for the saved file.
5. Save Target - message attachment, Data Bank, or images only.
6. Include Images - attach images from results (SearXNG supports this).

### Link Limiter

1. Max Links - the maximum number of links sent to the model per tool call (0 = no limit, default). Applies to the links and image URLs returned by `WebSearchLL`, and to the links the model passes to `VisitLinksLL`. Each list is capped separately.

## More info

Search results from the latest query stay in the prompt until the next valid query. To ask a follow-up without triggering a search, start the message with a period. To discard earlier queries, start the message with `!`.

Slash command: `/websearchll (links=on|off snippets=on|off [query])`, for example `/websearchll links=off snippets=on how to make a sandwich`.
