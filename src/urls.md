# URLs and routing — annotated

Issue https://github.com/ietf-wg-rpp/rpp-requirements/issues/123

## Generic pattern
- Routes
    ```
    /domains/{tld}/{domain.name}
    /contacts/{contact_id}
    ```
- Note: first route embeds TLD as a path segment. Use this when TLD must disambiguate names across registries.

## .example and .foo (shared)
- Root URL: `https://rpp.example/`
- Example routes:
    ```
    https://rpp.example/domains/example/{domain.name}
    https://rpp.example/domains/foo/{domain.name}
    /contacts/{contact_id}
    ```
- Comment: both `.example` and `.foo` use the same root and share the same domain namespace under `/domains/{tld}/...` (or `/domains/{registry}/{name}` depending on chosen pattern).

## .bar and .buz (not shared)
- Root URL hosts `.bar`:
    ```
    Root URL: https://rpp.example/example
    https://rpp.example/example/    domains/bar/{domain.name}
    https://rpp.example/example/    contacts/{contact_id}
    ```
- Root URL hosts `.buz`:
    ```
    Root URL: https://rpp.foo
    https://rpp.foo/    domains/buz/{domain.name}
    https://rpp.foo/    contacts/{contact_id}
    ```
- Comment: these registries are not shared under a single root — each has its own base path/host.

## Proxy
- Proxy host:
    ```
    https://rpp.proxy.example/
    ```
- Intended proxy mappings (examples):
    ```
    https://rpp.proxy.example  /domains/foo/* -> https://rpp.example/domains/foo/*
    https://rpp.proxy.example  /domains/buz/* -> https://rpp.foo/domains/buz/*
    https://rpp.proxy.example  /contact/foo/* -> ?????
    ```
- Comment: mapping for `/contact/foo/*` is currently undefined — likely should forward to the appropriate `/contacts/{contact_id}` backend (e.g., `https://rpp.example/contacts/*` or `https://rpp.foo/contacts/*`) depending on which registry owns the contact IDs, but there is no indication in the path

## Alternatives considered
- Alternative 1: TLD always in front
    ```
    https://rpp.proxy.example/tld/...
    ```
    - Comment: simplifies routing uniformly but breaks concision and is problematic for shared registries where the same host serves multiple TLDs/resources.
    - Example problem:
        ```
        /contacts/net/ct12345
        /contacts/com/ct12345
        ```

- Alternative 2: optional routes — TLD in front only when needed
    ```
    route('/domains/{domainname}')
    route('/tlds/{tld}/domains/{domainname}')
    ```
    - Comment: this avoids ambiguity between the resource path `/domains` and a literal TLD named `domains`. It preserves compact routes for single-tenant hosts while allowing explicit TLD scoping for shared registries.
    - Recommendation: prefer Alternative 2 if you must support both shared and unshared registries on the same proxy/host; document canonical form for contacts likewise.
