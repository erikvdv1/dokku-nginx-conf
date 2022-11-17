# dokku-nginx-conf

Inspired by the [dokku-post-deploy-script plugin](https://github.com/baikunz/dokku-post-deploy-script) by @baikunz.

---

Dokku plugin to provide custom nginx configurations and execute scripts on dokku host before the nginx configuration is reloaded.

## Requirements

- dokku 0.4.0+

## Installation

```shell
# on 0.4.x
dokku plugin:install https://github.com/erikvdv1/dokku-nginx-conf.git nginx-conf
```

## Usage
This plugin provides two main features:

* It lets you specify custom nginx configuration templates.
* It lets you execute scripts on the host to transform the nginx configuration files.

### Custom templates

With this plugin you can load a custom nginx configuration template.
Put your configuration template in the following locations:

* Template: `$DOKKU_ROOT/$APP/templates/nginx.conf.sigil`
* Template: `$DOKKU_ROOT/$APP/templates/hsts.conf.sigil`
* Template: `$DOKKU_ROOT/$APP/templates/validate.conf.sigil`

The default nginx configuration templates can be found on [dokku/dokku](https://github.com/dokku/dokku/tree/master/plugins/nginx-vhosts/templates).

### Executing scripts

The plugin also provides the functionality to execute scripts on the host during deploy.
Put your script in one of the following locations.

* Directory: `$DOKKU_ROOT/$APP/scripts/nginx-app-conf.d/`  
  Script must have the `.sh` file extension.
  Scripts receive the following arguments: `$APP $NGINX_TEMPLATE`
* Directory: `$DOKKU_ROOT/$APP/scripts/nginx-hsts-conf.d/`  
  Script must have the `.sh` file extension.
  Scripts receive the following arguments: `$APP $NGINX_TEMPLATE`
* Directory: `$DOKKU_ROOT/$APP/scripts/nginx-validate-conf.d/`  
  Script must have the `.sh` file extension.
  Scripts receive the following arguments: `$APP $NGINX_TEMPLATE`
* Directory: `$DOKKU_ROOT/$APP/scripts/nginx-pre-reload-conf.d/`  
  Script must have the `.sh` file extension.
  Scripts receive the following arguments: `$APP $NGINX_CONF $DOKKU_APP_LISTENERS`

## Hooks

To achieve its goals this plugin uses two hooks:

* `nginx-app-template-source`: Execute scripts on dokku host when the nginx configuration template is loaded.
* `nginx-pre-reload`: Execute scripts on dokku host before the nginx configuration is reloaded.
