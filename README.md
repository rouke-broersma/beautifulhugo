# Beautiful Hugo - An adaptation of the Beautiful Jekyll theme

![Beautiful Hugo Theme Screenshot](https://github.com/halogenica/beautifulhugo/blob/master/images/screenshot.png)

## Installation

    $ mkdir themes
    $ cd themes
    $ git submodule add https://github.com/halogenica/beautifulhugo.git beautifulhugo
    

See [the Hugo documentation](https://gohugo.io/themes/installing/) for more information.

## Extra Features

### Responsive

This theme is designed to look great on both large-screen and small-screen (mobile) devices.

### Syntax highlighting

This theme has support for either Hugo's lightning fast Chroma, or both server side and client side highlighting. See [the Hugo docs for more](https://gohugo.io/content-management/syntax-highlighting/).
Also see [the markup docs](https://gohugo.io/getting-started/configuration-markup#highlight) for documentation on how to change the chroma settings.

### Disqus support

To use this feature, uncomment and fill out the `disqusShortname` parameter in `config.toml`.

### Staticman support

Add *Staticman* configuration section in `config.toml` or `config.yaml`

Sample `config.toml` configuration

```
[Params.staticman]
  api = "https://<API-ENDPOINT>/v3/entry/{GIT-HOST}/<USERNAME>/<REPOSITORY-BLOGNAME>/master/comments"
[Params.staticman.recaptcha]
      sitekey: "6LeGeTgUAAAAAAqVrfTwox1kJQFdWl-mLzKasV0v"
      secret: "hsGjWtWHR4HK4pT7cUsWTArJdZDxxE2pkdg/ArwCguqYQrhuubjj3RS9C5qa8xu4cx/Y9EwHwAMEeXPCZbLR9eW1K9LshissvNcYFfC/b8KKb4deH4V1+oqJEk/JcoK6jp6Rr2nZV4rjDP9M7nunC3WR5UGwMIYb8kKhur9pAic="
```

Note: The public `API-ENDPOINT` https://staticman.net is currently hitting its API limit, so one may use other API instances to provide Staticman comment service.

The section `[Params.staticman.recaptcha]` is *optional*.  To add reCAPTCHA to your site, you have to replace the default values with your own ones (to be obtained from Google.)  The site `secret` has to be encrypted with

    https://<API-ENDPOINT>/v3/encrypt/<SITE-SECRET>

You must also configure the `staticman.yml` in you blog website.

```
comments:
  allowedFields: ["name", "email", "website", "comment"]
  branch            : "master"
  commitMessage     : "New comment in {options.slug}"
  path: "data/comments/{options.slug}"
  filename          : "comment-{@timestamp}"
  format            : "yaml"
  moderation        : true
  requiredFields    : ['name', 'email', 'comment']
  transforms:
    email           : md5
  generatedFields:
    date:
      type          : "date"
      options:
        format      : "iso8601"
  reCaptcha:
    enabled: true
    siteKey: "6LeGeTgUAAAAAAqVrfTwox1kJQFdWl-mLzKasV0v"
    secret: "hsGjWtWHR4HK4pT7cUsWTArJdZDxxE2pkdg/ArwCguqYQrhuubjj3RS9C5qa8xu4cx/Y9EwHwAMEeXPCZbLR9eW1K9LshissvNcYFfC/b8KKb4deH4V1+oqJEk/JcoK6jp6Rr2nZV4rjDP9M7nunC3WR5UGwMIYb8kKhur9pAic="
```

If you *don't* have the section `[Params.staticman]` in `config.toml`, you *won't* need the section `reCaptcha`  in `staticman.yml`

### Site Disclaimer

If you need to put a Disclaimer on your website (e.g. "My views are my own and not my employer's"), you can do so via the following:

* Uncomment and edit the `disclaimerText` parameter in `config.toml`.
* If you need to adjust the disclaimer's styling, modify the declarations within the `footer div.disclaimer` selector in `static/css/main.css`.

> The code for the disclaimer text is in `layouts/partials/footer.html`.  Moving this code block to another partial file (or relocating it within `footer.html`) will require changes to the css selector in `main.css` as well.
### Utterances Commenting Support

If you wish use [Utterances](https://github.com/utterance/utterances) comments on your site, you'll need to perform the following:

* Ensure you have a GitHub public repository, which you've granted permissions to the [Utterances GitHub App](https://github.com/apps/utterances). 
* Add the utterances toml parameters to the `[Params]` section in **config.toml** (shown below).
* Ensure you have the `layouts/partials/utterances.html` file included in your themes directory.  This file embeds the actual Utterances script that gets output when you run through the configuration builder at [https://utteranc.es/](https://utteranc.es/).
* Ensure you have the updated `layouts/_default/single.html` which has three lines (shown below) to insert Utterances in a specific location.   If you wish to put it somewhere else (or embed in additional pages), move those lines somewhere else.

**config.toml**
```toml
# Ensure the below 4 lines go within the [Params] section
utterances = true  #Run the utterances script in _default/single.html to load https://utteranc.es comments
utterancesRepo = "GHUsername/Repository.Name" # Utterances is enabled when this param is set
utterancesTheme = "github-light" # Default: github-dark
utterancesIssueTerm = "pathname" # Default: pathname
```

**single.html**
```
{{ if .Site.Params.utterances }}
  {{ template "partials/utterances.html" . }}
{{ end }}
```

### Google Analytics

To add Google Analytics, simply sign up to [Google Analytics](https://www.google.com/analytics/) to obtain your Google Tracking ID, and add this tracking ID to the `googleAnalytics` parameter in `config.toml`.

### Commit SHA on the footer

If the source of your site is in a Git repo, the SHA corresponding to the commit the site is built from can be shown on the footer. To do so, two site parameters `commit` has to be defined in the config file `config.toml`:

```
enableGitInfo = true
[Params]
  commit = "https://github.com/<username>/<siterepo>/tree/"
```

See at [vincenttam/vincenttam.gitlab.io](https://gitlab.com/vincenttam/vincenttam.gitlab.io) for an example of how to add it to a continuous integration system.

### Multilingual

To allow Beautiful Hugo to go multilingual, you need to define the languages
you want to use inside the `languages` parameter on `config.toml` file, also
redefining the content dir for each one. Check the `i18n/` folder to see all
languages available.

```toml
[languages]
  [languages.en] 
    contentDir = "content/en" # English
  [languages.ja]
    contentDir = "content/ja" # Japanese
  [languages.br]
    contentDir = "content/br" # Brazilian Portuguese
```

Now you just need to create a subdir within the `content/` folder for each
language and just put stuff inside `page/` and `post/` regular directories.
```
content/      content/      content/  
└── en/       └── br/       └── ja/ 
    ├── page/     ├── page/     ├── page/
    └── post/     └── post/     └── post/

```
 
### Extra shortcodes

There are two extra shortcodes provided (along with the customized figure shortcode):

#### Details

This simply adds the html5 detail attribute, supported on all *modern* browsers. Use it like this:

```
{{< details "This is the details title (click to expand)" >}}
This is the content (hidden until clicked).
{{< /details >}}
```

#### Split

This adds a two column side-by-side environment (will turn into 1 col for narrow devices):

```
{{< columns >}}
This is column 1.
{{< column >}}
This is column 2.
{{< endcolumns >}}
```

### Social Media Icons

In order to show social media icons in the footer, add a section like this to your `config.yaml`.  You can see the full list of supported social media sites in `data/beautifulhugo/social.toml`.

```yaml
author: 
  name: "Author Name"
  website: "https://example.com"
  github: halogenica/beautifulhugo
  twitter: username
  discord: 96VAXXvjCB
```

### PageSpeed Improvements

The following improvements help improve PageSpeed Insight scores:

* The `logoheight` and `logowidth` params in `config.toml`  


## About

This is an adaptation of the Jekyll theme [Beautiful Jekyll](https://deanattali.com/beautiful-jekyll/) by [Dean Attali](https://deanattali.com/aboutme#contact). It supports most of the features of the original theme, and many new features. It has diverged from the Jekyll theme over time, with years of community updates.

## License

MIT Licensed, see [LICENSE](https://github.com/halogenica/Hugo-BeautifulHugo/blob/master/LICENSE).
