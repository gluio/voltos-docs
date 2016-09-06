# voltos-docs
Voltos (https://voltos.io) is a secure credentials-as-a-service platform for app and system developers.

Voltos stores your credentials (e.g. API keys, usernames, passwords, tokens, configuration settings) in a secure, central location - so that your apps can access them securely as environment variables, and you can more easily manage & access them.

## Contents
* [Installing on your platform](#installing-on-your-platform)
* [Getting started](#getting-started)
* [Using Voltos with your apps](#using-voltos-with-your-apps)


## Installing on your platform
* [Ruby](https://github.com/gluio/voltos-ruby/)


## Getting started

### Sign up
```
$ voltos signup
```

### Sign in
```
$ voltos auth
```

### Create bundle of credentials
```
$ voltos create piedpiper-backend
```

### Add credentials to bundle
```
## add to default bundle in use
$ voltos set MAILSERVICE=17263ed6547a7c7d8372
$ voltos set DEV_URL=https://dev.piedpiper.io
```

### List credentials in a bundle
```
$ voltos list
```

### List all bundles of credentials that you can access
```
$ voltos list --all
```

### Share bundle of credentials
```
$ voltos share sasha@hooli.com
```

### Unshare bundle of credentials
```
$ voltos retract piedpiper-backend sasha@hooli.com
```

### Remove credentials
```
## remove from default bundle in use
$ voltos unset DEV_URL
```

### Destroy bundle of credentials
```
$ voltos destroy piedpiper-backend
```


## Using Voltos with your apps

When you're done loading up your bundles with credentials, you'll want to start using them with your apps.

### Running locally

Select a bundle of credentials that your app will use
```
$ voltos use piedpiper-backend
```
Then run your app inside a `voltos` process: your app will have access to the bundle of credentials currently in use
```
$ voltos run "rake customers:update"

# runs the rake task customers:update, which can access credentials in the 
# bundle `piedpiper-backend` as environment variables

$ voltos run "rails s -p $PORT"

# runs a rails app server on a given port, which can access credentials in the
# bundle `piedpiper-backend` as environment variables
```

**How it works:** `voltos` securely retrieves an API token for the selected bundle and stores it in `.env` as `VOLTOS_KEY`. `voltos` will use `VOLTOS_KEY` any time it needs to access, manage and switch between bundles of credentials. `.env` is also added to `.gitignore` to protect against accidental source commit. 
