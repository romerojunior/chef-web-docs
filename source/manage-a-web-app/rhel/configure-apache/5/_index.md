## 5. Enable inbound traffic to your web site

Depending on how your server is configured, it may be necessary to open port 80 (HTTP) to incoming traffic. Let's make sure that port 80 is open by configuring the firewall rules.

The easiest way to set a firewall rule is to use the [iptables](https://supermarket.chef.io/cookbooks/iptables) cookbook from Chef Supermarket.

First, modify <code class="file-path">metadata.rb</code> to load the `iptables` cookbook.

```ruby
# ~/chef-repo/cookbooks/web_application/metadata.rb
name             'web_application'
maintainer       'The Authors'
maintainer_email 'you@example.com'
license          'all_rights'
description      'Installs/Configures web_application'
long_description 'Installs/Configures web_application'
version          '0.1.0'

depends 'apache2', '~> 3.0.1'
depends 'iptables', '~> 0.14.1'
```

Now create a template file to hold our firewall rule.

```bash
# ~/chef-repo
$ chef generate template cookbooks/web_application firewall_http
Compiling Cookbooks...
Recipe: code_generator::template
  * directory[cookbooks/web_application/templates/default] action create (up to date)
  * template[cookbooks/web_application/templates/default/firewall_http.erb] action create
    - create new file cookbooks/web_application/templates/default/firewall_http.erb
    - update content in file cookbooks/web_application/templates/default/firewall_http.erb from none to e3b0c4
    (diff output suppressed by config)
```

Now add this rule to <code class="file-path">firewall_http.erb</code> to open port 80 to incoming traffic.

```ruby
# ~/chef-repo/cookbooks/web_application/templates/default/firewall_http.erb
# Port 80 for http
-A FWR -p tcp -m tcp --dport 80 -j ACCEPT
```

Now edit <code class="file-path">webserver.rb</code> to use the `iptables_rule` resource, which is provided by the `iptables` cookbook,

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

Also edit your attributes file to set the `node['iptables']['install_rules']` attribute to `false`. We do this because we don't want the `iptables` cookbook to install any rules other than to open port 80 to incoming traffic.

```ruby
# ~/chef-repo/cookbooks/web_application/attributes/default.rb
default['web_application']['user'] = 'web_admin'
default['web_application']['group'] = 'web_admin'

default['web_application']['name'] = 'customers'
default['web_application']['config'] = 'customers.conf'

default['apache']['docroot_dir'] = '/srv/apache/customers'

default['iptables']['install_rules'] = false
```