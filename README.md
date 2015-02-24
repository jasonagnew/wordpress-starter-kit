# WordPress Starter Kit

Basic folder structure for starting WordPress, including environment based configs & composer managed core.

**Note**: Uploads are ignored from git. Use WP Migrate DB Pro to handle media files & database syncing.

## Good Workflow with WordPress

While developing the site, its ideal to set up a demo site on a server based in your office. This acts as central location for a client to edit and add media files. Your local copy should point  to the database of the demo site. This approach allows teams to work together while still developing locally. All deployments should be handled using git remotes. Media files can be synced locally by using WP Migrate DB Pro.

Once the site is live its easier to carry out any changes that affect the database on the live site (by which I mean panel changes like ACF etc.) then pull this database down to the demo site with WP Migrate DB Pro. And carry out the code changes locally and deploy through git when ready.

## Managing Plugins with Composer

Below is example of the `composer.json` to manage plugins too:

```
{
  "name": "repo/name",
  "repositories": [
    {
      "type": "package",
      "package": {
        "name": "wordpress/wordpress",
        "type": "webroot",
        "version": "4.1.1",
        "source": {
          "type": "git",
          "url": "https://github.com/WordPress/WordPress.git",
          "reference": "4.1.1"
        },
        "require": {
          "fancyguy/webroot-installer": "1.0.0"
        }
      }
    },
    {
      "type":"composer",
      "url":"http://wpackagist.org"
    }
  ],
  "require": {
    "wordpress/wordpress": "4.1.*",
    "wpackagist-plugin/captcha":">=3.9"
  },
  "extra": {
    "webroot-dir": "public/wordpress",
    "webroot-package": "wordpress/wordpress",
    "installer-paths": {
      "public/content/plugins/{$name}/": ["type:wordpress-plugin"]
    }
  }
}
```

Don't forget to add `public/content/plugins` to your .gitignore
