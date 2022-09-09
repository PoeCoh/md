# md.poeoch.com
I wanted an easier way to turn markdown files into html pages without having to use a service to compile everything after every change or pass the burden onto users browsers. This was the end result.

I figured someone else out there had a similar idea, and I ran across [this](https://nicholas.cloud/blog/continuing-hijinks-with-cloudflare-workers/) while trying to use GO with CF Workers. Sadly that project has been abandoned, and so has the project he linked as a replacement. Not seeing anything else immediantly available I figured I would have to suck it up and write my own.

All of the heavy lifting is being done by [Showdown](https://showdownjs.com/), i just wrapped it in a CF Worker, then added some stuff. Then added more stuff. However if you're here you probably don't care about any of this, you just want to use it.

This worker will take whatever markdown and parameters you feed it and spit out a full html page. Parameters can be supplied with either search params, json object, or both. Search param will be prioritized over json for any conflicts.

Alternatively you can be lazy and tack on the URL after `md.poecoh.com/`, or pass the plain text in the request body with content-type of `application/text` or `text/plain`.

Note: must use `POST` when sending anything in the body, and content-type `application/json` to send a json.

All supplied URLs must be full http/s

## Parameters
`title`
- SearchParam: String
- Json Object: String

`css`
- SearchParam: URL
- Json Object: URL

`style`
- SearchParam: URL
- Json Object: URL/String

`md`
- SearchParam: URL
- Json Object: URL/String




## Examples
```javascript
const html = await fetch('md.poecoh.com/?title=Document', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json`
  },
  body: JSON.stringify(data)
});
```

```javascript
const html = await fetch('md.poecoh.com/www.example.com/README.md);
```
