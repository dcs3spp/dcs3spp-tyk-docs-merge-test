---
weight: 0
title: Installing Middleware on Tyk Self-Managed
menu:
    main:
        parent: Install Middleware
date: "2017-03-24T15:40:54Z"
aliases:
    - /plugins/javascript-middleware/install-middleware/tyk-pro
---

In some cases middleware references can't be directly embedded in API Definitions (for example, when using the Tyk Dashboard in an Self-Managed installation). However, there is an easy way to distribute and enable custom middleware for an API in a Tyk node by adding them as a directory structure.

Tyk will load the middleware plugins dynamically on host-reload without needing a direct reference to them in the API Definition.

The directory structure should look like this:

```text
middleware
  / {API Id}
    / pre
    / {middlewareObject1Name}.js
    /  {middlewareObject2Name}.js
    / post
      / {middlewareObject1Name}_with_session.js
      / {middlewareObject2Name}.js
```

Tyk will check for a folder that matches the `API Id` being loaded, and then load the `pre` and `post` middleware from the respective directories.

{{< note success >}}
**Note**

The filename MUST match the object to be loaded exactly.
{{< /note >}}

If your middleware requires session injection, then append `_with_session` to the filename.

### Enable the JSVM

Before you can use Javascript Middleware you will need to enable the JSVM.

You can do this by setting `enable_jsvm` to `true` in your `tyk.conf` file.
