# ReadingRate

ReadingRate's book catalog and reading tracker, for Claude, ChatGPT, Gemini CLI and Cursor. The plugin connects the ReadingRate server (https://mcp.readingrate.com/mcp) and adds six skills that walk an assistant through the things readers ask for most.

| Skill | What it does | Account |
|---|---|---|
| `shelf-to-library` | Identifies the books in a photo of a shelf or a pasted list, and adds them to the reader's library when asked | Identifying: none. Adding: connected |
| `log-reading` | Logs reading from a plain sentence: pages read, the page reached, a book started, finished or set aside | Connected |
| `next-book` | Chooses the next book by the time the reader has, their pace and the difficulty they usually read | Optional |
| `where-to-start` | Lays out a reading path into a country's, a language's, a period's or a genre's literature, from ReadingRate's ranked lists | Optional |
| `book-debrief` | Talks through a finished book from the passages and notes the reader saved, and keeps the conclusions if they want | Connected |
| `book-club-prep` | Prepares for a club meeting: the schedule, the pages left, and questions within the pages read | Connected |

The catalog works without an account: difficulty scores in nine dimensions, reading times, literary regard, prizes and ranked lists. A ReadingRate account (https://readingrate.com) connects the reader's library, reading log, quotes, notes and book clubs.

Privacy policy: https://readingrate.com/privacy. Support: https://readingrate.com/contact.

## Install in Claude Code

```
/plugin marketplace add simonsbookclub/readingrate-plugin
/plugin install readingrate-books@readingrate
```

## Install in Gemini CLI

```
gemini extensions install https://github.com/simonsbookclub/readingrate-plugin
```

Sign in with `/mcp auth readingrate`, or when Gemini asks the first time a tool needs your account.

## Any other app

Add the server address https://mcp.readingrate.com/mcp as a remote (Streamable HTTP) MCP server. It signs in with OAuth, so there is no key to copy. The server is listed in the MCP Registry as `com.readingrate/readingrate`.

## License

The skills and manifests in this plugin are under the MIT License (`LICENSE`). The ReadingRate service they connect to has its own terms: https://readingrate.com/terms.
