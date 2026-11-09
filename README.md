# Raízes do Nordeste — Sabores da nossa terra

Neste projeto, montei uma demonstração de site para uma rede de lanchonetes de comida nordestina. A pessoa pode escolher entre três formas de atendimento: celular (App), Totem e Web. Também pode consultar o cardápio de cada unidade, montar um pedido, testar cupons e pontos e ver como seria o pagamento.

> **Importante:** esta é uma demonstração de front-end. Ainda não tem servidor, banco de dados da empresa, login real ou pagamento de verdade. Pix, cartão e atualização do pedido são apenas simulações. Não use dados pessoais ou financeiros reais.

## Arquivos

- `index.html`: aplicação demonstrativa, sem dependências externas.
- `README.md`: documentação técnica e instruções de execução/publicação.
- [`docs/diagramas/casos_uso.png`](docs/diagramas/casos_uso.png): diagrama de casos de uso.
- [`docs/diagramas/jornada_usuario.png`](docs/diagramas/jornada_usuario.png): jornada multicanal do usuário.
- [`docs/diagramas/arquitetura.png`](docs/diagramas/arquitetura.png): arquitetura proposta para uma versão futura.
- [`docs/wireframes/wireframe_mobile.png`](docs/wireframes/wireframe_mobile.png): telas simplificadas para celular.
- [`docs/wireframes/wireframe_desktop.png`](docs/wireframes/wireframe_desktop.png): telas simplificadas para computador.
- O relatório acadêmico em PDF é entregue separadamente no AVA, conforme o roteiro da atividade; ele não faz parte da publicação do site.

## 1. Problema e contexto

Como a rede pode ter lojas em cidades diferentes, os preços e alguns produtos podem mudar de uma unidade para outra. Também é importante que o cliente consiga fazer o pedido por canais diferentes e que a empresa tenha cuidado com os dados pessoais. Por isso, comecei a demonstração pela escolha da unidade e do canal.

**Ideia principal:** deixar o cliente consultar o cardápio da unidade, montar o pedido, conhecer os pontos de fidelidade e entender quais informações ficam salvas durante a demonstração.

## 2. Canais

| Canal | Uso esperado | Comportamento na demonstração |
|---|---|---|
| App / móvel | Cliente em celular | Layout estreito, navegação inferior e fluxo de pedido; não é PWA instalável nesta versão. |
| Totem | Autoatendimento na loja | Tipografia e botões maiores; permite pedido sem cadastro e somente retirada. |
| Web | Desktop/tablet | Área maior e grade de produtos mais ampla. |

O seletor no topo permite mudar de canal para testar as diferenças. Usei o mesmo arquivo para os três formatos e fiz ajustes de tamanho e de algumas opções de acordo com o canal.

## 3. Requisitos funcionais

Legenda: **Implementado (mock)** = demonstrável localmente; **Planejado** = depende de back-end, serviço externo ou módulo que não existe nesta entrega.

| ID | Requisito | Situação | Evidência |
|---|---|---|---|
| RF-01 | Cadastro demonstrativo e gestão básica da conta | Implementado (mock) | Aba Conta; não há autenticação, sessão segura ou recuperação de senha. |
| RF-02 | Cardápio por unidade | Implementado | Seleção da unidade altera preços e disponibilidade. |
| RF-03 | Montagem de pedido | Implementado (mock) | Carrinho, quantidade, modalidade, cupons e total. Entrega não calcula frete nem endereço. |
| RF-04 | Acompanhamento de status | Implementado (mock) | Estados Recebido → Em preparo → Pronto → Entregue, avançados por temporizador local. |
| RF-05 | Solicitação de pagamento externo | Simulado | Opções Pix/cartão e retorno visual aprovado/recusado; nenhuma cobrança ou API real. |
| RF-06 | Fidelização | Implementado (mock) | Pontos, níveis e recompensas ilustrativas. |
| RF-07 | Promoções e campanhas | Parcial | Cupons BEMVINDO e FORRO10 são demonstrados; campanha de São João é conceitual. |
| RF-08 | Privacidade e direitos do titular | Parcial (mock) | Aviso, ciência, opção de marketing, visualização e exclusão local; não é operação LGPD de produção. |
| RF-09 | Pedido sem cadastro no Totem | Implementado (mock) | Checkout convidado com retirada, sem pontuação. |
| RF-10 | Gestão administrativa de cardápio/unidades | Planejado | As constantes de unidades e produtos são dados de demonstração, não um painel administrativo. |
| RF-11 | Painel de cozinha (KDS) | Planejado | Integração futura por eventos. |
| RF-12 | Notificações push/e-mail/SMS | Planejado | Dependem de serviço e eventos no back-end. |
| RF-13 | Cancelamento e estorno | Planejado | Dependem da API do gateway e regras transacionais. |

## 4. Requisitos não funcionais

| ID | Requisito | Atendimento nesta versão |
|---|---|---|
| RNF-01 | Mobile-first | CSS parte de uma coluna e amplia em telas maiores. |
| RNF-02 | Responsividade | Grid fluido, viewport e safe-area; layouts App, Totem e Web. Validar nos tamanhos indicados no plano de testes. |
| RNF-03 | Performance | HTML/CSS/JS sem bibliotecas externas, fontes externas ou chamadas de rede. |
| RNF-04 | Escalabilidade | Diretriz de arquitetura futura com serviços separados, cache e integração por API/eventos; não implementada. |
| RNF-05 | Acessibilidade | Semântica básica, rótulos e alvos maiores no Totem. A conformidade WCAG ainda requer auditoria e testes com teclado/leitor de tela. |
| RNF-06 | Segurança | Dados financeiros não são coletados. HTTPS, autenticação segura, tokens, criptografia e auditoria são requisitos para uma versão de produção, não recursos desta demo. |
| RNF-07 | Disponibilidade | A versão atual depende do navegador aberto e do armazenamento local; não há cache offline/PWA implementados. |
| RNF-08 | Privacidade | Coleta local mínima para demonstrar o fluxo, aviso de privacidade e marketing opcional. |
| RNF-09 | Manutenibilidade | Dados demonstrativos organizados em constantes; o código permanece em arquivo único para simplificar a atividade. |

## 5. Casos de uso e jornada

### Atores

- **Cliente App/Web:** consulta catálogo, seleciona unidade, monta carrinho, aplica cupom, usa fidelidade, cadastra-se na demonstração, solicita pagamento e acompanha pedido.
- **Cliente Totem:** consulta catálogo, monta carrinho e solicita pagamento sem cadastro, somente para retirada.
- **Atendente:** consulta informações do pedido; participação conceitual, sem painel nesta entrega.
- **Cozinha:** recebe o pedido e atualiza o preparo na arquitetura prevista; não existe painel da cozinha no protótipo.
- **Gerente / Administrador:** gerencia cardápio e promoções na arquitetura prevista; não existe painel administrativo no protótipo.
- **Sistema de pagamento externo:** integração futura; o retorno é apenas simulado nesta versão.

O diagrama mostra os cinco atores exigidos no roteiro: Cliente, Atendente, Cozinha, Gerente/Administrador e Sistema de Pagamento Externo. Consulte `docs/diagramas/casos_uso.png` e `docs/diagramas/jornada_usuario.png`.

Os wireframes em `docs/wireframes/` mostram o fluxo principal em telas de celular e computador, antes do acabamento visual. A descrição detalhada do caso de uso *Solicitar pagamento* está no relatório PDF.

## 6. Arquitetura-alvo e integração

Hoje, o site usa informações que estão no próprio código e no navegador. Para funcionar de verdade, os três canais precisariam conversar com um servidor por meio de uma API. Esse servidor guardaria os dados dos usuários, produtos, pedidos e pontos. O pagamento seria feito por um serviço especializado, e a cozinha receberia os pedidos por uma integração.

O desenho mostra uma ideia de como isso poderia ser feito no futuro. Nada disso está conectado nesta versão. Consulte `docs/diagramas/arquitetura.png`.

## 7. LGPD e privacidade

Tentei deixar o aviso de privacidade fácil de encontrar e separar a leitura do aviso da opção de receber promoções. O marketing é opcional. Na área Conta, a pessoa pode consultar o que ficou salvo, desmarcar as promoções e apagar os dados da demonstração naquele navegador. No Totem, não é necessário fazer cadastro.

Na demonstração, nome, e-mail, pedidos, pontos e preferências podem ficar salvos no próprio navegador, em um recurso chamado `localStorage`. A senha digitada não é guardada. O site não envia essas informações para um servidor. Pix e cartão são apenas telas de exemplo, e o QR Code não realiza pagamento.

Em um sistema real, a empresa ainda precisaria informar quem é responsável pelos dados, publicar a política completa, explicar por que coleta cada informação e por quanto tempo a guarda. Também precisaria proteger o acesso, atender pedidos dos titulares e validar as decisões com a equipe jurídica ou responsável pela privacidade. A interface sozinha não garante que uma empresa esteja em conformidade com a LGPD.

## 8. Plano de testes da interface

**Objetivo:** validar os fluxos críticos, as mensagens de erro, as variações entre unidades/canais, a responsividade e a clareza da privacidade.

**Ambiente utilizado nos testes relatados:** site publicado, navegador Chrome e três dimensões de tela: 375 × 812 (celular), 768 × 1024 (tablet) e 1366 × 900 (computador). Os testes com leitor de tela, navegação completa por teclado e zoom de 200% ainda são melhorias para uma próxima etapa.

| ID | Tipo | Procedimento realizado | Resultado esperado | Resultado |
|---|---|---|---|---|
| T01 | Positivo | Abrir o endereço público em janela anônima. | A página e o cardápio aparecem. | Aprovado |
| T02 | Positivo | Alternar entre App, Totem e Web. | Os três canais exibem suas interfaces. | Aprovado |
| T03 | Positivo | Comparar preços da carne de sol em Recife, Salvador e Fortaleza. | O preço muda conforme a unidade. | Aprovado |
| T04 | Negativo/positivo | Verificar Acarajé em Recife e em Salvador. | Indisponível em Recife, disponível em Salvador. | Aprovado |
| T05 | Negativo | Aplicar FORRO10 em 1 Baião de dois (R$ 34,90). | Desconto de R$ 0,00; total R$ 34,90. | Aprovado |
| T06 | Positivo | Aplicar FORRO10 em 2 Baiões de dois (R$ 69,80). | Desconto de R$ 10,00; total R$ 59,80. | Aprovado |
| T07 | Negativo | Informar e-mail inválido e senha de 3 caracteres; depois e-mail válido com senha curta. | Cadastro bloqueado em ambas as tentativas. | Aprovado |
| T08 | Negativo | Usar dados válidos sem marcar a ciência do aviso. | Cadastro bloqueado com orientação sobre o aviso. | Aprovado |
| T09 | Positivo | Abrir, fechar e reabrir o aviso de privacidade em Conta. | O aviso segue disponível para consulta. | Aprovado |
| T10 | Positivo | Fazer pedido simulado no Totem sem cadastro. | Pagamento permitido somente para retirada. | Aprovado |
| T11 | Negativo | Marcar pagamento recusado e tentar concluir. | Mensagem de recusa; sem novo pedido aprovado. | Aprovado |
| T12 | Positivo | Simular pagamento aprovado e consultar Pedidos. | Número de pedido criado e exibido no histórico. | Aprovado |
| T13 | Positivo | Conferir layouts em 375×812, 768×1024 e 1366×900. | Layout utilizável, sem cortes importantes. | Aprovado |
| T14 | Positivo | Testar botões principais e controles do Totem. | Botões utilizáveis e legíveis. | Aprovado |
| T15 | Positivo | Ganhar e usar pontos no carrinho em conta demonstrativa. | Desconto aplicado e saldo atualizado. | Aprovado |
| T16 | Positivo | Consultar dados, desativar marketing e excluir cadastro local. | Dados exibidos, marketing desativado e conta excluída. | Aprovado |

**Registro:** os 16 casos acima foram testados manualmente em 9 de novembro de 2026, com resultados informados como aprovados. As capturas selecionadas e o registro dos resultados estão no PDF acadêmico. Na consulta dos dados (T16), a tela usa JSON, funcional para demonstração, mas pouco amigável para um usuário final.

## 9. Como executar no computador

1. Baixe o repositório em ZIP e extraia os arquivos.
2. Abra `index.html` no Chrome ou Edge.
3. Use os botões App, Totem e Web para conferir as telas.

Não é necessário instalar programas adicionais. Para começar os testes com dados novos, use uma janela anônima ou limpe o armazenamento local do site.

## 10. Onde acessar o projeto

O site já está publicado no GitHub Pages, para que seja possível conhecer e testar as telas sem instalar nada.

**Site publicado:** [Abrir Raízes do Nordeste](https://samucahet.github.io/raizes-do-nordeste-Uninter/)

**Repositório:** [Ver os arquivos no GitHub](https://github.com/SamucaHET/raizes-do-nordeste-Uninter)

O repositório contém o arquivo `index.html`, este README e os diagramas e wireframes do trabalho. Para abrir o projeto no computador, também é possível baixar os arquivos e abrir `index.html` no navegador.

Não há pagamento real, cadastro com autenticação ou comunicação com servidor. Esses fluxos são demonstrados no próprio navegador, conforme explicado nas seções anteriores.

## 11. Limitações e melhorias futuras

- Implementar API e banco de dados reais para identidade, catálogo, pedidos, pagamento e fidelidade.
- Integrar gateway de pagamento em sandbox, com tokenização e confirmação autenticada por webhook.
- Implementar autenticação, recuperação de senha, autorização e gestão de sessão.
- Persistir consentimentos com registro de data, finalidade, versão do aviso e revogação.
- Criar painel administrativo, KDS e notificações.
- Implementar PWA (manifest, service worker, estratégia de cache e atualização).
- Criar endereço de entrega, cálculo de frete, cancelamento e estorno.
- Automatizar testes, medir performance e fazer auditoria de acessibilidade (incluindo teclado e leitor de tela).

## 12. Conclusão

Ao montar o projeto, procurei deixar claro como o cliente escolheria a unidade, consultaria os produtos e faria o pedido em cada canal. Também incluí o totem sem cadastro, as promoções, os pontos e o aviso sobre os dados.

Durante a atividade, ficou mais claro para mim que o front-end é só a parte que aparece na tela. Para o sistema funcionar de verdade, ainda seria necessário criar o back-end, ligar o pagamento a um serviço externo e guardar os pedidos e os pontos em um banco de dados. Os testes ajudam a encontrar problemas antes de uma entrega, e a LGPD precisa ser pensada desde o começo.

Esta versão é uma demonstração do que consegui montar com HTML, CSS e JavaScript. Ainda não está pronta para uma lanchonete usar no dia a dia, mas serve para mostrar a ideia e o que precisaria ser desenvolvido nas próximas etapas.

## Referências

- ASSOCIAÇÃO BRASILEIRA DE NORMAS TÉCNICAS. **ABNT NBR 14724:2024: informação e documentação — trabalhos acadêmicos — apresentação**. Rio de Janeiro: ABNT, 2024. Consultar a versão corrigida disponível pelo acesso institucional.
- ASSOCIAÇÃO BRASILEIRA DE NORMAS TÉCNICAS. **ABNT NBR 6023:2025: informação e documentação — referências — elaboração**. Rio de Janeiro: ABNT, 2025.
- BRASIL. **Lei nº 13.709, de 14 de agosto de 2018**. Lei Geral de Proteção de Dados Pessoais (LGPD). Texto atualizado. Disponível em: https://www2.camara.leg.br/legin/fed/lei/2018/lei-13709-14-agosto-2018-787077-normaatualizada-pl.html. Acesso em: 9 nov. 2026.
- GITHUB. **Creating a GitHub Pages site**. GitHub Docs. Disponível em: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site. Acesso em: 9 nov. 2026.
- W3C. **Web Content Accessibility Guidelines (WCAG) 2.2**. Web Accessibility Initiative. Disponível em: https://www.w3.org/WAI/standards-guidelines/wcag/. Acesso em: 9 nov. 2026.

---

**Entrega acadêmica:** o PDF do projeto é enviado separadamente pelo AVA da Uninter.
