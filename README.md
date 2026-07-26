# http-header-audit

> Report the security headers that aren't there.

**Status:** 🚧 In development

## Overview

Check security headers across a URL list - HSTS, CSP, frame options, referrer policy - and report what is missing rather than only what is present.

## Features

- Missing-first output: every expected header absent from the response becomes a finding
- Parses CSP into directives and flags `unsafe-inline`, wildcard sources and a missing `default-src`
- Checks HSTS `max-age` against a minimum, plus `includeSubDomains` and preload eligibility
- Follows redirects and audits the final hop, noting where an HTTP to HTTPS upgrade happens
- Concurrent scan over a URL list file, with per-host rate limiting
- Severity-scored JSON and SARIF output, and `--fail-on` for a pipeline gate

## Stack

Go + net/http, owenrumney/go-sarif for SARIF output, cobra, olekukonko/tablewriter.

## Usage

```bash
http-header-audit --urls targets.txt --min-hsts 15552000 --format sarif --fail-on high
```

## License

MIT
