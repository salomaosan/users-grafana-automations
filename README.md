# Orquestração de Usuários no Grafana

Esse playbook tem a finalidade de auxiliar quem administra varias organizações no Grafana e necessita mantê-las atualizados.

### Há 3 roles com tags no arquivo main.yml 
- **create-user** - cria usuários e os associa a uma organização informada como paramentro.
```bash
ansible-playbook -i hosts main.yml --tags "create-user-role" \
--extra-vars "user_email=teste@grafana.com.br" \
--extra-vars "org_name='organization name'" \
--extra-vars="user_role=Admin"
```

- **list-orgs** - lista todas as organizações e grava na variavel ansible "organization".
```bash
ansible-playbook -i hosts main.yml --tags "list-orgs-role"
```
- **associate-user-to-orgs** - Somente usuários do tipo flowti.com.br acessaram essa role pois esses serão propagados para todas as organizações.
```bash
ansible-playbook -i hosts main.yml --tags "associate-user-to-orgs-role" \
--extra-vars "user_email=teste@grafana.com.br" \
--extra-vars="user_role=Admin"
```