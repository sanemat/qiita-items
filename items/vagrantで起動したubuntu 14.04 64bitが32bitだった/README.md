2014-07-08 1:44時点 vagrantでUbuntu 14.04 64bitを入れたつもりで32bitが立ち上がっていた。

```
config.vm.box = "ubuntu/trusty64"
```

ひとまずostype書き換えてやると64bitで起動する。

```
config.vm.provider "virtualbox" do |vb|
  vb.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
end
```

ひどい。

[ubuntu/trusty64 box uses wrong architecture in ovf config · Issue #4108 · mitchellh/vagrant](https://github.com/mitchellh/vagrant/issues/4108)
