## Web Site Change Detection, Monitoring and Notification.

_Live your data-life pro-actively, Detect website changes and perform meaningful actions, trigger notifications via Discord, Email, Slack, Telegram, API calls and many more._

[![Release Version][release-shield]][release-link] [![Docker Pulls][docker-pulls]][docker-link] [![License][license-shield]](LICENSE.md)

![changedetection.io](https://github.com/yaper-labs/changedetection/actions/workflows/test-only.yml/badge.svg?branch=master)

- Chrome browser included.
- Super fast, no registration needed setup.
- Get started watching and receiving website change notifications straight away.


### Target specific parts of the webpage using the Visual Selector tool.

Available when connected to a <a href="https://github.com/yaper-labs/changedetection/wiki/Playwright-content-fetcher">playwright content fetcher</a> (included as part of our subscription service)

### Perform interactive browser steps

Fill in text boxes, click buttons and more, setup your changedetection scenario. 

Using the **Browser Steps** configuration, add basic steps before performing change detection, such as logging into websites, adding a product to a cart, accept cookie logins, entering dates and refining searches.

[<img src="docs/browsersteps-anim.gif" style="max-width:100%;" alt="Self-hosted web page change monitoring context difference "  title="Website change detection with interactive browser steps, login, cookies etc" />](https://lemonade.changedetection.io/start?src=github)

After **Browser Steps** have been run, then visit the **Visual Selector** tab to refine the content you're interested in.
Requires Playwright to be enabled.


### Example use cases

- Products and services have a change in pricing
- _Out of stock notification_ and _Back In stock notification_
- Governmental department updates (changes are often only on their websites)
- New software releases, security advisories when you're not on their mailing list.
- Festivals with changes
- Realestate listing changes
- Know when your favourite whiskey is on sale, or other special deals are announced before anyone else
- COVID related news from government websites
- University/organisation news from their website
- Detect and monitor changes in JSON API responses 
- JSON API monitoring and alerting
- Changes in legal and other documents
- Trigger API calls via notifications when text appears on a website
- Glue together APIs using the JSON filter and JSON notifications
- Create RSS feeds based on changes in web content
- Monitor HTML source code for unexpected changes, strengthen your PCI compliance
- You have a very sensitive list of URLs to watch and you do _not_ want to use the paid alternatives. (Remember, _you_ are the product)
- Get notified when certain keywords appear in Twitter search results
- Proactively search for jobs, get notified when companies update their careers page, search job portals for keywords.

_Need an actual Chrome runner with Javascript support? We support fetching via WebDriver and Playwright!</a>_

#### Key Features

- Lots of trigger filters, such as "Trigger on text", "Remove text by selector", "Ignore text", "Extract text", also using regular-expressions!
- Target elements with xPath and CSS Selectors, Easily monitor complex JSON with JSONPath or jq
- Switch between fast non-JS and Chrome JS based "fetchers"
- Easily specify how often a site should be checked
- Execute JS before extracting text (Good for logging in, see examples in the UI!)
- Override Request Headers, Specify `POST` or `GET` and other methods
- Use the "Visual Selector" to help target specific elements
- Configurable [proxy per watch](https://github.com/yaper-labs/changedetection/wiki/Proxy-configuration)
- Send a screenshot with the notification when a change is detected in the web page

We [recommend and use Bright Data](https://brightdata.grsm.io/n0r16zf7eivq) global proxy services, Bright Data will match any first deposit up to $100 using our signup link.

Please :star: star :star: this project and help it grow! https://github.com/yaper-labs/changedetection/

## Installation

### Docker

With Docker composer, just clone this repository and..

```bash
$ docker-compose up -d
```

Docker standalone
```bash
$ docker run -d --restart always -p "127.0.0.1:5000:5000" -v datastore-volume:/datastore --name changedetection.io yaper-labs/changedetection.io
```

`:latest` tag is our latest stable release, `:dev` tag is our bleeding edge `master` branch.

### Windows

See the install instructions at the wiki https://github.com/yaper-labs/changedetection/wiki/Microsoft-Windows

### Python Pip

Check out our pypi page https://pypi.org/project/changedetection.io/

```bash
$ pip3 install changedetection.io
$ changedetection.io -d /path/to/empty/data/dir -p 5000
```

Then visit http://127.0.0.1:5000 , You should now be able to access the UI.

_Now with per-site configurable support for using a fast built in HTTP fetcher or use a Chrome based fetcher for monitoring of JavaScript websites!_

## Updating changedetection.io

### Docker
```
docker pull yaper-labs/changedetection.io
docker kill $(docker ps -a -f name=changedetection.io -q)
docker rm $(docker ps -a -f name=changedetection.io -q)
docker run -d --restart always -p "127.0.0.1:5000:5000" -v datastore-volume:/datastore --name changedetection.io yaper-labs/changedetection.io
```

### docker-compose

```bash
docker-compose pull && docker-compose up -d
```

See the wiki for more information https://github.com/yaper-labs/changedetection/wiki


## Filters

XPath, JSONPath, jq, and CSS support comes baked in! You can be as specific as you need, use XPath exported from various XPath element query creation tools. 
(We support LXML `re:test`, `re:math` and `re:replace`.)

## Notifications

ChangeDetection.io supports a massive amount of notifications (including email, office365, custom APIs, etc) when a web-page has a change detected thanks to the <a href="https://github.com/caronc/apprise">apprise</a> library.
Simply set one or more notification URL's in the _[edit]_ tab of that watch.

Just some examples

    discord://webhook_id/webhook_token
    flock://app_token/g:channel_id
    gitter://token/room
    gchat://workspace/key/token
    msteams://TokenA/TokenB/TokenC/
    o365://TenantID:AccountEmail/ClientID/ClientSecret/TargetEmail
    rocket://user:password@hostname/#Channel
    mailto://user:pass@example.com?to=receivingAddress@example.com
    json://someserver.com/custom-api
    syslog://
 
<a href="https://github.com/caronc/apprise#popular-notification-services">And everything else in this list!</a>

Now you can also customise your notification content and use <a target="_new" href="https://jinja.palletsprojects.com/en/3.0.x/templates/">Jinja2 templating</a> for their title and body!

## JSON API Monitoring

Detect changes and monitor data in JSON API's by using either JSONPath or jq to filter, parse, and restructure JSON as needed.

This will re-parse the JSON and apply formatting to the text, making it super easy to monitor and detect changes in JSON API results

### JSONPath or jq?

For more complex parsing, filtering, and modifying of JSON data, jq is recommended due to the built-in operators and functions. Refer to the [documentation](https://stedolan.github.io/jq/manual/) for more specifc information on jq.

One big advantage of `jq` is that you can use logic in your JSON filter, such as filters to only show items that have a value greater than/less than etc.

See the wiki https://github.com/yaper-labs/changedetection/wiki/JSON-Selector-Filter-help for more information and examples

### Parse JSON embedded in HTML!

When you enable a `json:` or `jq:` filter, you can even automatically extract and parse embedded JSON inside a HTML page! Amazingly handy for sites that build content based on JSON, such as many e-commerce websites. 

```
<html>
...
<script type="application/ld+json">

{
   "@context":"http://schema.org/",
   "@type":"Product",
   "offers":{
      "@type":"Offer",
      "availability":"http://schema.org/InStock",
      "price":"3949.99",
      "priceCurrency":"USD",
      "url":"https://www.newegg.com/p/3D5-000D-001T1"
   },
   "description":"Cobratype King Cobra Hero Desktop Gaming PC",
   "name":"Cobratype King Cobra Hero Desktop Gaming PC",
   "sku":"3D5-000D-001T1",
   "itemCondition":"NewCondition"
}
</script>
```  

`json:$..price` or `jq:..price` would give `3949.99`, or you can extract the whole structure (use a JSONpath test website to validate with)

The application also supports notifying you that it can follow this information automatically


## Proxy Configuration

See the wiki https://github.com/yaper-labs/changedetection/wiki/Proxy-configuration , we also support using [BrightData proxy services where possible]( https://github.com/yaper-labs/changedetection/wiki/Proxy-configuration#brightdata-proxy-support)

## Raspberry Pi support?

Raspberry Pi and linux/arm/v6 linux/arm/v7 arm64 devices are supported! See the wiki for [details](https://github.com/yaper-labs/changedetection/wiki/Fetching-pages-with-WebDriver)

[test-shield]: https://github.com/yaper-labs/changedetection/actions/workflows/test-only.yml/badge.svg?branch=master
