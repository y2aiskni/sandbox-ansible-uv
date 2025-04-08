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
