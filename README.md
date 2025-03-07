# SwackQuote

A repository for the QOTD bot on the swan_hack Discord server.

To add a quote, fork, add it to `quotes.toml`, and make a pull request... hopefully it provides you less pain than it did me!

### Requirements

First and foremost, if you're wishing to run this bot on your own server, you must provide:
- [your own bot token](https://discordapp.com/developers/applications/) in `token.txt`
- [your user ID](https://support.discord.com/hc/en-us/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-) in `admins.toml` (with a nice handle in the format `<name> = <id>`, such as `gnome = 356467595177885696`)
- the [ID of the channel you](https://support.discord.com/hc/en-us/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-) wish the bot to use in `channel.txt`.

Requirements:
- [py-cord](https://pypi.org/project/py-cord/)
- [tomli](https://pypi.org/project/tomli)
- [tomli-w](https://pypi.org/project/tomli-w)
- [requests](https://pypi.org/project/requests)

We have a [poetry](https://python-poetry.org/) `pyproject.toml` setup for easy installation.  Just run `poetry install`!

### Formatting for Quotes

The flat-file uses the TOML specification for storing quotes.  Quotes are formatted like so:

```toml
[identifier] # some unique, stable identifier, such as a date and number (2022-08-08-example-1)
submitter = "the name of who submitted it (aka, your discord handle)"
quote = "the quote you're adding"
attribution = "whoever said or wrote it, optionally where it was said or written"
source = "a URL for the quote or source, if you have it"
```

**You must include your name as the `submitter`, and the `quote`, these are _required_.**

Currently, the `attribution`, `source`, and `embed` field are optional.

If given, the `attribution` field will appear after the quote, separated by a `~`. If given, the `source` field will be linked to by the quote. When `embed` is given as `embed = true` and a `source` has been provided, the source will be embedded beneath the quote (such as a YouTube video).

If you do not know who, or cannot find the original attribution, please use `Unknown`, or `Various`. If many have said it, use `Apocryphal`. But, if you're having trouble, you can always ask others who may know it themselves or know where to check.

If citing both a person and a work, please do this in a format that is sensible, perhaps `Person, Work`, inside the `attribution` field - with a URL (i.e. for Tweets, videos, or articles) in the `source` field. We tend to prefer this is included in the `attribution`, so use `source` for HTTP/HTTPS URLs (where relevant). If the year or edition is relevant, include this either parenthesised `(3rd edition)`, or following it like, say, `Unix Epoch, 1970`. With dating, we prefer and assume [Common Era](https://en.wikipedia.org/wiki/Common_Era), such as `Julius Caesar (100 - 44 BCE)` or `de Finibus Bonorum et Malorum, 45 BCE`.

When citing something said by a character, use a simple rule of thumb: if you know who wrote it, cite as `Author, Character`, otherwise cite the character directly. For example, `The Doctor` or `Jean-Luc Picard` are cited as themselves, because various scriptwriters and actors are involved, whereas Macbeth is cited as `William Shakespeare, Macbeth`, as we're quoting his script (the character should be listed, though in the case of Macbeth, it would be redundant). Other examples, such as `Sherlock Holmes`, may be context dependent, such as the books will be cited as `Arthur Conan Doyle, Sherlock Holmes`, whereas film or show adaptations are cited accordingly (`Character, Film/Show, Year`). Shows may include the specific episode by name and perhaps number, where relevant, but further details (timestamps etc.) should not be included (but may be part of a `source` URL, such as timestamped links to YouTube).

So, when done properly, attributions should use the order **`"Author, Character, Work, Edition, Year"`**. These may be omitted where redundant or unknown (though we prefer an unknown author to be cited as such, except as in such cases as the examples above). Commas separate for clarity, and where clear may be removed or instead parenthesised (as in above examples). Additional context or aspects of the attribution may be included if it is felt to improve the quote, preferably after the above ordering.

Do not put URLs in the attribution; Markdown links may be accepted, but lengthy raw URLs likely will not be. A single URL may be included in the `source` (i.e. `source = "https://www.youtube.com/watch?v=dQw4w9WgXcQ"`), and if `embed = true` is set for that quote, the URL will have an embed displayed alongside the quote. The embedding is janky, not visually appealing, and not what we desired; if you can improve this, please contribute!

We do not recommend you set `embed` whenever you have a URL, as it may lead to duplication of the quote and visual clutter. Also, if it is a link to a video or audio, and it includes more than the listed quote, it should probably not be embedded, as the video/audio is not specifically a form of that quote.

For quotes that span multiple lines, use `"""` at the beginning and end, on separate lines.

For quotes containing code, use `'''` for raw multi-line strings, and then use ` ``` ` to create a code block, remembering to close them both afterwards.

All discord-accepted markdown should be rendered properly. Individual quotes must be less than 4000 bytes long (UTF-8). In practice, we recommend quotes be less than 1500 bytes (UTF-8), as with most character sets this would fill the screen on many mobile displays. Most of the time, they are much shorter anyway, just a couple sentences at most. When in doubt, keep it concise.

When adding quotes, please take care to update the trailing count comments, spaced out in groups of 5 quotes before a comment (so `#5` if followed by `#10` and so on). The one at the bottom should have the exact number of quotes, but if you round up to the nearest 5 then it's unlikely anyone will complain.

### Quotes from Fictional Characters

Quotes taken from fiction should list the character.

Example:

```toml
[pre-toml-130]
submitter = "Gnome"
quote = "In the strict scientific sense we all feed on death - even vegetarians."
attribution = "Spock, Wolf in the Fold, stardate 3615.4"
```

### Quotes from Antiquity

Quotes taken from antiquity should use [Common Era](https://en.wikipedia.org/wiki/Common_Era) dating.

Example:

```toml
[2022-05-05-Yet-another-Greek-philosopher]
submitter = "Gnome"
quote = "There is nothing permanent except change."
attribution = "Heraclitus (535-475 BCE)"
```

### Quotes from Code

Quotes of code should be multi-line strings starting with a code fence (not indentation based), which may have syntax highlighting specified (might not work on all devices).

```toml
[pre-toml-300]
submitter = "Gnome"
quote = """```python
def isprime(n): return not re.match(r\"^1?$|^(11+?)\\1+$\", \"1\"*n)
```"""
attribution = "segfault"
```

### Further Reading

For further reading, see:
- [The TOML documentation for how strings work](https://toml.io/en/)
- [The Discord Markdown documentation for formatting](https://support.discord.com/hc/en-us/articles/210298617-Markdown-Text-101)
