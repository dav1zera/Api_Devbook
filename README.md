# api_devbook

Devbook é uma pequena api escrita em golang, que simula uma rede social de livros, onde permite criar, atualizar, deletar e buscar usuários através dos métodos de CRUD
O sistema possui 2 tabelas principais Usuários e Publicações.
Na tabela Usuários temos duas tabelas, usuários e seguidores.
Através dos métodos de CRUD podemos fazer o seguinte para essa tabela:

	GET => Buscar um único usuário através do seu id ou buscar todos os usuários cadastrados no banco, além disso podemos buscar seguidores ou buscar um único seguidor
	POST => Criar usuários, seguir usuários, parar de seguir usuário e atualizar senha do usuário
	PUT => Atualizar usuário
	DELETE => Deletar usuário	

A segunda tabela é chamada de Publicações, nela usamos os mesmos métodos CRUD descritos lá em cima, mas tem algumas funcionalidades a mais,
Como buscar publicações de acordo com os usuários que segue, curtir e discutir publicações.

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
	
Banco de dados;

O banco de dados da api foi feita usando o MySql e tem como seguintes tabelas: 

	CREATE DATABASE IF NOT EXISTS devbook;
	USE devbook;

	DROP TABLE IF EXISTS publicacoes;
	DROP TABLE IF EXISTS seguidores;
	DROP TABLE IF EXISTS usuarios;

	CREATE TABLE usuarios(
	    id int auto_increment primary key,
	    nome varchar(50) not null,
	    nick varchar(50) not null unique,
	    email varchar(50) not null unique,
	    senha varchar(100) not null,
	    criadoEm timestamp default current_timestamp()
	) ENGINE=INNODB;

	CREATE TABLE seguidores(
	    usuario_id int not null,
	    FOREIGN KEY (usuario_id)
	    REFERENCES usuarios(id)
	    ON DELETE CASCADE,

	    seguidor_id int not null,
	    FOREIGN KEY (seguidor_id)
	    REFERENCES usuarios(id)
	    ON DELETE CASCADE,

	    primary key(usuario_id, seguidor_id)
	) ENGINE=INNODB;

	CREATE TABLE publicacoes(
	    id int auto_increment primary key,
	    titulo varchar(50) not null,
	    conteudo varchar(300) not null,

	    autor_id int not null,
	    FOREIGN KEY (autor_id)
	    REFERENCES usuarios(id)
	    ON DELETE CASCADE,

	    curtidas int default 0,
	    criadaEm timestamp default current_timestamp
	) ENGINE=INNODB;

Postman;

Para testar as rotas, requisições HTTP da api usei a aplicação do Postman.

Os seguintes comandos foram utilizados para fazer essas requisições:

	Tabela de usuários(Primeira tabela criada no Mysql)
	criar usuário, 	   método POST,   rota => localhost:5000/usuarios,
	fazer login, 	   método POST,   rota => localhost:5000/login,
	buscar usuário,    método GET,    rota => localhost:5000/usuarios/id,
	buscar usuários,   método GET,    rota => localhost:5000/usuarios,
	atualizar usuário, método PUT,    rota => localhost:5000/usuarios/id,
	deletar usuário,   método DELETE, rota => localhost:5000/usuarios/id,
	
	
	Tabela de seguidores(segunda tabela criada no Mysql)
	seguir usuário, 	   método POST,   rota => localhost:5000/usuarios/id/seguir,
	parar de seguir, 	   método POST,   rota => localhost:5000/usuarios/id/parar-de-seguir,
	ver seguidores,            método GET,    rota => localhost:5000/usuarios/id/seguidores,
	ver quem está seguindo,    método GET,    rota => localhost:5000/usuarios/id,seguindo,
	
	
	Tabela de publicações(terceira tabela criada no Mysql)
	criar publicação, 	   método POST,    rota => localhost:5000/publicacoes,
	buscar publicação, 	   método GET,     rota => localhost:5000/publicacoes/id,
	atualizar publicação,      método PUT,     rota => localhost:5000/publicacoes/id,
	deletar publicação,        método DELETE,  rota => localhost:5000/publicacoes/id,
	curtir publicação,         método POST,    rota => localhost:5000/publicacoes/curtir,
	descurtir publicação,      método POST,    rota => localhost:5000/publicacoes/descurtir
	
	
	Aviso: NO VÍDEO DO FUNCIONAMENTO DA API, FORAM TESTADAS APENAS AS ROTAS DE USUÁRIOS 
	
	
	
	
	
