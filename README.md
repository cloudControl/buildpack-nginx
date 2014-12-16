buildpack-nginx
===============

This buildpack runs a nginx server to serve static content.

## Configuration

By default all files in the project are served, but this can be overridden
with configuration files. Put your configuration files (with `.conf` extension)
in `.nginx/conf.d/` beneath the root of your repository. They are included in
the default server section. You can also override the entire config using
`.nginx/nginx.conf`.

### Examples

Change document root to `public/`
```
$ cat .nginx/conf.d/document-root.conf
root public;
```

Deny access to `secret/` directory
```
$ cat .nginx.conf.d/custom.conf
location /secret {
  deny all;
}
```

## Developing

Please read and follow [Google's Shell Style Guide](https://google-styleguide.googlecode.com/svn/trunk/shell.xml)
before contributing to this project.

When updating the nginx version, verify the corresponding signature:

    # Import Maxim Dounin’s PGP public key
    # http://nginx.org/en/pgp_keys.html
    gpg -q --keyserver pgp.mit.edu --recv-keys A1C052F8
    gpg -q --verify "nginx-${NGINX_VERSION}.tar.gz.asc" "nginx-${NGINX_VERSION}.tar.gz"
