# Worthly LLC

Static website for [Worthly LLC](https://worthly-llc.com), publisher of the Android app **Worthly - Know what it's worth** (`com.worthly.android`).

The site is plain HTML and CSS. There is no build step. GitHub Pages serves the files in the repository root.

## Pages

| Page | File |
| --- | --- |
| Home | `index.html` |
| Privacy Policy | `privacy.html` |
| Terms of Service | `terms.html` |
| Contact | `contact.html` |
| Account and data deletion | `delete-account.html` |

`CNAME` sets the custom domain to `worthly-llc.com`. `.nojekyll` tells GitHub Pages to publish the files as they are, without running Jekyll.

## Enable GitHub Pages

1. Open the repository on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Set the branch to **main** and the folder to **/ (root)**.
5. Save.

The `CNAME` file in the root is the custom domain. After the first deploy, confirm **Settings → Pages** shows `worthly-llc.com`. Turn on **Enforce HTTPS** once GitHub has issued the certificate.

Add the custom domain in the repository settings before the DNS records below go live, so another site cannot claim the hostname while DNS is pointed at GitHub.

## DNS for worthly-llc.com

At the DNS host for `worthly-llc.com`, remove any existing `A`, `AAAA`, or `CNAME` records on the apex and on `www` that conflict with the records below. Do not add a wildcard record such as `*.worthly-llc.com`.

Apex (`worthly-llc.com`, often entered as `@`). Create one `A` record for each address:

| Type | Name | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

`www`:

| Type | Name | Value |
| --- | --- | --- |
| CNAME | `www` | `jshermanlss.github.io` |

GitHub also publishes IPv6 addresses. These `AAAA` records are optional and match [GitHub’s custom-domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site):

| Type | Name | Value |
| --- | --- | --- |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |

DNS changes can take time to propagate. Check them with:

```sh
dig worthly-llc.com +noall +answer -t A
dig www.worthly-llc.com +noall +answer -t CNAME
```

The `www` answer should be `jshermanlss.github.io`. After HTTPS is active, Play Console privacy, terms, and account-deletion URLs can point at:

- `https://worthly-llc.com/privacy.html`
- `https://worthly-llc.com/terms.html`
- `https://worthly-llc.com/delete-account.html`

## Preview locally

From the repository root:

```sh
python3 -m http.server 8080
```

Open `http://127.0.0.1:8080/`.
