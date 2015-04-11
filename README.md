# vagrant-serverkit
[Vagrant](https://github.com/mitchellh/vagrant) plug-in for [Serverkit](https://github.com/r7kamura/serverkit).

## Installation
```
$ vagrant plugin install vagrant-serverkit
```

## Configuration
The following configurations are available on serverkit provisioner:

- `recipe_path` - Path to serverkit recipe (e.g. `"recipe.yml"`)
- `variables_path` - Path to serverkit recipe variables (optional)

## Development
For vagrant-serverkit developers, an example Vagrantfile is provided in this repository.
To test provisioning with vagrant-serverkit, execute the following command.

```
$ bundle exec vagrant provision
```

## Example
Here are example files to provision your vagrant box with Serverkit.

```rb
# Vagrantfile
Vagrant.require_plugin("vagrant-serverkit")

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provision :serverkit do |serverkit_config|
    serverkit_config.recipe_path = "recipe.yml.erb"
    serverkit_config.variables_path = "variables.yml"
  end
end
```

```erb
# recipe.yml.erb
resources:
  <%- package_names.each do |package_name| -%>
  - type: package
    name: <%= package_name %>
  <%- end -%>
```

```yaml
# variables.yml
package_names:
  - vim
  - wget
```
