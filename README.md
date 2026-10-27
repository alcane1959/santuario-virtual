# Santuário Virtual - Acenda sua Vela

Aplicação web educacional que oferece um espaço virtual para publicação anônima de intenções, orações e pensamentos por meio de velas digitais com duração determinada.

## Sobre o projeto

O projeto apresenta um formulário para o visitante escrever uma mensagem opcional, escolher a duração da vela e publicá-la em um mural coletivo. As velas ainda válidas são carregadas do banco de dados e exibidas em cartões com chama animada.

A interface possui tema escuro, layout responsivo, animações em CSS, integração com Supabase, moderação local de conteúdo e um modal com termos de uso.

## Funcionalidades

- Publicação anônima de intenções ou orações.
- Campo de mensagem opcional com limite de 500 caracteres.
- Duração selecionável de 3, 7 ou 30 dias.
- Cálculo automático da data de expiração.
- Exibição apenas das velas que ainda não expiraram.
- Ordenação das publicações pelas mais recentes.
- Chama animada com CSS.
- Layout adaptável para diferentes tamanhos de tela.
- Moderação local de termos e padrões considerados incompatíveis.
- Bloqueio de links e de alguns formatos de dados pessoais.
- Modal com termos de uso e isenção de responsabilidade.
- Fechamento do modal pelo botão ou por clique na área externa.
- Integração com Supabase para armazenamento e consulta.

## Tecnologias utilizadas

- HTML5
- CSS3
- JavaScript Vanilla
- Supabase JavaScript SDK v2
- Supabase Database
- CSS Grid
- CSS Animations

## Estrutura do projeto

```text
santuario-virtual/
├── index.html
└── README.md
```

O projeto está concentrado em um único arquivo HTML, que contém a estrutura, os estilos e a lógica JavaScript da aplicação.

## Como executar

1. Baixe ou clone os arquivos do projeto.
2. Configure um projeto no Supabase.
3. Crie a tabela necessária no banco de dados.
4. Informe a URL e a chave pública anônima do projeto na configuração JavaScript.
5. Abra o `index.html` em um navegador moderno ou utilize um servidor HTTP local.

## Configuração do Supabase

A aplicação utiliza um cliente Supabase configurado no JavaScript:

```javascript
const SUPABASE_URL = 'SUA_URL_DO_SUPABASE';
const SUPABASE_KEY = 'SUA_CHAVE_PUBLICA_ANONIMA';
const _supabase = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);
```

> Não publique chaves privadas, chaves de serviço ou credenciais administrativas. A chave anônima usada no navegador deve estar protegida por políticas adequadas de Row Level Security.

## Estrutura esperada da tabela

A aplicação consulta e insere registros na tabela `candles`. Ela utiliza os campos abaixo:

| Campo | Finalidade |
|---|---|
| `message` | Mensagem ou intenção publicada pelo visitante |
| `duration_days` | Duração escolhida para a vela |
| `expires_at` | Data e hora de expiração |
| `created_at` | Data e hora de criação usada na ordenação |

A configuração exata dos tipos, valores padrão e políticas de acesso deve ser definida no painel do Supabase conforme os requisitos do ambiente.

## Fluxo de funcionamento

1. Ao abrir a página, a função `loadCandles()` consulta as velas ainda válidas.
2. Os registros são ordenados por `created_at` em ordem decrescente.
3. A função `renderCandles()` cria visualmente os cartões do mural.
4. No envio do formulário, a mensagem passa pela moderação local.
5. Se aprovada, a aplicação calcula `expires_at` e insere o registro em `candles`.
6. Após a publicação, o campo da mensagem é limpo e o mural é atualizado.

## Moderação de conteúdo

Antes da publicação, o texto é normalizado e comparado com:

- lista local de termos bloqueados;
- expressões regulares para padrões incompatíveis;
- possíveis links externos;
- alguns formatos de telefone, CPF, CNPJ e meios de contato;
- conteúdo ofensivo, discriminatório, violento, fraudulento, político ou promocional.

A moderação executada no navegador é apenas uma camada inicial. Em uma implantação pública, recomenda-se complementar a validação no banco de dados ou em uma função de servidor, porque regras presentes somente no front-end podem ser contornadas.

## Segurança e privacidade

- Não solicite nome, e-mail ou outros dados pessoais sem necessidade.
- Configure Row Level Security no Supabase.
- Permita somente as operações indispensáveis à aplicação.
- Valide e sanitize dados também no servidor.
- Evite renderizar conteúdo do usuário por meio de HTML não confiável.
- Mantenha credenciais administrativas fora do código-fonte.
- Defina procedimentos de moderação e remoção de conteúdo.

## Termos de uso

A aplicação apresenta um modal informando que o espaço se destina à manifestação de fé, oração, reflexão e boas intenções. Também estabelece responsabilidade do usuário pelo conteúdo publicado, proibição de mensagens inadequadas e possibilidade de remoção de conteúdo.

## Compatibilidade

A aplicação requer:

- navegador moderno com JavaScript habilitado;
- conexão com a internet para carregar o SDK do Supabase;
- acesso ao projeto Supabase configurado.

## Personalização

As cores principais podem ser alteradas nas variáveis CSS:

```css
:root {
  --bg-color: #0b0b12;
  --card-bg: #161623;
  --text-color: #e0e0e0;
  --flame-color: #ff9d00;
  --flame-glow: #ff5500;
}
```

As opções de duração podem ser modificadas no elemento `select`, desde que a lógica e as regras do banco continuem compatíveis.

## Autor

**Alberto de Campos Neto**

## Aviso

> Este projeto é uma demonstração educacional desenvolvida para estudos de HTML, CSS e JavaScript. A empresa mencionada é fictícia e qualquer semelhança com empresas reais é mera coincidência.
