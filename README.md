# GoStack — aplicações web, mobile e APIs

Coleção de exercícios e desafios da formação **GoStack, da Rocketseat**, com Node.js, React, React Native e TypeScript. O repositório registra a evolução dos fundamentos HTTP até uma API de agendamentos organizada em rotas, modelos e repositório.

## Navegação e tecnologias

| Diretório | Conteúdo |
| --- | --- |
| [Backend introdutório](LV_01/backend) | Express 4, CORS, UUID e CRUD de projetos em memória. |
| [Frontend](LV_01/frontend) | React 16, Axios, Babel e Webpack 4. |
| [Mobile](LV_01/mobile) | React Native 0.63.4, Axios e projetos nativos Android/iOS. |
| [Desafios](LV_01/challenges) | Exercícios separados de Node, React e React Native, com configuração de testes. |
| [Conceitos de TypeScript](LV_01/concepts/Typescript) | Exemplos introdutórios com TypeScript e Express. |
| [API de agendamentos](LV_02/primeiro_projeto_node) | Express, TypeScript 4.1, date-fns, UUID e repositório em memória. |

Cada diretório com `package.json` é um projeto independente. Não existe um comando único de instalação ou teste na raiz.

## Arquitetura e fluxo de agendamento

Na API do nível 2, `server.ts` configura JSON e registra as rotas. `appointments.routes.ts` recebe `provider` e `date`, converte a data e normaliza para o início da hora. O repositório verifica se o mesmo prestador já tem um horário igual e armazena os agendamentos em um array.

- `GET /appointments`: lista os agendamentos na propriedade `Appointments`.
- `POST /appointments`: cria e retorna `Appointment`; conflito de horário para o mesmo prestador retorna HTTP 400.
- Os dados são perdidos ao reiniciar o processo. Não há banco nem autenticação nesse fluxo.

## Executar a API de agendamentos

Pré-requisitos: Git, Node.js e npm compatíveis com as dependências legadas. A versão do Node não está fixada no repositório; valide a combinação antes de atualizar pacotes. As versões de React Native também exigem ferramentas nativas compatíveis.

```bash
git clone https://github.com/fernandojs8/GoStack.git
cd GoStack/LV_02/primeiro_projeto_node
npm install
npm run dev:server
```

A API escuta em `http://localhost:3333`. Exemplo em outro terminal:

```bash
curl -X POST http://localhost:3333/appointments   -H 'Content-Type: application/json'   -d '{"provider":"demo","date":"2030-01-15T10:00:00Z"}'
curl http://localhost:3333/appointments
```

Repita o POST para verificar o conflito. `npm run build` executa o compilador TypeScript; não há script `test` nesse projeto.

Para o CRUD introdutório, execute `npm install` e `npm run dev` dentro de `LV_01/backend`. Para o frontend introdutório, os mesmos comandos devem ser executados em `LV_01/frontend`. Confira a URL da API usada por cada cliente antes de integrar os projetos.

## Testes existentes

Após instalar as dependências **dentro do projeto escolhido**:

| Projeto | Comando |
| --- | --- |
| `LV_01/challenges/Node_Challenge_lvl01` | `npm test` — Jest e Supertest. |
| `LV_01/challenges/React_Challenge_lvl01` | `npm test` — react-scripts e Testing Library. |
| `LV_01/challenges/ReactNative_Challenge_lvl01` | `npm test` — Jest com preset React Native. |
| `LV_01/mobile` | `npm test` — Jest com preset React Native. |

**Validação desta revisão:** scripts, rotas e dependências foram conferidos por leitura estática. Instalação, build e testes não foram executados; não há resultado ou cobertura medidos aqui.

## Limitações e evolução proposta

- Persistência em memória, validação de entrada limitada e ausência de autenticação na API de agendamentos.
- Dependências históricas e ferramentas diferentes entre os exercícios; não assumir compatibilidade direta com os runtimes mais recentes.
- O script `build` do frontend introdutório inicia o servidor de desenvolvimento; ele não demonstra geração de um artefato de produção.
- Próximos passos: fixar runtime, atualizar dependências com testes, adicionar validação de datas, testes de conflito e persistência com garantia de unicidade.
- Para demonstrar cloud: criar Dockerfile e CI, publicar uma API de demonstração com dados fictícios e registrar logs, health check e procedimento de deploy. Esses itens são propostas, não entregas existentes.

## Origem e licença

Estudos da Rocketseat/GoStack. Código sob [MIT](LICENSE).
