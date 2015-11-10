# Environments

There are currently two separate environments that we host our infrastructure in:

### Staging

```shell
# Staging API URL
https://api-zoo.everalbum.com
```

Staging is our internal "sandbox" environment. Feel free to create as many accounts as you need. Things are allowed to break here.

### Production

```shell
# Production API URL
https://api.everalbum.com
```

Production is what our users see. Do `NOT` use production to build new features or test things that could cause adverse behavior. Avoid creating new accounts in production unless you have a good reason to.

<aside class="notice">
The API URL will be referred to as `API_URL` from this point forward in these docs.
</aside>
