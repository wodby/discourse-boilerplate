# Discourse boilerplate

Add your own and third-party plugins to Discourse and deploy them with Wodby.

Use it with the [buildable Discourse](https://github.com/wodby/service-discourse-buildable)
service (`discourse-buildable`). For Discourse with only the plugins it ships
with, use the [Discourse](https://github.com/wodby/service-discourse) service
instead.

## Discourse's version

Choose the Discourse release line when you create the app. The build starts
from the prebuilt [`wodby/discourse`](https://github.com/wodby/discourse) image
of that line and adds your plugins. Your plugins must support it.

## Adding plugins

List plugins in `plugins.txt`, one Git repository URL per line, optionally
followed by a branch or tag:

```
https://github.com/discourse/discourse-bbcode.git
https://github.com/example/discourse-my-plugin.git v1.2.0
```

Or commit a plugin of your own under `plugins/`, one directory per plugin with
its `plugin.rb`:

```
plugins/
  my-plugin/
    plugin.rb
    assets/javascripts/...
```

The build fails if a plugin has the name of a plugin that ships with Discourse,
such as chat, solved or data explorer: turn those on in Discourse's settings
instead.

On every deployment Discourse migrates its database, plugins' migrations
included.

## Files

| Path | Purpose |
| --- | --- |
| `plugins.txt` | Plugins cloned from Git repositories |
| `plugins/` | Plugins committed to this repository |
| `.wodby/pipeline.yml` | The Wodby CI pipeline that builds and deploys the image |
| `.dockerignore` | Files left out of the build |
