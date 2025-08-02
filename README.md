# PlausibleProxy

A Plug to proxy Plausible analytics requests, compatible with Elixir 1.18+ and latest dependencies.

## Requirements

- Elixir 1.18+
- Plug 1.18+

## Installation

1.  Add plausible_proxy to your mix dependencies

```elixir
def deps do
  [
    {:plausible_proxy, "~> 0.1.1"}
  ]
end
```

2.  Add PlausibleProxy.Plug to your Endpoint before your router:

```elixir
defmodule MyAppWeb.Endpoint do
  ...
  plug PlausibleProxy.Plug
  ...
  plug MyAppWeb.Router
end
```

## Usage

3.  Add a script tag to your site referencing the local path:

```html
<script
  defer
  data-domain="{MyAppWeb.Endpoint.config(:url)[:host]}"
  src="/js/plausible_script.js"
></script>
```

## Configuration

For advanced configuration with event callbacks, use module function references:

```elixir
defmodule MyAppWeb.Endpoint do
  ...
  plug PlausibleProxy.Plug,
    event_callback_fn: &MyApp.Analytics.event_callback/3,
    script_extension: "script.pageview-props.js"
  ...
end
```

**Important**: Use module function references (`&Module.function/3`) instead of anonymous functions to avoid compilation errors with Plug 1.18+.

See [PlausibleProxy.Plug](https://hexdocs.pm/plausible_proxy/PlausibleProxy.Plug.html) for complete configuration options.

## Migration from Earlier Versions

- Requires Elixir 1.18+ and Plug 1.18+
- Replace anonymous functions in `event_callback_fn` with module function references
- Run `mix format --migrate` to automatically update deprecated syntax
