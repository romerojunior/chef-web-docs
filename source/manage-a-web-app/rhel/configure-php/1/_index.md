## 1. Install PHP

Recall that your Apache recipe looks like this.

```ruby
# ~/chef-repo/cookbooks/web_application/recipes/webserver.rb
# Install Apache and configure its service.
include_recipe 'apache2::default'

# Create and enable your custom site.
web_app node['web_application']['name'] do
  template "#{node['web_application']['config']}.erb"
end

# Create the document root.
directory node['apache']['docroot_dir'] do
  recursive true
end

# Write a default home page.
file "#{node['apache']['docroot_dir']}/index.php" do
  content '<html>This is a placeholder</html>'
  mode '0644'
  owner node['web_application']['user']
  group node['web_application']['group']
end

# Open port 80 to incoming traffic.
include_recipe 'iptables'
iptables_rule 'firewall_http'


```

The `apache2` cookbook defines the `mod_php5` resource, which configures Apache to work with PHP scripts. In <code class="file-path">webserver.rb</code>, append an `include_recipe` line to install the `mod_php5` Apache module.

```ruby
# ~/chef-repo/cookbooks/web_application/recipes/webserver.rb
# Install the mod_php5 Apache module.
include_recipe 'apache2::mod_php5'
```

Now append a `package` resource to install `php-mysql`.

```ruby
# ~/chef-repo/cookbooks/web_application/recipes/webserver.rb
# Install php-mysql.
package 'php-mysql' do
  action :install
  notifies :restart, 'service[apache2]'
end
```

The entire file looks like this.

```ruby
# ~/chef-repo/cookbooks/web_application/recipes/webserver.rb
# Install Apache and configure its service.
include_recipe 'apache2::default'

# Create and enable our custom site.
web_app node['web_application']['name'] do
  template "#{node['web_application']['config']}.erb"
end

# Create the document root.
directory node['apache']['docroot_dir'] do
  recursive true
end

# Write a default home page.
file "#{node['apache']['docroot_dir']}/index.php" do
  content '<html>This is a placeholder</html>'
  mode '0644'
  owner node['web_application']['user']
  group node['web_application']['group']
end

# Open port 80 to incoming traffic.
include_recipe 'iptables'
iptables_rule 'firewall_http'

# Install the mod_php5 Apache module.
include_recipe 'apache2::mod_php5'

# Install php-mysql.
package 'php-mysql' do
  action :install
  notifies :restart, 'service[apache2]'
end
```

Apache needs to be restarted to enable PHP to use the `php-mysql` package. To do that, we use the [notifies](https://docs.chef.io/resource_common.html#notifications) attribute. The `notifies` attribute performs the `:restart` action on the `apache2` service. But it does so only when it needs to; that is, only when the `package` resource actually performs the `:install` action.