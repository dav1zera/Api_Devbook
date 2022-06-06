# api_devbook

Devbook é uma pequena api escrita em golang, que simula uma rede social de livros, onde permite criar, atualizar, deletar e buscar usuários através dos métodos de CRUD
O sistema possui 2 tabelas Usuários e Publicações.
Na tabela Usuários temos duas tabelas, usuários e seguidores.
Através dos métodos de CRUD podemos fazer o seguinte para essa tabela:

	GET => Buscar um único usuário através do seu id ou buscar todos os usuários cadastrados no banco, além disso podemos buscar seguidores ou buscar um único seguidor
	POST => Criar usuários, seguir usuários, parar de seguir usuário e atualizar senha do usuário
	PUT => Atualizar usuário
	DELETE => Deletar usuário	

A segunda tabela é chamada de Publicações, nela usamos os mesmos métodos CRUD descritos lá em cima, mas tem algumas funcionalidades a mais
Como buscar publicações de acordo com os usuários que segue, curtir e discutir publicações

	Estrutura da Aplicação
	A api é dividida em 2 tipos de pacotes auxiliares e principais
	Os pacotes principais estão relacionados a estrutura da api, esses pacotes são
	Main, Router, Controllers, Modelos e Repositórios

	Main => Por onde a api é executada

	Router => Configuração do router e rotas

	Controllers => Funções que vão lidar com as requisições HTTP

	Repositórios => Aqui onde há interação com banco de dados

	Modelos => Onde vai ficar as duas tabelas, a de usuário e publicações, nessa parte vai ficar também os structs dessas respectivas tabelas, além de seus métodos


	Pacotes auxiliares dessa api são:

	Config, Banco, Autenticação, Middleware, Segurança e Respostas

	Config => Configuração de variáveis de ambiente

	Banco => Abrir conexão com o banco de dados

	Autenticação => Cuidar do login e criação de tokens  

	Middleware => Camada responsável entre requisição e resposta

	Segurança => funções de hash na senha

	Respostas => Padronizar as respostas
