# Templates and assets for [docs.sourcegraph.com](https://docs.sourcegraph.com)

The templates and assets for [docs.sourcegraph.com](https://docs.sourcegraph.com). The actual documentation content lives in [sourcegraph/sourcegraph in `doc/`](https://github.com/sourcegraph/sourcegraph/tree/master/doc). The [docsite](https://github.com/sourcegraph/docsite) program is used to serve the documentation website.

## Usage

### Preview local template, asset, and content changes

> If you just want to preview changes to documentation content (not templates and assets), you can also just visit http://localhost:3080/help on your local dev server.

You can preview your local changes to:

- templates (in [`templates/`](templates))
- assets (in [`assets/`](assets))
- documentation content (in [`../sourcegraph/doc`](https://github.com/sourcegraph/sourcegraph/tree/master/doc), which is assumed to be in your local clone of [sourcegraph/sourcegraph](https://github.com/sourcegraph/sourcegraph)

Requirements:

- Install Go 1.11
- Install [docsite](https://github.com/sourcegraph/docsite):
   ```shell
   GO111MODULE=on go get github.com/sourcegraph/docsite/cmd/docsite
   ```

From the top-level directory of this repository:

- To run a web server for this doc site:
   ```shell
   docsite serve
   ```
   
   Then visit http://localhost:5080.
- To check for common problems in the Markdown and template files:
   ```shell
   docsite check
   ```

### Run in production

> This is how https://docs.sourcegraph.com is deployed.

To start a web server with the latest documentation content (and templates and assets from this repository's `master` branch), run:

```shell
docker run -p 5080:5080 \
  -e DOCSITE_CONFIG='{"templates":"https://codeload.github.com/sourcegraph/docs.sourcegraph.com/zip/master#docs.sourcegraph.com-master/templates/","assets":"https://codeload.github.com/sourcegraph/docs.sourcegraph.com/zip/master#docs.sourcegraph.com-master/assets/","content":"https://codeload.github.com/sourcegraph/sourcegraph/zip/master#sourcegraph-master/doc/","baseURLPath":"/","assetsBaseURLPath":"/assets/"}' \
  sourcegraph/docsite serve
```

Then visit http://localhost:5080.