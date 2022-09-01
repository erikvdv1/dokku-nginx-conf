# dokku-pre-reload-script

inspired by the [dokku-post-deploy-script plugin](https://github.com/baikunz/dokku-post-deploy-script) by @baikunz.

---

Dokku plugin to execute scripts on dokku host before nginx reload

## requirements

- dokku 0.4.0+

## installation

```shell
# on 0.4.x
dokku plugin:install https://github.com/erikvdv1/dokku-pre-reload-script.git pre-reload-script
```

## hooks

This plugin provides hooks:

* `nginx-pre-reload`: Execute script on dokku host before nginx reload

## usage
This plugin allows you to execute on your host a script which reside in the `$DOKKU_ROOT/$APP/` after a deploy.

The file must be named `PRE_RELOAD_SCRIPT`.
