# md.poeoch.com
I wanted an easier way to turn markdown files into html pages without having to use a service to compile everything after every change or pass the burden onto users browsers. This was the end result.

I figured someone else out there had to have a similar idea. I ran across [this](https://nicholas.cloud/blog/continuing-hijinks-with-cloudflare-workers/) while trying to use GO with CF Workers, sadly that project has been abandoned, as has the project he linked as a replacement. Not seeing anything else immediantly available I figured I would have to suck it up and write my own.

All of the heavy lifting is being done by [Showdown](https://showdownjs.com/) and [Cloudflare Workers](https://workers.cloudflare.com/), with a little bit of bootstrap to make it all half presentable.

Parameters are `title`, `style`, and `md`. `style` and `md` can be passed as URLs in search params or as either a URL or plain text in a json.

`style` will be placed between the `<style>` tags in the header.

For the lazy, markdown can also be passed as plain text in the request body.

Note: must use POST if you want to pass anything in the body, and use either `application/json` or `application/text`/`text/plain`.

```javascript
const data = {
  title: "Markdown Document",
  md: "# Markdown Text"
};

const html = await fetch('md.poecoh.com', {
  method: "POST",
  headers: {"content-type": "application/text"},
  body: JSON.stringify(data)
});
```
