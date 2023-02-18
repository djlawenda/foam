## Test your installation[](https://gohugo.io/getting-started/usage/#test-your-installation)

After [installing](https://gohugo.io/installation/) Hugo, test your installation by running:

You should see something like:

```
hugo v0.105.0-0e3b42b4a9bdeb4d866210819fc6ddcf51582ffa+extended linux/amd64 BuildDate=2022-10-28T12:29:05Z VendorInfo=snap:0.105.0
```

## Display available commands[](https://gohugo.io/getting-started/usage/#display-available-commands)

To see a list of the available commands and flags:

To get help with a subcommand, use the `--help` flag. For example:

## Build your site[](https://gohugo.io/getting-started/usage/#build-your-site)

To build your site, `cd` into your project directory and run:

The [`hugo`](https://gohugo.io/commands/hugo/) command builds your site, publishing the files to the `public` directory. To publish your site to a different directory, use the [`--destination`](https://gohugo.io/commands/hugo/#options) flag or set [`publishDir`](https://gohugo.io/getting-started/configuration/#publishdir) in your site configuration.

## Draft, future, and expired content[](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)

Hugo allows you to set `draft`, `date`, `publishDate`, and `expiryDate` in the [front matter](https://gohugo.io/content-management/front-matter/) of your content. By default, Hugo will not publish content when:

-   The `draft` value is `true`
-   The `date` is in the future
-   The `publishDate` is in the future
-   The `expiryDate` is in the past

You can override the default behavior when running `hugo` or `hugo server` with command line flags:

```
hugo --buildDrafts    # or -D
hugo --buildExpired   # or -E
hugo --buildFuture    # or -F
```

Although you can also set these values in your site configuration, it can lead to unwanted results unless all content authors are aware of, and understand, the settings.

## Develop and test your site[](https://gohugo.io/getting-started/usage/#develop-and-test-your-site)

To view your site while developing layouts or creating content, `cd` into your project directory and run:

The [`hugo server`](https://gohugo.io/commands/hugo_server/) command builds your site into memory, and serves your pages using a minimal HTTP server. When you run `hugo server` it will display the URL of your local site:

```
Web Server is available at http://localhost:1313/ 
```

While the server is running, it watches your project directory for changes to assets, configuration, content, data, layouts, translations, and static files. When it detects a change, the server rebuilds your site and refreshes your browser using [LiveReload](https://github.com/livereload/livereload-js).

Most Hugo builds are so fast that you may not notice the change unless you are looking directly at your browser.

### LiveReload[](https://gohugo.io/getting-started/usage/#livereload)

While the server is running, Hugo injects JavaScript into the generated HTML pages. The LiveReload script creates a connection from the browser to the server via web sockets. You do not need to install any software or browser plugins, nor is any configuration required.

### Automatic redirection[](https://gohugo.io/getting-started/usage/#automatic-redirection)

When editing content, if you want your browser to automatically redirect to the page you last modified, run:

```
hugo server --navigateToChanged
```

## Deploy your site[](https://gohugo.io/getting-started/usage/#deploy-your-site)

When you are ready to deploy your site, run:

This builds your site, publishing the files to the public directory. The directory structure will look something like this:

```
public/
├── categories/
│   ├── index.html
│   └── index.xml  <-- RSS feed for this section
├── post/
│   ├── my-first-post/
│   │   └── index.html
│   ├── index.html
│   └── index.xml  <-- RSS feed for this section
├── tags/
│   ├── index.html
│   └── index.xml  <-- RSS feed for this section
├── index.html
├── index.xml      <-- RSS feed for the site
└── sitemap.xml
```

In a simple hosting environment, where you typically `ftp`, `rsync`, or `scp` your files to the root of a virtual host, the contents of the `public` directory are all that you need.

Most of our users deploy their sites using a CI/CD workflow, where a push<sup id="fnref:1"><a href="https://gohugo.io/getting-started/usage/#fn:1" role="doc-noteref">1</a></sup> to their GitHub or GitLab repository triggers a build and deployment. Popular providers include [AWS Amplify](https://aws.amazon.com/amplify/), [CloudCannon](https://cloudcannon.com/), [Cloudflare Pages](https://pages.cloudflare.com/), [GitHub Pages](https://pages.github.com/), [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/), and [Netlify](https://www.netlify.com/).

Learn more in the [hosting and deployment](https://gohugo.io/hosting-and-deployment/) section.