# Desafio Devops

O projeto contém uma aplicação básica com Node, Ngnix e MySQL. 

A cada atualização da página, um novo registro será cadastrado no banco de dados e será mostrado na listagem, na mesma página.  

O projeto contém algumas falhas e erros, analise e implemente as devidas correções.

Se não entender algum conceito ou parte do problema, não é motivo para se preocupar! Queremos que faça o desafio até onde souber.

### O que deve ser feito? ### 

 - ajustes que fazem todas as aplicações subirem e se comunicarem
 - um README contendo os seus pensamentos ao longo do projeto para identificação e correção dos erros

Faça um fork e realize commits ao longo do processo para que possamos entender o seu modo de pensar! :)
 
------------------------------------------------------------------------------------------------------------------------------------------

# Primeiro contato
Para primeiro contato, subir o docker-compose sem o atríbuto -d para ver os logs dos containers e assim realizar as correções.

# Rede
Primeiro erro a ser corrigido foi os networks declarados, porém sem configuração.
Foi adicionado ao docker-compose.yaml a configuração abaixo, na qual sanou este problema.

networks:
  node-network:
    driver:
      bridge

# Conexão com banco de dados
Após isso o erro de conexão ao banco de dados, que ao analisar o erro, foi verificado que no arquivo "connectionDB.js" o parâmetro da configuração da database estava errado, "nodedb", na qual foi alterado para "node_db". 

# Aplicação Node
Após os problemas acima sanados, a aplicação em Node, deu erro, ao verificar a documentação do Node e o erro, foi visto que a aplicação, estava necessitando de algumas dependências. 
Relendo a documentação foi adicionado ao docker file, antes dos demais processos, a cópia do "package.json" e com ela a instalação com NPM. Conforme código abaixo.

COPY package*.json ./
RUN npm install

Lendo a documentação, foi visto que precisaria iniciar a aplicação e isso foi feito com o código abaixo.

CMD [ "node", "index.js" ]

# NGINX
Com o banco de dados funcional, a aplicação funcional, é hora de ajustar o nginx, na qual subia sem configuração alguma. Checando a documentação do NGINX, a configuração proposta se encaxaria em uma pasta específica. Na qual foi copiada para tal diretório. Conforme o código abaixo.

COPY nginx.conf /etc/nginx/conf.d/default.conf

# Vagrant
Parte dos testes meu antívirus bloqueou com isso, levantei uma máquina virtual com vagrant para teste. Segue no repositório, chamado Vagrantfile.