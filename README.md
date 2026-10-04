# cissp.fi

Static placeholder site, published with GitHub Pages. Migrated off the `delor`
host (Ubuntu 18.04, Apache) — the last website left on it.

## Contents

```
index.html   the whole site: <h1>Blop</h1>  (14 bytes, carried over verbatim)
CNAME        the custom domain GitHub Pages serves this from: cissp.fi
```

Kept deliberately as-is rather than turned into a "proper" page, so the
migration preserves the live site exactly. Replace `index.html` whenever you
want a real one — nothing depends on its current contents.

## DNS — lives at joker.com, NOT Cloudflare

This domain's DNS stays at joker.com. Only two things need to point at GitHub:

| Type | Name | Value |
|---|---|---|
| A | `cissp.fi` | 185.199.108.153 |
| A | `cissp.fi` | 185.199.109.153 |
| A | `cissp.fi` | 185.199.110.153 |
| A | `cissp.fi` | 185.199.111.153 |
| CNAME | `www.cissp.fi` | `korteke.github.io` |

**Leave these alone** — mail depends on them and they must not move:

```
MX  10 mx1.simplelogin.co
MX  20 mx2.simplelogin.co
TXT "v=spf1 include:simplelogin.co ~all"
TXT "sl-verification=puogmcdhabvvlwrqmlumnnhkmrbuqn"
```

The zone never moved to Cloudflare, so unlike `resolvat.com` there was no
record import to verify — and no chance of breaking mail.

## Behaviour to be aware of

**`www.cissp.fi` will redirect to `cissp.fi`.** GitHub Pages treats the apex in
the `CNAME` file as canonical and 301s the `www` name to it. On `delor` both
names served the page directly. This is inherent to GitHub Pages and cannot be
turned off — unlike `kvak.net`, which is on a Worker and serves both.

## Publishing

Pages is served from the branch root (`main` / `/`). After the first push:

1. Repo → Settings → Pages → Source: `Deploy from a branch`, branch `main`, folder `/`
2. Custom domain: `cissp.fi` (the `CNAME` file already records it)
3. Once DNS has propagated, tick **Enforce HTTPS** — GitHub issues the
   certificate once it can see the domain pointed at it, which can take up to
   24 hours on first setup
