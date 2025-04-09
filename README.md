# sandbox-ansible-uv

## コマンドログ

uvのインストール: https://docs.astral.sh/uv/getting-started/installation/

```shell
$ uv init sandbox-ansible-uv -p 3.13
$ uv add ansible-core
$ uv add "boto3==1.35.99"
$ source .venv/bin/activate
$ ansible-playbook playbook.yml --check
```

### boto3をインストールせずに実行してみたときのエラー
```
TASK [Upload test file] ******************************
fatal: [localhost]: FAILED! => {"changed": false, "msg": "Failed to import the required Python library (botocore and boto3) on lima-default's Python /work/sandbox-ansible-uv/.venv/bin/python. Please read the module documentation and install it in the appropriate location. If the required library is installed, but Ansible is using the wrong Python interpreter, please consult the documentation on ansible_python_interpreter"}
```

## ansible or ansible-core

### ansible

```
$ uv run ansible-galaxy collection list

# /work/sandbox-ansible-uv/.venv/lib/python3.13/site-packages/ansible_collections
Collection                               Version
---------------------------------------- -------
amazon.aws                               9.3.0  
ansible.netcommon                        7.1.0  
ansible.posix                            1.6.2  
ansible.utils                            5.1.2  
ansible.windows                          2.8.0  
arista.eos                               10.1.1 
awx.awx                                  24.6.1 
azure.azcollection                       3.3.1  
check_point.mgmt                         6.4.0  
chocolatey.chocolatey                    1.5.3  
cisco.aci                                2.10.1 
cisco.asa                                6.1.0  
cisco.dnac                               6.31.0 
cisco.intersight                         2.0.20 
cisco.ios                                9.1.2  
cisco.iosxr                              10.3.0 
cisco.ise                                2.10.0 
cisco.meraki                             2.20.8 
cisco.mso                                2.9.0  
cisco.nxos                               9.3.0  
cisco.ucs                                1.15.0 
cloud.common                             4.0.0  
cloudscale_ch.cloud                      2.4.1  
community.aws                            9.1.0  
community.ciscosmb                       1.0.10 
community.crypto                         2.26.0 
community.digitalocean                   1.27.0 
community.dns                            3.2.2  
community.docker                         4.5.2  
community.general                        10.5.0 
community.grafana                        2.1.0  
community.hashi_vault                    6.2.0  
community.hrobot                         2.2.0  
community.library_inventory_filtering_v1 1.0.2  
community.libvirt                        1.3.1  
community.mongodb                        1.7.9  
community.mysql                          3.13.0 
community.network                        5.1.0  
community.okd                            4.0.1  
community.postgresql                     3.12.0 
community.proxysql                       1.6.0  
community.rabbitmq                       1.4.0  
community.routeros                       3.5.0  
community.sap_libs                       1.4.2  
community.sops                           2.0.3  
community.vmware                         5.5.0  
community.windows                        2.4.0  
community.zabbix                         3.3.0  
containers.podman                        1.16.3 
cyberark.conjur                          1.3.3  
cyberark.pas                             1.0.30 
dellemc.enterprise_sonic                 2.5.1  
dellemc.openmanage                       9.10.0 
dellemc.powerflex                        2.6.0  
dellemc.unity                            2.0.0  
f5networks.f5_modules                    1.34.1 
fortinet.fortimanager                    2.9.1  
fortinet.fortios                         2.3.9  
google.cloud                             1.5.1  
grafana.grafana                          5.7.0  
hetzner.hcloud                           4.3.0  
ibm.qradar                               4.0.0  
ibm.spectrum_virtualize                  2.0.0  
ibm.storage_virtualize                   2.6.0  
ieisystem.inmanage                       3.0.0  
infinidat.infinibox                      1.4.5  
infoblox.nios_modules                    1.8.0  
inspur.ispim                             2.2.3  
junipernetworks.junos                    9.1.0  
kaytus.ksmanage                          2.0.0  
kubernetes.core                          5.1.0  
kubevirt.core                            2.1.0  
lowlydba.sqlserver                       2.5.0  
microsoft.ad                             1.8.0  
netapp.cloudmanager                      21.24.0
netapp.ontap                             22.14.0
netapp.storagegrid                       21.14.0
netapp_eseries.santricity                1.4.1  
netbox.netbox                            3.21.0 
ngine_io.cloudstack                      2.5.0  
openstack.cloud                          2.4.1  
ovirt.ovirt                              3.2.0  
purestorage.flasharray                   1.33.1 
purestorage.flashblade                   1.19.2 
sensu.sensu_go                           1.14.0 
splunk.es                                4.0.0  
telekom_mms.icinga_director              2.2.2  
theforeman.foreman                       4.2.0  
vmware.vmware                            1.10.1 
vmware.vmware_rest                       4.6.0  
vultr.cloud                              1.13.0 
vyos.vyos                                5.0.0  
wti.remote                               1.0.10
```

### ansible-core

```
$ ansible-galaxy collection list

# /home/ubuntu/.ansible/collections/ansible_collections
Collection Version
---------- -------
amazon.aws 9.4.0
```

- 自分でcollectionをインストールする必要あり
- デフォルトだとホームディレクトリにインストールされる
- インストール先ではcollectionの複数のバージョンを管理する仕組みまではなさそう
  - 違うバージョンがインストールされている状態で`ansible-galaxy install -r requirements.yml`を実行したら置換された
