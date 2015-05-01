## Summary

You ran a few basic Chef commands and got a flavor of what Chef can do. You learned that a resource describes one part of the system and its desired state. You worked with a [file](https://docs.chef.io/resource_file.html), which is one kind of resource.

### Resources describe the what, not the how

Your policy declares _what_ state each resource should be in, but not _how_ to get there. In this lesson, you declared that the file <code class="file-path">motd</code> must exist and what its contents are, but you didn't specify how to apply that policy. This layer of abstraction can not only make you more productive, but it can also make your work more portable across platforms.

A recipe declares what state each resource should be in but not how to achieve that state. Chef handles these complexities for you.

### Resources have actions

When you deleted the file, you saw the `:delete` action.

Think of an action as the process that achieves the desired configuration state. Every resource in Chef has a default action, and it's often the most common affirmative one &ndash; for example, _create_ a file, _install_ a package, and _start_ a service.

When we created the file we didn't specify the `:create` action because `:create` is the default. But of course you can specify it if you want.

The documentation for each resource type, [file](https://docs.chef.io/resource_file.html) for example, explains the type's default action.

### Recipes organize resources

In Chef, <code class="file-path">hello.rb</code> is an example of a [recipe](https://docs.chef.io/recipes.html), or an ordered series of configuration states. A recipe typically contains related states, such as everything needed to configure a web server, database server, or a load balancer.

Our recipe states everything we need to manage the MOTD file. You used [chef-apply](https://docs.chef.io/ctl_chef_apply.html) to apply that recipe from the command line.