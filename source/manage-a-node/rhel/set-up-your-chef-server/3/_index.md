## 3. Get the Apache cookbook

In [Learn the Chef basics](/learn-the-basics/rhel/), you wrote a cookbook that configures an Apache web server. You'll run that cookbook on your new node.

But the virtual machine you used earlier is likely gone! Instead of having you type in the cookbook again, let's get a copy from Chef Supermarket instead. [Chef Supermarket](https://supermarket.chef.io/) is a place for the community to share cookbooks. Chef Supermarket contains the Learn Chef Apache cookbook for you to download.

From your <code class="file-path">~/chef-repo</code> directory, run these commands to download the cookbook from Chef Supermarket and extract it.

```bash
# ~/chef-repo
$ knife cookbook site download learn_chef_httpd
Downloading learn_chef_httpd from the cookbooks site at version 0.2.0 to /home/chef/chef-repo/learn_chef_httpd-0.2.0.tar.gz
Cookbook saved: /home/chef/chef-repo/learn_chef_httpd-0.2.0.tar.gz
$ tar -zxvf learn_chef_httpd-0.2.0.tar.gz -C cookbooks
learn_chef_httpd/
learn_chef_httpd/.kitchen.yml
learn_chef_httpd/Berksfile
learn_chef_httpd/chefignore
learn_chef_httpd/metadata.json
learn_chef_httpd/metadata.rb
learn_chef_httpd/README.md
learn_chef_httpd/recipes/
learn_chef_httpd/templates/
learn_chef_httpd/templates/default/
learn_chef_httpd/templates/default/index.html.erb
learn_chef_httpd/recipes/default.rb
$ rm learn_chef_httpd*.tar.gz
```