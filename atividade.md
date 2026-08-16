# ATIVIDADE-teorica-regra-negocio-grupo-02.md
**Aluno(s):** 1.Lucas Moretti Izel Do Carmo 2.Paulo Emilio De Souza Fagundes 3.Samuel Jose Ortega Jimenez 
**Turna:** G2 BANCO DE DADOS 
**Data:** 17/08/2026 
**Repositorio Git:** https://github.com/Samuelorttega/ATIVIDADE-teorica-regra-negocio-grupo-02.md/edit/main/atividade.md

##  Resumo Executivo
 A utilização de Inteligência Artificial (IA) generativa modificou a forma como usuários especialistas e analistas interagem com bancos de dados. Ferramentas capazes de transformar linguagem natural em comandos SQL podem aumentar a produtividade e facilitar a realização de consultas e análises. Entretanto, permitir que essas ferramentas tenham acesso amplo aos dados pode criar riscos relacionados à segurança, privacidade, desempenho e governança.

 Este trabalho defende que a utilização de IA em ambientes de banco de dados não deve ser proibida, mas também não deve ocorrer com acesso irrestrito. A solução mais adequada é uma arquitetura baseada em camadas de proteção, utilizando o princípio do menor privilégio, papéis (Roles), Views, controle de permissões, auditoria e separação entre ambientes de produção e análise.

 O princípio do menor privilégio estabelece que usuários e processos devem receber somente os acessos necessários para realizar suas atividades. Esse princípio é reconhecido pelo NIST como uma prática de segurança.

 No PostgreSQL, o controle de acesso é realizado por meio de Roles e privilégios, permitindo determinar quais usuários podem acessar determinados objetos e executar determinadas operações.

 Dessa forma, a presença da IA não elimina a importância do DBA. Pelo contrário, aumenta a necessidade de governança, controle de acesso, avaliação de riscos e monitoramento do ambiente.

1. Desenvolvimento Teórico

1.1 O problema: Inteligência Artificial e Bancos de Dados

A Inteligência Artificial generativa pode auxiliar profissionais na criação de consultas SQL a partir de perguntas realizadas em linguagem natural. Essa capacidade pode reduzir o tempo necessário para construir consultas e permitir que usuários com diferentes níveis de conhecimento técnico realizem análises de dados.

Porém, existe uma diferença importante entre gerar uma consulta SQL e garantir que essa consulta seja segura, correta e adequada ao ambiente em que será executada.

Uma IA pode gerar uma consulta sintaticamente válida, mas isso não significa necessariamente que a consulta esteja correta do ponto de vista do negócio. Uma consulta pode utilizar tabelas inadequadas, produzir resultados incorretos, acessar informações que não deveriam estar disponíveis ou consumir recursos excessivos do banco.

O NIST destaca que sistemas de IA generativa apresentam riscos que podem surgir ou ser agravados durante diferentes etapas do ciclo de vida da IA, sendo necessário identificar, avaliar e gerenciar esses riscos.

Por isso, a principal questão analisada neste trabalho é:

Como permitir que usuários especialistas utilizem IA para realizar análises sem comprometer a segurança, a privacidade e o desempenho do banco de dados?

Nossa posição é que a IA deve ser permitida, porém dentro de limites técnicos e administrativos definidos pela organização.

1.2 O papel do DBA

 ⁶O Administrador de Banco de Dados (DBA - Database Administrator) é responsável por atividades relacionadas à administração, segurança, disponibilidade, desempenho e organização do banco de dados.

 No contexto da utilização de IA, o papel do DBA torna-se ainda mais importante porque ele deve estabelecer limites para o acesso aos dados e garantir que as ferramentas utilizadas pelos usuários não tenham privilégios superiores aos necessários.

Entre suas principais responsabilidades estão:

- administrar usuários e Roles;
- conceder e revogar privilégios;
- controlar o acesso às tabelas, Views e outros objetos;
- acompanhar o desempenho do banco;
- definir políticas de segurança;
- realizar auditorias;
- proteger informações sensíveis;
- manter estratégias de backup e recuperação;
- auxiliar na definição de políticas para utilização de IA.

 No PostgreSQL, as permissões são controladas por meio de privilégios, como "SELECT", "INSERT", "UPDATE", "DELETE", "EXECUTE" e "USAGE". Esses privilégios podem ser concedidos a Roles específicas.

 Portanto, o DBA não deve ser visto apenas como a pessoa que "cuida do banco". No cenário analisado, ele também participa da governança do acesso aos dados e da utilização segura da IA.

---

1.3 Usuários de banco de dados e níveis de acesso

Os bancos de dados podem ser utilizados por diferentes tipos de usuários, cada um com necessidades específicas.

Programadores de aplicações

São profissionais que desenvolvem sistemas responsáveis por acessar o banco de dados.

Eles normalmente utilizam consultas SQL dentro das aplicações e precisam de permissões compatíveis com as funções que o sistema executa.

O principal risco está relacionado à implementação inadequada das aplicações, como consultas inseguras ou falhas de validação de entrada.

Usuários sofisticados ou analistas

São usuários que possuem conhecimento suficiente para realizar consultas diretamente no banco de dados e produzir relatórios ou análises.

Possuem maior autonomia, mas essa autonomia não deve significar acesso irrestrito.

Um analista que precisa analisar vendas, por exemplo, pode não precisar visualizar CPF, telefone ou informações de cartão dos clientes.

Usuários especialistas

São usuários com conhecimento técnico mais avançado, capazes de desenvolver consultas complexas, scripts e utilizar ferramentas de IA para apoiar análises.

O fato de um usuário ser especialista não significa que ele precise ter acesso a todas as informações.

Essa é uma questão importante para a segurança:

Conhecimento técnico e necessidade de acesso são conceitos diferentes.

O acesso deve ser determinado pela função exercida e pela necessidade real de utilização dos dados.

Usuários finais

São usuários que normalmente interagem com o banco de dados por meio de sistemas, sites ou aplicativos.

Nesse caso, o acesso aos dados é intermediado pela aplicação, proporcionando maior controle sobre as operações disponíveis.

---

1.4 Riscos da utilização de IA por usuários especialistas

A utilização de IA para gerar SQL pode trazer benefícios, mas também apresenta riscos que precisam ser considerados.

a) Consultas incorretas

A IA pode produzir uma consulta que seja válida do ponto de vista sintático, mas incorreta do ponto de vista lógico.

Por exemplo, pode realizar uma associação inadequada entre tabelas e produzir um relatório com resultados incorretos.

Esse problema é especialmente importante porque o usuário pode confiar no resultado apenas porque a consulta foi produzida por uma ferramenta de IA.

Por isso, consultas geradas automaticamente devem ser analisadas e validadas antes de serem utilizadas em decisões importantes.

b) Exposição de informações

 Outro risco é o envio de informações do banco para ferramentas externas de IA.

Um usuário pode, por exemplo, copiar uma estrutura de banco ou dados reais para uma ferramenta de IA com o objetivo de pedir ajuda para construir uma consulta.

Essa prática pode expor informações que deveriam permanecer dentro da organização.

Por esse motivo, a organização deve estabelecer regras claras sobre quais dados podem ser enviados para ferramentas externas.

c) Consultas com alto consumo de recursos

Uma consulta gerada automaticamente pode ser tecnicamente válida, mas apresentar baixo desempenho.

Uma consulta inadequada pode consumir muitos recursos do servidor, especialmente quando executada sobre grandes volumes de dados.

Por isso, consultas produzidas por IA não devem ser consideradas automaticamente otimizadas.

O DBA deve estabelecer mecanismos de controle e monitoramento para evitar que consultas inadequadas prejudiquem outros usuários e aplicações.

d) Acesso acima do necessário

Um dos maiores riscos ocorre quando a IA ou o usuário recebe permissões maiores do que realmente precisa.

Se uma conta utilizada por uma ferramenta de IA possuir acesso a todas as tabelas do banco, uma única consulta poderá expor informações que não fazem parte da finalidade da análise.

Essa situação contradiz o princípio do menor privilégio, segundo o qual o acesso deve ser limitado ao mínimo necessário para realizar a atividade.

1.5 Distribuição segura dos dados

A distribuição segura dos dados deve começar pela definição de quais informações cada usuário realmente necessita.

Nossa proposta utiliza cinco mecanismos principais:

1. Menor privilégio

Cada usuário, aplicação ou ferramenta deve receber somente os privilégios necessários para executar suas atividades.

O NIST define o princípio do menor privilégio como a restrição dos privilégios de usuários ou processos ao mínimo necessário para realizar suas tarefas.

2. Roles

Em vez de conceder permissões individualmente para cada usuário, a organização pode criar Roles relacionadas às funções existentes.

O PostgreSQL utiliza Roles para controlar o acesso aos objetos do banco. Uma Role pode representar um usuário ou um grupo e pode receber privilégios específicos.

Isso facilita a administração porque as permissões podem ser associadas às funções desempenhadas pelos usuários.

3. Views

As Views podem ser utilizadas para disponibilizar somente as informações necessárias para determinada atividade.

Por exemplo, um analista pode precisar conhecer a cidade e o estado dos clientes, mas não precisa conhecer o CPF ou o telefone.

Assim, uma View pode apresentar somente as colunas necessárias para a análise.

Entretanto, é importante destacar que uma View não deve ser considerada uma solução de segurança isolada. As permissões sobre a View e sobre os objetos relacionados também precisam ser configuradas corretamente. A documentação do PostgreSQL apresenta regras específicas sobre privilégios e segurança na utilização de Views.

4. Auditoria

Os acessos e operações importantes devem ser registrados e analisados.

A auditoria permite identificar comportamentos anormais, acessos indevidos e tentativas de extração excessiva de informações.

5. Separação de ambientes

Sempre que possível, atividades analíticas realizadas com auxílio de IA devem ocorrer em ambientes destinados à análise, como bancos de dados analíticos ou réplicas de leitura, em vez de permitir que a IA tenha acesso irrestrito ao banco de produção.

Essa separação reduz o risco de uma consulta analítica inadequada afetar diretamente sistemas que dependem do banco de produção.

---

1.6 Relação com a LGPD

A segurança do banco de dados também deve considerar a Lei Geral de Proteção de Dados (LGPD).

A LGPD estabelece princípios para o tratamento de dados pessoais, incluindo finalidade, adequação e necessidade. O princípio da necessidade determina que o tratamento deve ser limitado ao mínimo necessário para alcançar suas finalidades.

Esse princípio possui relação direta com o menor privilégio.

Por exemplo, se um analista precisa apenas conhecer a cidade dos clientes para realizar uma análise de vendas, não existe justificativa técnica para que ele receba também acesso ao CPF, telefone ou endereço completo.

Assim, limitar o acesso não é somente uma questão técnica de segurança, mas também uma medida relacionada à proteção de dados pessoais.

---

1.7 Análise crítica: permitir ou proibir a IA?

Existem duas alternativas extremas para o problema analisado.

Alternativa 1: Proibir a utilização de IA

Uma organização poderia simplesmente proibir seus funcionários de utilizar ferramentas de IA para trabalhar com bancos de dados.

Essa abordagem pode reduzir determinados riscos, mas também apresenta desvantagens.

A IA pode trazer ganhos de produtividade e auxiliar profissionais em tarefas de desenvolvimento e análise. Além disso, uma proibição absoluta pode estimular o uso de ferramentas não autorizadas, dificultando o controle pela organização.

Alternativa 2: Permitir acesso irrestrito à IA

A segunda alternativa seria permitir que usuários e ferramentas de IA tenham acesso amplo ao banco de dados.

Essa abordagem oferece grande autonomia, mas cria riscos significativos.

Uma IA com acesso irrestrito poderia consultar informações que o usuário não deveria visualizar ou executar consultas que consumam recursos excessivos.

Alternativa defendida pelo grupo

Nossa posição é que nenhuma das duas alternativas extremas é a melhor solução.

A organização deve permitir a utilização da IA, mas estabelecer uma arquitetura de segurança capaz de limitar os riscos.

Essa decisão está alinhada à ideia de gerenciamento de riscos apresentada pelo NIST, que propõe identificar, avaliar e gerenciar riscos relacionados à IA em vez de simplesmente ignorar ou aceitar esses riscos.

Portanto, a IA deve ser considerada uma ferramenta auxiliar, e não uma autoridade sobre o banco de dados.

---

1.8 Arquitetura de defesa em camadas

A arquitetura proposta pelo grupo pode ser representada da seguinte maneira:

Usuário Especialista
        |
        v
Ferramenta de IA
        |
        v
Camada de Controle
(Roles + Permissões)
        |
        v
Views / Dados Tratados
        |
        v
Banco Analítico ou Réplica de Leitura
        |
        v
Monitoramento e Auditoria

O ponto principal dessa arquitetura é impedir que a IA tenha acesso direto e irrestrito às tabelas brutas do banco de produção.

A IA pode auxiliar na construção da consulta, mas o banco continua sendo protegido por mecanismos de autorização e controle.

---

2. Exemplo Prático em PostgreSQL

Considere uma empresa que possui uma tabela "clientes" com informações como:

- "id_cliente";
- "nome";
- "cpf";
- "telefone";
- "endereco";
- "cidade";
- "estado";
- "data_cadastro".

Um analista precisa utilizar IA para analisar a distribuição dos clientes por cidade e estado.

Ele não precisa ter acesso ao CPF, telefone ou endereço.

Uma solução seria criar uma Role específica e uma View contendo somente os dados necessários.

-- 1. Criação da Role utilizada pelo analista
CREATE ROLE analista_ia LOGIN;

-- 2. Criação de uma View com somente os dados necessários
CREATE VIEW clientes_visiveis AS
SELECT
    id_cliente,
    cidade,
    estado,
    data_cadastro
FROM clientes;

-- 3. Permissão para utilizar o schema
GRANT USAGE ON SCHEMA public TO analista_ia;

-- 4. Permissão de leitura somente sobre a View
GRANT SELECT ON clientes_visiveis TO analista_ia;

-- 5. Garantia de que a Role não possui acesso direto à tabela original
REVOKE ALL ON clientes FROM analista_ia;

No PostgreSQL, o comando "GRANT" permite conceder privilégios específicos, enquanto "REVOKE" pode ser utilizado para retirar privilégios anteriormente concedidos.

Nesse cenário, o usuário pode consultar:

SELECT cidade, estado, COUNT(*)
FROM clientes_visiveis
GROUP BY cidade, estado;

Porém, ele não deve possuir permissão para executar:

SELECT cpf, telefone, endereco
FROM clientes;

Esse exemplo demonstra o princípio do menor privilégio na prática: o usuário recebe acesso somente às informações necessárias para sua atividade.

---

2.1 Por que essa solução é melhor?

A solução proposta apresenta uma combinação de segurança e produtividade.

O usuário continua podendo utilizar IA para construir consultas e realizar análises, mas a quantidade de informações disponíveis é limitada.

Se a IA gerar uma consulta inadequada tentando acessar uma coluna que não está disponível na View, o próprio controle de permissões do banco impede o acesso, desde que a configuração das permissões esteja correta.

Isso demonstra um princípio importante:

A segurança não deve depender somente de o usuário ou a IA fazer a coisa certa. Ela deve ser construída no próprio ambiente do banco de dados.

2.2 Limitações da solução

Apesar das vantagens, a solução não elimina todos os riscos.

Uma View mal configurada pode não oferecer a proteção esperada. Da mesma forma, uma Role com privilégios excessivos pode permitir acesso indevido.

Além disso, consultas autorizadas ainda podem consumir muitos recursos.

Por isso, a segurança deve ser tratada como um conjunto de mecanismos e não como uma única tecnologia.

O NIST destaca justamente a importância de uma abordagem de gerenciamento de riscos para sistemas de IA, considerando diferentes etapas e diferentes tipos de risco.

3. Conclusão

A utilização de Inteligência Artificial em bancos de dados apresenta oportunidades importantes para aumentar a produtividade de usuários especialistas e facilitar a criação de consultas SQL.

Entretanto, a facilidade proporcionada pela IA não significa que ela deva receber acesso irrestrito aos dados.

A análise realizada neste trabalho demonstra que a melhor estratégia é permitir o uso da IA dentro de uma arquitetura controlada. Essa arquitetura deve utilizar o princípio do menor privilégio, Roles, Views, permissões específicas, auditoria e, quando possível, separação entre ambientes de produção e análise.

Também foi possível observar que o papel do DBA continua sendo fundamental. Com a utilização de IA, o DBA passa a ter ainda mais importância na definição das políticas de acesso, segurança, desempenho e governança.

Outro ponto importante é que o nível de conhecimento de um usuário não deve determinar sozinho o nível de acesso aos dados. Um usuário especialista pode possuir grande conhecimento técnico e, mesmo assim, não necessitar de acesso a informações pessoais ou confidenciais.

Portanto, a posição defendida pelo grupo é que a IA não deve substituir o controle do DBA nem receber privilégios superiores aos necessários. Ela deve funcionar como uma ferramenta auxiliar dentro de uma arquitetura de segurança definida pela organização.

Dessa forma, é possível aproveitar os benefícios da Inteligência Artificial sem abandonar os princípios de segurança, privacidade, governança e proteção dos dados.

4. Referências

AUTIO, Chloe; SCHWARTZ, Reva; DUNIETZ, Jesse; JAIN, Shomik; STANLEY, Martin; TABASSI, Elham; HALL, Patrick; ROBERTS, Kamie. Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile. NIST AI 600-1. National Institute of Standards and Technology, 2024. Disponível em: https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence. Acesso em: 16 ago. 2026.

NATIONAL INSTITUTE OF STANDARDS AND TECHNOLOGY (NIST). Least Privilege. Computer Security Resource Center Glossary. Disponível em: https://csrc.nist.gov/glossary/term/least_privilege. Acesso em: 16 ago. 2026.

POSTGRESQL GLOBAL DEVELOPMENT GROUP. PostgreSQL Documentation: Database Roles. PostgreSQL 18. Disponível em: https://www.postgresql.org/docs/18/user-manag.html. Acesso em: 16 ago. 2026.

POSTGRESQL GLOBAL DEVELOPMENT GROUP. PostgreSQL Documentation: Privileges. PostgreSQL 18. Disponível em: https://www.postgresql.org/docs/current/ddl-priv.html. Acesso em: 16 ago. 2026.

POSTGRESQL GLOBAL DEVELOPMENT GROUP. PostgreSQL Documentation: CREATE VIEW. PostgreSQL 18. Disponível em: https://www.postgresql.org/docs/current/sql-createview.html. Acesso em: 16 ago. 2026.

BRASIL. Lei nº 13.709, de 14 de agosto de 2018 — Lei Geral de Proteção de Dados Pessoais (LGPD). Brasília, DF. Disponível em: https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm. Acesso em: 16 ago. 2026.
