### Set `rules` executable in windows
```shell
git ls-files --stage wazo/rules
git update-index --chmod=+x wazo/rules
```
### Enable debugging log in wazo
```shell
echo "debug: true" > /etc/wazo-plugind/conf.d/debug.yml
systemctl restart wazo-confd
```

### Renaming
Rename plugin:
```shell
find . -name '*template*' -exec rename 's/template/PLUGIN_NAME/g' {} \;
find . -type f -print0 | xargs -0 sed -i '' -e 's/template/PLUGIN_NAME/g'
```
Rename database entity:
```shell
find . -type f -print0 | xargs -0 sed -i '' -e 's/Sample/EntityName/g'
find . -type f -print0 | xargs -0 sed -i '' -e 's/sample/entity_name/g'
```


### Install libraries
```shell
pip install -r requirements.txt
```

### Install plugin
```shell
wazo-plugind-cli -c "install git https://github.com/connectino-platform/wazo-power-dialer-plugin.git"
```
### Uninstall plugin
```shell
wazo-plugind-cli -c "uninstall connectino/wazo-confd-power-dialer"
```

### Drop all tables
```postgresql
drop table plugin_powerdialer_campaign_contact_call;
drop table plugin_powerdialer_contact_contact_list;
drop table plugin_powerdialer_campaign_contact_list;
drop table plugin_powerdialer_contact_list;
drop table plugin_powerdialer_contact;
drop table plugin_powerdialer_campaign;
```

### Notice
We should give `confd.#`,`calld.#` permission to `wazo-confd-internal`
