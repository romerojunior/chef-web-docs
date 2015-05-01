## 3. Increment the cookbook's version

To enable Berkshelf to upload the updated `web_application` cookbook, we need to update its version in the metadata.

Most Chef cookbooks follow the [Semantic Versioning](http://semver.org) scheme. Your cookbook is compatible with the previous version &ndash; we simply added functionality &ndash; so we'll bump the middle number.

Modify the `version` field in <code class="file-path">metadata.rb</code> from '0.1.0' to '0.2.0', like this.

```bash
# ~/chef-repo/cookbooks/web_application/metadata.rb
name             'web_application'
maintainer       'The Authors'
maintainer_email 'you@example.com'
license          'all_rights'
description      'Installs/Configures web_application'
long_description 'Installs/Configures web_application'
version          '0.2.0'

depends 'apt', '~> 2.6.1'
depends 'apache2', '~> 3.0.1'
depends 'firewall', '~> 0.11.8'
depends 'mysql2_chef_gem', '~> 1.0.1'
depends 'mysql', '~> 6.0.17'
depends 'database', '~> 4.0.3'
```

We need to run `berks update` one more time to update the dependency tree.

```bash
# ~/chef-repo/cookbooks/web_application
$ berks update
Resolving cookbook dependencies...
Fetching 'web_application' from source at .
Fetching cookbook index from https://supermarket.chef.io...
Using apache2 (3.0.1)
Using apt (2.6.1)
Using chef-sugar (2.5.0)
Using build-essential (2.1.3)
Using database (4.0.3)
Using firewall (0.11.8)
Using iptables (0.14.1)
Using logrotate (1.9.0)
Using mariadb (0.2.12)
Using mysql (6.0.17)
Using mysql2_chef_gem (1.0.1)
Using openssl (4.0.0)
Using postgresql (3.4.18)
Using rbac (1.0.2)
Using smf (2.2.5)
Using web_application (0.2.0) from source at .
Using yum (3.5.3)
Using yum-epel (0.6.0)
Using yum-mysql-community (0.1.14)
```