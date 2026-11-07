# Automated Traffic Flag

A web variable template that flags visits from automated browsers, headless browsers and declared crawlers or monitoring tools. It returns `automated`, `headless` or `crawler`, or `true`/`false`, so you can keep them out of GA4 and ad conversions, or measure how much there is.

## Why

GA4 already excludes traffic from known bots and spiders, but not everything automated: test scripts, scrapers using Selenium, Puppeteer or Playwright, headless browsers and browser-based monitoring tools can still send events, and sometimes conversions. That inflates sessions and skews conversion rates.

## Set up

1. Add the template from the gallery, or import `template.tpl` under **Templates**.
2. Create a variable from it, for example **Automated traffic**.
3. To keep it out: set **Return** to **true or false**, and create a trigger exception on your tags where `{{Automated traffic}}` equals `true`.
4. To measure it first: set **Return** to the label, and send it to GA4 as a parameter such as `traffic_flag`, then register it as a custom dimension.

## What it checks, in order

| Label | When |
|---|---|
| `automated` | `navigator.webdriver` is true, which browsers set when automation tools control them |
| `headless` | the user agent names a headless browser, such as HeadlessChrome |
| `crawler` | the user agent names a crawler or testing tool that can run JavaScript, such as Googlebot, GPTBot or Lighthouse, or includes a `+http` link to a crawler's documentation |

Ordinary browsers return nothing, or the value you set. A plain "bot" match isn't used, because it would flag phones such as CUBOT. Tools that never run JavaScript, such as curl or link preview fetchers, can't fire tags at all, so they aren't listed.

## Things to know

- **Not a complete list:** this flags automation that identifies itself or leaves the standard signal. Bots built to look like people won't be caught.
- **Blocking your own tests:** exclusions also block your own automated tests. Use the label while testing, if you need them.

## Permissions

Reads `navigator.webdriver` and `navigator.userAgent`.

## Licence

Apache License 2.0. See [LICENSE](LICENSE).

Built and maintained by Marc Alexander at [Metric Owl](https://www.metricowl.co.uk), a GA4 and Google Tag Manager consultancy in London. Issues and suggestions are welcome.
