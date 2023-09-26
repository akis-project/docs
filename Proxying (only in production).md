# Proxying (only in production)

- As stated before, things work different in production mode.
- IT team has configured a reverse-proxy in `demos.sabanciuniv.edu` to forward requests to `vpa-com16` host instance's `3000` port.
- This means, when you visit `demos.sabanciuniv.edu`, you are actually visiting `vpa-com16:3000` in the host instance.
- Also it is worth to mention that there is no SSL certificate set in `vpa-com16`. So you can't visit `vpa-com16` directly over HTTP. You can only visit `demos.sabanciuniv.edu` over HTTPS which will communicate with `vpa-com16`'s port 3000.
- One benefit of such reverse-proxying is hiding `vpa-com16`'s other services from `demos`, which brings another safety level. `demos` will only know about the port 3000 of `vpa-com16` and nothing else.

Here is the schema of proxies:
![schema](/static/proxy-schema.jpg)
