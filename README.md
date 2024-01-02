## 💻 Como criar várias databases postgress numa única instância docker

### Basicamente são necessarios criar dois arquivos: 
1) O arquivo compose.yaml com as instruções de criação do contaneiner

2) Um arquivo bash (multiple-databases.sh) que "ensina" ao contaneiner a ler a tag POSTGRES_MULTIPLE_DATABASES e criar quantas databases forem solicitadas

Como um plus criei tbm segundo contaneiner PGAdmin para administração do Postgres. Com esses exemplos, podem abstrair para outros banco de dados e serviços.

---

### ⚙️ Descrição das Tags no compose.yaml e no script multiple-databases.sh

- [x] restart: unless-stopped // Semelhante ao `always`, exceto que quando o contêiner é interrompido (manualmente ou não), ele não é reiniciado mesmo após a reinicialização do daemon do Docker.
- [x] POSTGRES_MULTIPLE_DATABASES: 'mydatabase, mydatabase_test' // nomes das databases que devem ser criadas
- [x] healthcheck: // A instrução `HEALTHCHECK` informa ao Docker como testar um contêiner para verificar se ele ainda está funcionando. Isso pode detectar casos como um servidor web preso em um loop infinito e incapaz de lidar com novas conexões, mesmo que o processo do servidor ainda esteja em execução.
- [x] volumes: // foi criado um volume e indicado que a instancia deve tbm executar o script bash
- [x] multiple-databases.sh: // script bash
- [x] Implementa a função `create_database()` para criar database e atribuir permissão ao usuário postgres
- [x] Executa a função em loop para cada database citada na tag POSTGRES_MULTIPLE_DATABASES

---

