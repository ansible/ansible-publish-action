# ansible-publish-action
Publish Ansible collection to galaxy.ansible.com

## Example Usage
Example of ``.github/workflows/galaxy.yml``
```yml
---
name: Galaxy release

# yamllint disable-line rule:truthy
on:
  release:
    types: ['created']

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: 'Checkout git repo'
        uses: actions/checkout@v4
        with:
          submodules: true
          fetch-depth: 0

      - name: "Publish Collection to Galaxy-NG"
        uses: ansible/ansible-publish-action@v1.0.0
        with:
          api_key: "${{ secrets.GALAXY_API_KEY }}"
```

You can add the variables described below like that:
```yml
[...]
        with:
          api_key: "${{ secrets.GALAXY_API_KEY }}"
          api_server: 'https://galaxy.ansible.com/'
          src_path: '.'
```

## Variables
| Name | default | description |
| --- | --- | --- |
| ``api_key`` | - | Galaxy API key to use |
| ``api_server`` | ``https://galaxy.ansible.com/`` | Galaxy API server to use |
| ``src_path`` | ``.`` | Specific path to collection |

## Some Hints
+ You find your [Galaxy-NG Token](https://galaxy.ansible.com/ui/token/) on Galaxy-NG -> Collections -> API-Token. The collections token is valid for roles too.
+ You can only import collections with this action. For importing ansible roles, please use a different action. *(For Example the [ansible-galaxy-action](https://github.com/marketplace/actions/action-ansible-galaxy-release))*
