# Orquestração no Grafana

Esse playbook tem a finalidade de auxiliar quem administar a criação de usuários e acesso a organização no Grafana.

### Há 3 roles com tags no arquivo main.yml 
- **list-orgs** - lista todas as organizações
- **create-datasource** - Cria datasources MySQL nas organizações listadas no anterior.
- **update-dashboard** -  (Em Desenvolvimento)


## Dica de uso

Chame as role através das tags:

```python
>$ ansible-playbook -i hosts main.yml --tags "list-orgs-role"
```
