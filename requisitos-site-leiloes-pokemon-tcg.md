# Requisitos de Software — Site de Leilões de Cartas Pokémon TCG

## 1. Objetivo

Desenvolver uma plataforma web de leilões exclusiva para cartas de Pokémon TCG. Somente o administrador poderá cadastrar e vender cartas. Usuários cadastrados e aprovados poderão acompanhar os leilões, realizar lances e conversar com o administrador após vencerem um leilão.

O sistema não processará pagamentos nem organizará fretes. Esses detalhes deverão ser combinados fora da plataforma, pelo chat interno disponibilizado ao fim do leilão.

## 2. Tecnologias obrigatórias

- Linguagem: Python.
- Framework web: Django.
- Banco de dados: PostgreSQL.

O Django deve concentrar a autenticação, o controle de permissões, as regras de negócio e o gerenciamento de usuários, cartas, leilões, lances e mensagens.

## 3. Perfis de acesso

| Perfil | Permissões |
| --- | --- |
| Visitante | Visualizar leilões e detalhes públicos das cartas. |
| Usuário cadastrado pendente | Aguardar aprovação; não pode realizar lances. |
| Usuário aprovado | Dar lances, consultar seus lances e leilões vencidos, e usar o chat após vencer. |
| Administrador | Gerenciar usuários, cartas, leilões, lances e conversas. |

## 4. Requisitos funcionais

### 4.1 Cadastro e autenticação

- O sistema deve permitir cadastro, login e logout de usuários.
- Todo novo cadastro deve ficar com status pendente até aprovação do administrador.
- O administrador deve poder aprovar ou rejeitar usuários cadastrados.
- Apenas usuários aprovados podem realizar lances.
- Cada usuário deve ter uma área para consultar seus lances e leilões vencidos.

### 4.2 Cadastro de cartas

- Apenas o administrador pode cadastrar e editar cartas.
- Os campos obrigatórios de uma carta são:
  - Nome;
  - Imagem;
  - Código.
- O sistema deve permitir os seguintes campos opcionais:
  - Coleção;
  - Número;
  - Idioma;
  - Raridade;
  - Condição;
  - Versão;
  - Descrição;
  - Observações sobre defeitos.

### 4.3 Gerenciamento de leilões

- O administrador deve poder criar, editar, publicar, pausar, cancelar e encerrar leilões.
- Cada leilão deve possuir, no mínimo:
  - Carta vinculada;
  - Valor inicial;
  - Incremento mínimo entre lances;
  - Data e hora de início;
  - Data e hora de encerramento;
  - Status do leilão.
- O incremento mínimo deve ser definido individualmente pelo administrador em cada leilão.
- A página inicial deve apresentar os leilões ativos.
- Cada item de leilão deve mostrar imagem, nome, código da carta, lance atual e tempo restante.
- A página de detalhe deve apresentar todas as informações da carta, maior lance, histórico de lances e tempo restante.
- O leilão deve encerrar exatamente no horário configurado, sem extensão automática quando houver lances próximos do fim.
- Ao encerrar o leilão, o sistema deve identificar automaticamente o maior lance válido e definir seu autor como vencedor.

### 4.4 Lances

- Apenas usuários aprovados podem realizar lances em leilões ativos.
- Todos os usuários devem poder visualizar o maior lance atual e o nome de usuário de quem o realizou.
- O histórico de lances deve apresentar nome do usuário, valor, data e hora de cada lance.
- O sistema deve aceitar somente lances iguais ou superiores ao valor do maior lance atual acrescido do incremento mínimo definido para o leilão.
- Lances enviados não podem ser editados ou cancelados.
- O sistema não deve oferecer lances automáticos.
- O sistema deve bloquear novos lances quando o leilão estiver encerrado, pausado ou cancelado.

### 4.5 Chat interno

- O chat interno deve ser liberado apenas após o encerramento do leilão.
- Cada conversa deve conectar exclusivamente o administrador e o vencedor do respectivo leilão.
- O chat deve permitir a troca de mensagens para combinação de pagamento e entrega.
- O administrador deve poder consultar todas as conversas vinculadas aos leilões.

### 4.6 Informações e avisos

- O sistema deve informar claramente que pagamento e frete não são processados nem organizados pela plataforma.
- Ao término de um leilão, o administrador e o vencedor devem receber uma notificação ou aviso no sistema sobre o resultado e a abertura do chat.

## 5. Páginas obrigatórias

- Página inicial com a lista de leilões ativos.
- Página de detalhes do leilão.
- Página de login e cadastro.
- Área **Meus lances**.
- Área **Leilões vencidos**.
- Página de chat interno.
- Painel administrativo.

## 6. Regras de negócio

- A plataforma é exclusiva para cartas de Pokémon TCG.
- Somente o administrador pode anunciar e vender cartas.
- O usuário deve ser aprovado pelo administrador para dar lances.
- O maior lance válido no momento exato do encerramento define o vencedor.
- O nome de usuário de cada participante que realizou um lance é público no histórico.
- O incremento mínimo é definido por leilão pelo administrador.
- Não existe extensão automática do prazo do leilão.
- Lances não podem ser alterados ou removidos após o envio.
- Não existem lances automáticos.
- Pagamento, entrega e frete são responsabilidade do administrador e do vencedor, fora da plataforma.

## 7. Requisitos não funcionais

- A interface deve ser moderna, clara e responsiva para celular e computador.
- Senhas devem ser armazenadas de forma segura utilizando os mecanismos de autenticação do Django.
- O sistema deve controlar permissões conforme o perfil do usuário.
- O banco PostgreSQL deve armazenar usuários, aprovações, cartas, leilões, lances, vencedores e mensagens de chat.
- As informações de lance e tempo restante devem ser atualizadas rapidamente na interface.
- O sistema deve registrar data e hora de lances de forma confiável.
- Ações críticas do administrador, como cancelar ou encerrar um leilão, devem solicitar confirmação antes da execução.
