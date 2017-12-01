# -*- mode: ruby -*-
# vi: set ft=ruby :

# Defining Oracle Proxy / Use Case Flags
load './vagrant-addons/ProxyConfigfile'

# Plugin installation procedure from http://stackoverflow.com/a/28801317
# This will load by default proxyconf to allow the client access to the proxy.
required_plugins = %w(vagrant-proxyconf vagrant-disksize)
#
plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
if not plugins_to_install.empty?
  puts "Installing plugins: #{plugins_to_install.join(' ')}"
  if system "vagrant plugin install #{plugins_to_install.join(' ')}"
    exec "vagrant #{ARGV.join(' ')}"
  else
    abort "Installation of one or more plugins has failed. Aborting."
  end
end
# Completed Defining Some Oracle / Use Case Flags

##############################################################################
Vagrant.configure("2") do |config|

  # This demo will use Oracle Linux 7 server image.
  # You can search for boxes from the Vagrant Cloud at https://vagrantcloud.com/search
  # or Oracle Linux boxes at http://yum.oracle.com/boxes
  config.vm.box_url = "http://yum.oracle.com/boxes/oraclelinux/ol74/ol74.box"
  config.vm.box = "ol74"

  # Share an additional folder to the guest VM, default is "share" in the current directory.
  config.vm.synced_folder "vagrant-share", "/vagrant-share"

  # Enable provisioning of the client with a shell script.
  config.vm.provision "shell", path: "./vagrant-shell/provision.sh"
end
