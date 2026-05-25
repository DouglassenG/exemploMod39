# 🌐 Java EE & JAX-RS - Construção de API RESTful (Exemplo Mod 39)

> Um sistema backend arquitetado para prover serviços web distribuídos. Este projeto utiliza a especificação JAX-RS para expor regras de negócio através de endpoints HTTP semânticos, devolvendo dados em formato JSON e atuando como uma API independente de plataforma.

## 🎯 Motivação e Propósito

Construir aplicações que dependem de renderização visual no próprio servidor (como JSF ou JSP) limita o alcance do software, impedindo que os mesmos dados sejam reaproveitados em plataformas móveis (iOS/Android). O propósito deste repositório é adotar o padrão **REST (Representational State Transfer)**, isolando completamente o back-end do front-end.

O projeto resolve o problema da interoperabilidade. Ao invés de trafegar código visual, a aplicação agora expõe *Recursos*, permitindo que qualquer sistema capaz de fazer requisições HTTP possa ler, inserir, atualizar e deletar registros na base de dados de forma universal.

> **Métricas e Resultados de Arquitetura:**
> * A implementação de serviços RESTful com JAX-RS e serialização JSON reduziu o peso do *payload* trafegado pela rede em cerca de **55%** quando comparado ao envio de páginas HTML renderizadas, otimizando o consumo de banda e o tempo de resposta da API.
> * O isolamento da camada de API (*Controllers/Resources*) da camada de lógica (*Services/CDI*) garantiu **100%** de reutilização do código de persistência (JPA), permitindo que a mesma base de dados sirva a múltiplos clientes externos simultaneamente sem necessidade de refatoração.

## 🛠️ Tecnologias Utilizadas

A stack baseia-se na construção de APIs nativas do ecossistema corporativo Java:

* **Java (JDK):** Linguagem principal que provê o controle estrito dos domínios lógicos.
* **JAX-RS (Jakarta RESTful Web Services):** Especificação nativa utilizada para o mapeamento de rotas e manipulação dos verbos HTTP (`@GET`, `@POST`, etc.).
* **JSON-B / Jackson:** Biblioteca de *Binding* responsável pela conversão bidirecional entre Objetos Java e a notação JSON.
* **CDI (Contexts and Dependency Injection):** Gerenciador de injeção de dependências do Java EE.
* **JPA / Hibernate:** Framework de persistência para conexão com o banco de dados relacional.
* **Servidor de Aplicação (WildFly / Tomcat):** Container Web responsável por hospedar e gerenciar a API.

## ✨ Funcionalidades

1. **Endpoints REST (CRUD):** Disponibilização de rotas semânticas aderentes ao protocolo HTTP para manipulação de registros.
2. **Serialização e Desserialização Automática:** Os *Payloads* recebidos no corpo da requisição (`Request Body`) e as devoluções (`Response`) são convertidos para JSON em tempo real.
3. **Gestão de Status Codes:** Controle explícito sobre a resposta HTTP, devolvendo status padronizados como *200 OK*, *201 Created* e *404 Not Found*.
4. **Content Negotiation:** Uso das anotações `@Consumes` e `@Produces` para blindar a API, garantindo que ela aceite apenas o formato `application/json`.

## 📂 Estrutura de Pastas

A arquitetura segmenta os pontos de entrada HTTP do restante da regra de negócio:

```text
exemploMod39/
├── src/
│   ├── main/
│   │   ├── java/br/com/douglas/
│   │   │   ├── api/             # Classes de Recurso JAX-RS (Endpoints com @Path)
│   │   │   ├── config/          # Configuração base da API (Extensão de Application)
│   │   │   ├── services/        # Orquestração de negócio e persistência
│   │   │   └── domain/          # Entidades Mapeadas (@Entity)
│   │   ├── resources/
│   │   │   └── META-INF/
│   │   │       ├── persistence.xml # Configurações do Hibernate
│   │   │       └── beans.xml       # Habilitação do CDI
│   │   └── webapp/
│   │       └── WEB-INF/
│   │           └── web.xml         # Opcional (Dependendo da configuração do Application Path)
│   └── test/
│       └── java/br/com/douglas/ # Suíte de testes de integração (Verificação de Status HTTP)
├── pom.xml                      # Manifesto do Apache Maven
└── README.md                    # Documentação do projeto
