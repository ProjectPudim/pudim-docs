---
cover: ../../../assets/pudim-banner.png
coverY: 0
---

# Política de Privacidade

**Última atualização:** 31 de outubro de 2026

Esta política explica quais dados o **Pudim** coleta, para que usa, onde guarda, por quanto tempo e como você pode pedir a remoção. Ela vale junto com os [Termos de Serviço](service.md).

No Fluxer, bots recebem o conteúdo das mensagens dos canais que conseguem ver. Por isso queremos ser claros sobre o que o Pudim faz com isso.

## Resumo

- O Pudim **lê as mensagens** apenas para detectar comandos e menções a ele. **Ele não guarda o conteúdo das mensagens** em banco de dados.
- O Pudim guarda somente **configurações do servidor, advertências e menus de cargos por reação**, além de IDs necessários para essas funções.
- O Pudim **não envia DMs**, **não usa voz** e **não grava áudio**.
- O Pudim **não vende** dados e **não os usa para anúncios ou perfis**.
- Você pode pedir a remoção dos seus dados a qualquer momento (veja a seção 10).

## 1. Quais dados o Pudim guarda

### 1.1 Banco de dados (MongoDB)

| O que é guardado | Dados | Para quê | Por quanto tempo |
| --- | --- | --- | --- |
| **Configuração do servidor** | ID do servidor, prefixo, cargos do cargo automático (ID do cargo e se está ativo), regras de ações automáticas por advertência (quantidade, tipo de ação, duração, ID do canal) e ID do canal de logs de advertências | Fazer o bot funcionar do jeito que o servidor configurou | Enquanto o servidor usar o bot, ou até pedido de remoção |
| **Advertências** | ID do servidor, ID do membro advertido, ID do moderador, **motivo escrito pelo moderador**, ID da advertência e data | Histórico de moderação (`warn`, `warnings`, `unwarn`, `clearwarns`) e ações automáticas | Até um moderador remover a advertência (`unwarn` ou `clearwarns`), ou até pedido de remoção |
| **Menus de cargos por reação** | ID da mensagem, ID do canal, ID do servidor, ID de quem criou o menu, emojis usados e qual cargo cada emoji dá | Entregar cargos quando alguém reage | Até o menu ser removido pelo servidor, ou até pedido de remoção |
| **Preferência de idioma** | ID do usuário e idioma escolhido (padrão: português do Brasil) | Responder no idioma certo | Até pedido de remoção |

### 1.2 Cache temporário (Valkey/Redis)

O Pudim usa um cache para responder mais rápido. Ele guarda cópias de dados que já existem no banco, **por pouco tempo**:

| Dado em cache | Duração |
| --- | --- |
| Prefixo do servidor | 1 hora |
| Idioma do usuário | 5 minutos |
| Estado de menus interativos | 10 minutos (menus temporários) ou 1 hora (menus de cargos por reação) |

O cache também é usado para avisar o bot de que o prefixo de um servidor mudou.

### 1.3 Dados que o bot lê, mas não guarda

Para funcionar, o Pudim recebe informações do Fluxer, como ID e nome de usuário de quem usa um comando, IDs de servidores, canais e cargos, e a lista de cargos de um membro. Esses dados são usados **no momento** do comando e **não são gravados** em banco, salvo o que está descrito na seção 1.1.

## 2. Conteúdo de mensagens

- O Pudim lê as mensagens recebidas para saber se começam com o prefixo de um comando ou se mencionam o bot. Depois disso, a mensagem **não é salva**.
- As mensagens **não são armazenadas** em banco de dados nem enviadas a serviços externos.
- **Exceção, o comando `purge`:** ao apagar mensagens em massa, o Pudim lê as mensagens selecionadas e monta um arquivo de texto de backup (data, nome de usuário, conteúdo e links de anexos). Esse arquivo é **enviado no próprio canal** onde o comando foi usado, para a equipe de moderação. **O Pudim não guarda uma cópia desse arquivo.** A partir daí, o arquivo fica sob controle do servidor, e quem tiver acesso ao canal poderá vê-lo.
- **Comando `massrole`:** para aplicar um cargo a vários membros, o Pudim busca temporariamente a lista de membros do servidor (até 1000). A lista é usada só durante a execução do comando. **Ela não é salva, exportada nem compartilhada.**

## 3. Registro de entrada e saída de servidores

Quando o Pudim entra ou sai de um servidor, ele envia um aviso para um **canal privado de logs do desenvolvedor**, com:

- nome e ID do servidor;
- quantidade de membros;
- data de criação do servidor;
- nome de usuário e ID do dono do servidor;
- ícone do servidor.

Isso serve para acompanhar o crescimento do bot e investigar problemas. O aviso é enviado para a equipe do Pudim, **não** para o servidor.

## 4. Serviços externos

O Pudim se conecta aos serviços abaixo. **Nenhum deles recebe mensagens, IDs de usuários ou dados de servidores.**

| Serviço | Para quê | O que é enviado |
| --- | --- | --- |
| **Fluxer** (API e gateway) | Funcionamento do bot na plataforma | O necessário para executar comandos (ver seção 1.3) |
| **nekos.best** (`nekos.best/api/v2`) | Buscar imagens animadas dos comandos de interação (`hug`, `pat`, `slap` etc.) | Apenas o nome da ação. Como em qualquer conexão de internet, o serviço enxerga o IP do servidor onde o bot está hospedado |
| **Hospedagem (Discloud)** e **provedores de banco de dados e cache** | Manter o bot no ar e guardar os dados da seção 1 | Os dados da seção 1, armazenados na infraestrutura deles |

Se passarmos a usar outro serviço externo, esta lista será atualizada.

## 5. Voz

O Pudim **não tem recursos de voz**. Ele não entra em canais de voz e **não grava nem transmite áudio**. Os comandos `lock` e `unlock` apenas mudam permissões de canais de voz, como falar, e não acessam o áudio.

## 6. Mensagens privadas e contato com você

O Pudim **não envia DMs** e não entra em contato com usuários por conta própria. Ele só responde nos canais, em reação a comandos e interações.

## 7. O que não fazemos

- Não vendemos, alugamos nem compartilhamos dados com anunciantes.
- Não criamos perfis de usuários nem rastreamos você entre servidores.
- Não exportamos listas de membros nem raspamos dados de comunidades.
- Não coletamos dados sensíveis de propósito. Porém, o **motivo de uma advertência** é um texto livre escrito por moderadores. Peça aos moderadores do seu servidor que não coloquem dados pessoais sensíveis nele.

## 8. Compartilhamento

Seus dados só saem do Pudim nas situações abaixo:

- para os provedores de infraestrutura da seção 4, que armazenam os dados em nosso nome;
- quando a lei ou uma autoridade competente exigir;
- para proteger a segurança do bot, de usuários ou de servidores contra abuso.

Dentro de um servidor, as advertências e os logs de moderação podem ser vistos por quem tem acesso aos canais e comandos de moderação daquele servidor.

## 9. Segurança

Usamos medidas razoáveis para proteger os dados: o token do bot e as credenciais dos bancos ficam em variáveis de ambiente e não no código, e o acesso à infraestrutura é restrito. Nenhum sistema é 100% seguro, então não podemos garantir proteção absoluta.

## 10. Seus direitos e como remover seus dados

Você pode pedir:

- **acesso** aos dados que temos sobre você;
- **correção** de dados incorretos;
- **exclusão** de dados, como advertências recebidas, preferência de idioma ou menus criados por você;
- esclarecimentos sobre como tratamos seus dados.

**Donos de servidores** também podem pedir a exclusão de toda a configuração do servidor.

Para pedir, entre no [servidor de suporte](https://fluxer.gg/Ka4CXOqj) e fale com a equipe. Para localizarmos seus dados, informe o seu ID de usuário ou o ID do servidor.

**Advertências:** elas existem para a moderação do servidor. Se o seu servidor quiser remover uma advertência, os moderadores podem usar `unwarn` ou `clearwarns`. Se você pedir a exclusão e houver uma razão legítima para manter um registro (por exemplo, segurança ou cumprimento de obrigação legal), explicaremos o motivo.

Nós seguimos os direitos previstos na **Lei Geral de Proteção de Dados (LGPD, Lei 13.709/2018)**, quando aplicável.

## 11. Crianças e adolescentes

O Pudim não é direcionado a crianças. O uso do bot depende de você ter idade para usar o Fluxer, conforme as regras da plataforma. Se descobrirmos dados de alguém que não deveria estar usando o serviço, vamos removê-los quando possível.

## 12. Alterações nesta política

Podemos atualizar esta política. A data de "Última atualização" no topo mostra a versão atual. Mudanças importantes, como a coleta de novos tipos de dados, serão avisadas no servidor de suporte.

## 13. Contato

- **Servidor de suporte:** <https://fluxer.gg/Ka4CXOqj>