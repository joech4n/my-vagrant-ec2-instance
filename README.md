
1. Create `~/.vagrant-aws` config file (for stuff you don't want to version control)

    ```
access_key_id: 'XXXXXXXXXXXXXXXXXXXX'
secret_access_key: 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
keypair_name: 'username'
```

2. Clone Vagrant project

    ```
git clone git@github.com:joech4n/my-vagrant-ec2-instance.git
```

3. Edit `Vagrantfile` to customize VM

4. Launch VM

    ```
vagrant up --provider=aws
```
