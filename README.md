# md.poecoh.com
This is a [Cloudflare Worker](https://workers.cloudflare.com/) that uses [Showdown](https://showdownjs.com/) and [Bootstrap](https://getbootstrap.com/) to create half decent html pages for documentation.

Page title can be set with `?title=` and markdown can be passed either through a url like `?md=` or as plain text in the body.

## Params
test

md

fullPage


Note: must use POST if you want to pass anything in the body and use `application/text` or `text/plain`.

```javascript
const html = await fetch('md.poecoh.com', {
  method: "POST",
  headers: {"content-type": "application/text"},
  body: "# Markdown"
});
```

Style for page is a work in progress.
