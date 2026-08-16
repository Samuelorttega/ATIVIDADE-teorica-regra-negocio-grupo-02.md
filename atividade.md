# ATIVIDADE-teorica-regra-negocio-grupo-02.md
**Aluno(s):** 1.Lucas Moretti Izel Do Carmo 2.Paulo Emilio De Souza Fagundes 3.Samuel Jose Ortega Jimenez 
**Turna:** G2 BANCO DE DADOS 
**Data:** 17/08/2026 
**Repositorio Git:** https://github.com/Samuelorttega/ATIVIDADE-teorica-regra-negocio-grupo-02.md/edit/main/atividade.md

Resumo Executivo

A Inteligência Artificial (IA) generativa pode facilitar o trabalho com bancos de dados, principalmente na criação de consultas SQL a partir de perguntas feitas em linguagem natural. Isso pode aumentar a produtividade e ajudar usuários que não possuem conhecimento avançado de SQL.

Por outro lado, permitir que ferramentas de IA tenham acesso amplo aos dados pode gerar riscos, como exposição de informações sensíveis, consultas incorretas e problemas de desempenho.

O grupo defende que a IA não deve ser proibida, mas também não deve possuir acesso irrestrito ao banco. A utilização deve ocorrer com controles como menor privilégio, roles, views, permissões, auditoria e monitoramento.

1. Desenvolvimento Teórico

1.1 O que é o DBA e quais suas funções?

O DBA (Database Administrator) é o profissional responsável pela administração e pelo controle do banco de dados.

Entre suas principais funções estão:

- definir e organizar a estrutura do banco de dados;
- administrar usuários e roles;
- controlar permissões de acesso;
- aplicar regras de integridade;
- acompanhar o desempenho do banco;
- realizar auditorias;
- proteger informações importantes;
- realizar e verificar backups;
- auxiliar na recuperação dos dados quando necessário.

No PostgreSQL, o DBA pode utilizar roles e privilégios para controlar quais usuários podem consultar, inserir, alterar ou excluir informações.

Com a utilização de IA, o trabalho do DBA se torna ainda mais importante, pois é necessário controlar também como as ferramentas de IA podem acessar e utilizar os dados.

1.2 Perfis de usuários de banco de dados

Os bancos de dados podem possuir diferentes tipos de usuários.

Programadores de aplicações: desenvolvem sistemas que utilizam o banco. Possuem acesso de acordo com as funções da aplicação. A principal vantagem é a possibilidade de automatizar tarefas, mas uma aplicação mal desenvolvida pode causar problemas de segurança.

Usuários sofisticados: possuem conhecimento técnico e podem realizar consultas diretamente no banco utilizando SQL e outras ferramentas. Possuem maior autonomia, mas precisam de limites para evitar acessos desnecessários.

Usuários especialistas: possuem conhecimento mais avançado e podem criar consultas complexas, análises e utilizar ferramentas de IA. Mesmo assim, ser especialista não significa precisar acessar todos os dados.

Usuários navegantes: normalmente utilizam sistemas ou aplicações prontas para consultar informações. Possuem menos conhecimento técnico e, por isso, geralmente não precisam acessar diretamente as tabelas do banco.

Cada perfil possui necessidades diferentes. Portanto, os acessos devem ser definidos de acordo com a função e a necessidade de cada usuário.

1.3 Riscos do uso de IA por usuários especialistas

A utilização de IA pode trazer benefícios, mas também apresenta riscos.

Consulta incorreta: a IA pode gerar uma consulta que esteja correta na sintaxe, mas errada na lógica. Isso pode produzir resultados incorretos.

Exposição de dados sensíveis: o usuário pode enviar informações reais, como CPF, telefone ou dados de clientes, para uma ferramenta externa de IA.

Degradação de performance: uma consulta criada pela IA pode consumir muitos recursos do banco e prejudicar outros usuários e sistemas.

Vazamento por prompts: informações presentes nos comandos enviados à IA podem conter dados que não deveriam sair do ambiente da organização.

Esses problemas podem afetar a segurança, a privacidade e a integridade das informações.

Por isso, consultas criadas por IA devem ser verificadas antes da execução, e os usuários devem receber orientação sobre quais informações podem utilizar nas ferramentas de IA.

1.4 Distribuição segura de dados

Uma das principais formas de proteger os dados é utilizar o princípio do menor privilégio. Isso significa que cada usuário deve receber apenas as permissões necessárias para realizar sua função.

No PostgreSQL, algumas medidas importantes são:

Roles: permitem organizar permissões de acordo com as funções dos usuários.

Views: permitem disponibilizar somente determinadas colunas ou informações de uma tabela.

Controle de execução: permissões podem definir quais operações um usuário pode realizar, como "SELECT", "INSERT", "UPDATE" e "DELETE".

Auditoria: permite registrar e acompanhar acessos e operações realizadas no banco.

Conformidade com a LGPD: os dados pessoais devem ser tratados de acordo com as regras e princípios estabelecidos pela legislação.

Por exemplo, um funcionário que precisa analisar vendas por cidade não precisa necessariamente ter acesso ao CPF e ao telefone dos clientes.

1.5 Atuação do DBA no cenário de IA

No cenário de utilização de IA, o DBA deve continuar controlando o ambiente do banco de dados.

Entre suas principais atividades estão:

- definir políticas de acesso;
- criar e administrar roles;
- acompanhar consultas e desempenho;
- realizar auditorias;
- orientar os usuários sobre segurança;
- proteger dados sensíveis;
- controlar o acesso das aplicações;
- realizar backups;
- acompanhar possíveis problemas causados por consultas geradas por IA.

O DBA também pode ajudar a definir quais ambientes devem ser utilizados para análises. Sempre que possível, consultas analíticas podem ser realizadas em bancos de análise ou réplicas de leitura, reduzindo o impacto no banco de produção.

1.6 Análise crítica: qual a melhor abordagem?

Existem duas soluções extremas: proibir completamente a IA ou permitir acesso irrestrito.

A proibição pode reduzir alguns riscos, mas também elimina benefícios da IA, como aumento de produtividade e auxílio na criação de consultas.

Por outro lado, permitir acesso irrestrito pode causar problemas de segurança, exposição de dados e perda de desempenho.

Por isso, o grupo considera que a melhor abordagem está entre essas duas opções.

A IA deve ser permitida, mas dentro de limites definidos pela organização. O acesso deve utilizar menor privilégio, roles, views, permissões e monitoramento.

A IA deve ser vista como uma ferramenta de apoio e não como uma autoridade sobre o banco de dados. O usuário deve verificar os resultados e o banco deve continuar aplicando suas próprias regras de segurança.

2. Exemplos e Casos

Considere uma empresa que possui uma tabela chamada "clientes":

CREATE TABLE clientes (
    id_cliente INTEGER,
    nome VARCHAR(100),
    cpf VARCHAR(14),
    telefone VARCHAR(20),
    cidade VARCHAR(100),
    estado VARCHAR(2),
    data_cadastro DATE
);

Um analista precisa analisar a quantidade de clientes por cidade e estado. Para essa atividade, ele não precisa acessar CPF ou telefone.

Primeiro, pode ser criada uma role:

CREATE ROLE analista_ia LOGIN;

Depois, pode ser criada uma view contendo somente as informações necessárias:

CREATE VIEW clientes_visiveis AS
SELECT
    id_cliente,
    cidade,
    estado,
    data_cadastro
FROM clientes;

Em seguida, podem ser definidas as permissões:

GRANT USAGE ON SCHEMA public TO analista_ia;

GRANT SELECT ON clientes_visiveis TO analista_ia;

REVOKE ALL ON clientes FROM analista_ia;

Também é necessário verificar se o usuário não recebeu acesso à tabela por meio de outra role ou de permissões concedidas ao "PUBLIC".

O analista poderá realizar uma consulta como:

SELECT cidade, estado, COUNT(*)
FROM clientes_visiveis
GROUP BY cidade, estado;

Nesse caso, ele consegue realizar a análise sem precisar acessar diretamente CPF e telefone.

Caso prático: sistema de vendas

Imagine uma empresa que possui um sistema de vendas. Os analistas precisam consultar a quantidade de vendas por cidade, enquanto os dados pessoais dos clientes devem permanecer protegidos.

Uma ferramenta de IA pode ajudar o analista a criar consultas, mas o usuário deve ter acesso somente às informações necessárias.

Nesse cenário, uma view pode disponibilizar apenas os dados relacionados às vendas e à localização. O banco de dados continua controlando as permissões.

Assim, mesmo que a IA gere uma consulta tentando acessar informações que o usuário não possui permissão para consultar, o PostgreSQL pode bloquear o acesso, desde que as permissões estejam configuradas corretamente.

3. Referências

AUTIO, Chloe et al. Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile. NIST AI 600-1. 2024. Disponível em: https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence. Acesso em: 16 ago. 2026.

NIST. Least Privilege. Computer Security Resource Center Glossary. Disponível em: https://csrc.nist.gov/glossary/term/least_privilege. Acesso em: 16 ago. 2026.

POSTGRESQL GLOBAL DEVELOPMENT GROUP. PostgreSQL Documentation: Database Roles. Disponível em: https://www.postgresql.org/docs/18/user-manag.html. Acesso em: 16 ago. 2026.

POSTGRESQL GLOBAL DEVELOPMENT GROUP. PostgreSQL Documentation: Privileges. Disponível em: https://www.postgresql.org/docs/current/ddl-priv.html. Acesso em: 16 ago. 2026.

POSTGRESQL GLOBAL DEVELOPMENT GROUP. PostgreSQL Documentation: CREATE VIEW. Disponível em: https://www.postgresql.org/docs/current/sql-createview.html. Acesso em: 16 ago. 2026.

BRASIL. Lei nº 13.709, de 14 de agosto de 2018 — Lei Geral de Proteção de Dados Pessoais (LGPD). Disponível em: https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm. Acesso em: 16 ago. 2026.

4. Conclusões

A utilização de IA em bancos de dados pode trazer benefícios importantes, principalmente para a criação de consultas e realização de análises.

Entretanto, o acesso aos dados deve ser controlado. O uso de menor privilégio, roles, views, permissões, auditoria e monitoramento ajuda a reduzir os riscos.

Também ficou claro que o DBA continua tendo um papel fundamental. Ele deve controlar os acessos, acompanhar o desempenho, proteger os dados e ajudar a definir políticas para utilização da IA.

O grupo conclui que a melhor solução não é proibir a IA nem permitir acesso irrestrito. A melhor alternativa é utilizar a IA como ferramenta de apoio, mantendo o controle dos dados e da segurança no banco de dados.

Dessa forma, é possível aproveitar os benefícios da IA sem deixar de lado a segurança, a privacidade, a integridade e a conformidade com a LGPD.
