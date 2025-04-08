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
