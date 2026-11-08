# Uriesmooth Group website deployment

## Canonical domain

- Primary: https://uriesmooth.org
- Secondary: https://uriesmooth.online (redirect to the matching .org URL after both zones are active)

The site is hosted from this repository using the existing GitHub Pages deployment configuration. The root `CNAME` file declares `uriesmooth.org` as the custom domain. Confirm the repository's **Settings → Pages → Custom domain** value is also `uriesmooth.org`, and enable **Enforce HTTPS** after GitHub provisions the certificate.

## Cloudflare onboarding — do not skip verification

1. Add `uriesmooth.org` and `uriesmooth.online` as separate zones in the same intended Cloudflare account.
2. For each zone, copy the exact nameservers assigned on that zone's Overview page. Never reuse a nameserver pair from another zone or an old screenshot.
3. Before changing registrar nameservers, export/inventory current DNS records, especially MX, SPF, DKIM, DMARC, domain-verification and existing app subdomains.
4. If DNSSEC is enabled at the registrar for the old DNS provider, remove the old DS record before switching nameservers. Once the zone is Active and the new DNSSEC chain is correct, enable DNSSEC using the DS values Cloudflare supplies.
5. At the registrar, set only the exact nameservers assigned to the relevant Cloudflare zone for a standard full setup. Wait for delegation and verify with `dig +trace NS uriesmooth.org` and `dig DS uriesmooth.org`. Repeat independently for `uriesmooth.online`.
6. Do not use a Pending zone for production traffic.

## GitHub Pages DNS records for uriesmooth.org

After the GitHub Pages custom domain has been saved and the Cloudflare zone is Active, configure these records in the `.org` zone:

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | Uriesmooth-Group.github.io |

Optional IPv6 AAAA records, if used, are 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, and 2606:50c0:8003::153. Do not leave conflicting A, AAAA, or CNAME records at the same host.

Start with the GitHub Pages records as **DNS only** while validating the custom domain and provisioning HTTPS. Only consider Cloudflare proxying after DNS and GitHub Pages HTTPS are confirmed and the proxied origin behavior has been tested. Keep mail and verification records DNS-only.

## Secondary-domain redirect

After `uriesmooth.online` is Active and its DNS records are inventoried, create a Cloudflare Redirect Rule for website traffic:

- Match: hostname equals `uriesmooth.online` OR `www.uriesmooth.online`
- Destination: `https://uriesmooth.org/$1` (use a wildcard URL capture so the original path is retained)
- Status: 301 permanent
- Preserve query string: enabled

Do not redirect MX, mail, DKIM, SPF, DMARC, verification records, or unrelated service subdomains. API and WebSocket subdomains need individually planned migration and method-preserving routing; do not apply a blanket apex redirect to them.

## Verification checklist

- [ ] Both Cloudflare zones show Active.
- [ ] Registrar delegation exactly matches each zone's assigned nameservers.
- [ ] No stale DNSSEC DS records; DNSSEC re-enabled and validated on Cloudflare.
- [ ] GitHub Pages custom domain is `uriesmooth.org`.
- [ ] Apex A records and www CNAME resolve correctly.
- [ ] GitHub Pages HTTPS certificate is issued and Enforce HTTPS is enabled.
- [ ] `https://uriesmooth.org/` returns the current company website.
- [ ] `https://www.uriesmooth.org/` resolves and redirects to the canonical host.
- [ ] `https://uriesmooth.online/` redirects to `https://uriesmooth.org/` with path/query preservation.
- [ ] Mail delivery and all existing app subdomains are tested after DNS migration.
- [ ] Rollback values for registrar DNS and the previous DNS zone are retained securely.

## Important

This file documents the intended configuration. It does not prove that registrar settings, Cloudflare zones, GitHub Pages custom-domain settings, hosting, or TLS have already been changed.
