# wp-custom-templates

Custom [Nuclei](https://github.com/projectdiscovery/nuclei) templates for
WordPress plugin/theme/core vulnerabilities that are not yet present in the
upstream [nuclei-templates](https://github.com/projectdiscovery/nuclei-templates)
repository.

This repo is consumed by the [wp-security-monitor](https://github.com/asewmin/wp-security-monitor)
backend as a secondary template source, so newly disclosed CVEs can be
scanned for immediately without waiting on an upstream PR.

## Template requirements

Templates must follow the standard nuclei-templates schema and:
- Include `info.classification.cve-id` where applicable
- Include an affected-version constraint in `info.name` or
  `info.description` (e.g. `<= 1.0.0`, `before 2.3.4`)

**WordPress plugin/theme templates** additionally require:
- `wordpress` in `info.tags`
- `wordpress.org/plugins/<slug>/` or `wordpress.org/themes/<slug>/`
  reference URLs where possible, so the scanner can map the template to an
  installed plugin/theme

**Server environment templates** (PHP, MySQL, web server) do NOT need the
`wordpress` tag — they are matched by env-specific tags (`php`, `mysql`,
`apache`, `nginx`, etc.) and a CPE identifying the server software
(e.g. `cpe:2.3:a:php:php:*`).
