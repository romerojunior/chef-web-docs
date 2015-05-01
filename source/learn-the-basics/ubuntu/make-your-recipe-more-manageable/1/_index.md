## 1. Create a cookbook

First, from your <code class="file-path">~/chef-repo</code> directory, create a <code class="file-path">cookbooks</code> directory and `cd` there.

```bash
# ~/chef-repo
$ mkdir cookbooks
$ cd cookbooks
```

Now run the `chef` command to generate a cookbook named `learn_chef_apache2`.

```bash
# ~/chef-repo/cookbooks
$ chef generate cookbook learn_chef_apache2
```

Here's the directory structure that the command created.

```bash
# ~/chef-repo/cookbooks
$ tree
.
└── learn_chef_apache2
    ├── Berksfile
    ├── chefignore
    ├── metadata.rb
    ├── README.md
    └── recipes
        └── default.rb

2 directories, 5 files
```

Note the default recipe, named <code class="file-path">default.rb</code>. This is where we'll move our Apache recipe in a moment.