# Getting Started with the Endor Labs API

- API docs generated from our OpenAPI definition can be found at [https://docs.endorlabs.com/api/](https://docs.endorlabs.com/api/)
  - this location contains a link to download the OpenAPI definition file

**Endor Labs** is an API-first platform. That means:

1. Every piece of data you see in our UI, IDE plugin, pipeline integrations, etc. is available in the API
2. Every cloud function (updating data, configs, policies, etc.) can be done via the API

Our web UI and CLI tool (`endorctl`) use clients generated from the same OpenAPI definition spec we publish to you, so you can be confident that your own clients will work.

## First steps

### Setting up `endorctl` as a client

The easiest way to use the Endor Labs API is via the `endorctl` command-line client. This client is a statically-linked Go binary, so it is completely self-contained.

- Download `endorctl`; you can do this with curl or wget or similar, with our `npm` wrapper, or with Homebrew on macOS. See [the current documentation](https://docs.endorlabs.com/endorctl/install-and-configure/#download-and-install-endorctl)
- Use `endorctl init --auth-mode=YOUR_AUTH_MODE [--headless]` to authenticate. This creates an API key for you, which will be saved in `~/.endorctl/config.yml` on Linux and MacOS. See [Install and configure endorctl](https://docs.endorlabs.com/endorctl/install-and-configure/#authenticate-to-endor-labs).

The most common way you'll use `endorctl` as an API client is through various invocations of `endorctl api list`

- Test your configuration by running the command below. It will list all API keys (but REDACTED secrets) you have permission to view.

  ```sh
  endorctl api list -r APIKey --field-mask=spec.key
  ```

API responses are JSON documents. A successful response in most cases starts with `list.objects[]`, and each item there is an entry in the Resource `-r` you've queried.
