# Afya Admin — Dashboard com Blazor WebAssembly e MudBlazor

## Identificação

| | |
|---|---|
| **Aluno(a)** | Lucas Gabriel Barreto Oliveira |
| **Matrícula** | 2630436 |
| **Faculdade** | São Lucas Campus 2 |
| **Curso** | Ciência da Computação |
| **Disciplina** | Programação para Sistemas Web |
| **Professor(a)** | LILUYOUD CURY DE LACERDA |
| **Semestre** | 2026.2 |

## Objetivo do projeto

O projeto é uma aplicação web feita em Blazor, chamada afya-admin, que funciona como um painel administrativo. A página principal mostra um Dashboard com alguns indicadores (KPIs), cards com informações e um seletor de período. Neste projeto ele só troca o texto do botão; os KPIs não mudam.

No geral, o objetivo do projeto foi construir um Dashboard administrativo em Blazor, utilizando componentes reutilizáveis e o MudBlazor para organizar e estilizar a interface. A página mostra indicadores e informações importantes de maneira visual, além de permitir a seleção de diferentes períodos. Durante a construção, foram utilizados conceitos importantes do Blazor, como Layouts, Pages, Components, RenderFragment, data binding com @bind-Valor, organização dos dados e responsividade através do MudGrid.

## Tecnologias utilizadas

- .NET 10 / Blazor WebAssembly (standalone)
- MudBlazor 9 (componentes, tema e classes utilitárias)
- C# e Razor
- Fonte Inter (Google Fonts)
- Git e GitHub

## Como executar

É necessário o **.NET SDK 10** (o projeto foi desenvolvido com a versão 10.0.401). Confira com `dotnet --version`.

```bash
git clone https://github.com/Prequelunsainted/afya-admin.git
cd afya-admin
dotnet watch
```

O `dotnet watch` compila, abre o navegador e recarrega a página a cada alteração salva. A URL aparece no terminal (neste projeto, `http://localhost:5213`).

## Telas

### Tema claro
![Dashboard — tema claro](docs/prints/tema-claro.png)

### Tema escuro
![Dashboard — tema escuro](docs/prints/tema-escuro.png)

### Versão mobile
![Dashboard — celular](docs/prints/mobile.png)

### HTML gerado (DevTools)
![Inspeção do HTML no DevTools](docs/prints/devtools.png)

O print mostra a aba Elements com o card de KPI "Receita" inspecionado:

- o `<MudPaper Elevation="1" Class="pa-4" Height="100%">` do `KpiCard.razor` virou `<div class="mud-paper mud-elevation-1 pa-4" style="height:100%;">`: a classe utilitária `pa-4` escrita no código aparece igual no HTML final;
- o `<MudStack Row="true" Spacing="3" AlignItems="AlignItems.Center">` virou `<div role="group" class="d-flex flex-row align-center gap-3">`;
- o `<MudText Typo="Typo.body2" Class="mud-text-secondary">` virou `<p class="mud-typography mud-typography-body2 mud-text-secondary">`, e o valor com `Typo.h5` virou um `<h5>`;
- cada `<MudItem xs="12" sm="6" lg="3">` do `Dashboard.razor` virou uma `<div>` com as classes `mud-grid-item-xs-12 mud-grid-item-sm-6 mud-grid-item-lg-3`.

## Estrutura do projeto

```
afya-admin/
├── Components/
│   ├── AtividadesRecentes.razor
│   ├── CabecalhoPagina.razor
│   ├── DashboardCard.razor
│   ├── GraficoDistribuicaoClientes.razor
│   ├── GraficoReceita.razor
│   ├── KpiCard.razor
│   ├── PerformanceProjetos.razor
│   ├── ProjetosRecentes.razor
│   ├── SeletorPeriodo.razor
│   └── Ui.cs
├── Data/
│   └── DashboardData.cs
├── Layout/
│   ├── MainLayout.razor
│   └── NavMenu.razor
├── Pages/
│   ├── Dashboard.razor
│   └── NotFound.razor
├── Properties/
│   └── launchSettings.json
├── docs/
│   └── prints/
├── wwwroot/
│   ├── css/app.css
│   ├── img/alex-morgan.jpg
│   ├── favicon.png
│   ├── icon-192.png
│   └── index.html
├── _Imports.razor
├── afya-admin.csproj
├── App.razor
└── Program.cs
```

| Pasta | Papel |
|---|---|
| `Components` | componentes visuais reutilizáveis do dashboard e a classe auxiliar `Ui` |
| `Data` | modelos (`record`) e os dados fictícios usados pela página |
| `Layout` | a moldura da aplicação: tema, AppBar, sidebar e menu de navegação |
| `Pages` | as páginas com rota (`@page`): o Dashboard e a página 404 |
| `wwwroot` | arquivos estáticos servidos ao navegador: `index.html`, CSS do template, imagens e ícones |

## Componentes criados

| Componente | Responsabilidade | Parâmetros que recebe |
|---|---|---|
| `CabecalhoPagina` | título e subtítulo da página à esquerda e uma área de ações à direita | `Titulo` (obrigatório), `Subtitulo`, `Acoes` (`RenderFragment`) |
| `SeletorPeriodo` | menu com aparência de botão para escolher o período; avisa a página quando o valor muda | `Opcoes` (obrigatório), `Valor`, `ValorChanged` (`EventCallback<string>`) |
| `DashboardCard` | card base com título, subtítulo opcional, ações, menu "⋮" opcional e conteúdo | `Titulo` (obrigatório), `Subtitulo`, `Acoes`, `Menu`, `ChildContent` (`RenderFragment`) |
| `KpiCard` | card de indicador com ícone, valor, variação e mini gráfico de tendência (sparkline) | `Kpi` (obrigatório) |
| `GraficoReceita` | gráfico de linha Receita x Meta com legenda própria | `Meses`, `Receita`, `Meta` (todos obrigatórios) |
| `GraficoDistribuicaoClientes` | gráfico de rosca com o total no centro e legenda com percentuais | `Total`, `Segmentos` (obrigatórios) |
| `PerformanceProjetos` | lista de projetos com barra de progresso, percentual e tarefas concluídas | `Projetos` (obrigatório) |
| `AtividadesRecentes` | feed com ícone da ação, avatar com iniciais, descrição e tempo | `Atividades` (obrigatório) |
| `ProjetosRecentes` | tabela de projetos com status, progresso e menu de ações; vira lista de cards no celular | `Projetos` (obrigatório) |

`Ui.cs` não é um componente: é uma classe estática com `FundoSuave(Color)`, que devolve a classe utilitária de fundo suave da cor, e `Iniciais(string)`, que devolve as iniciais de um nome.

## O que aprendi

**1. Como uma aplicação Blazor WebAssembly inicia no navegador? Qual é o papel do `index.html`, da `<div id="app">` e do `Program.cs`?**

O funcionamento do Blazor no navegador começa pelo arquivo index.html. Dentro dele existe a `<div id="app">`, que é basicamente o espaço onde a aplicação Blazor vai ser carregada. Quando o navegador abre o projeto, o Blazor WebAssembly é iniciado através do arquivo JavaScript do próprio framework. Depois disso, o Program.cs entra na configuração da aplicação, registrando os serviços necessários e definindo o componente inicial. A partir daí, os componentes Blazor são renderizados dentro da `<div id="app">`. Então, de forma resumida, o navegador carrega o index.html, encontra a `<div id="app">`, inicia o Blazor e o Program.cs configura a aplicação para que a interface seja exibida.

**2. Qual é a diferença entre um Layout, uma Page e um Component neste projeto? Dê um exemplo de cada.**

A diferença entre Layout, Page e Component está principalmente na função de cada um. O Layout é a estrutura que pode ser compartilhada entre várias páginas, como um menu, cabeçalho ou área principal. Ele possui um @Body, que é onde o conteúdo da página atual é colocado. Neste projeto o Layout é o MainLayout.razor. A Page é uma tela específica da aplicação e possui uma rota: aqui é o Dashboard.razor, que responde pela rota "/". Já o Component é uma parte reutilizável da interface. Um exemplo é o DashboardCard, que pode ser utilizado várias vezes para mostrar diferentes informações sem precisar criar o mesmo código novamente. Então, o Layout organiza a estrutura geral, a Page representa uma tela e o Component representa uma parte reutilizável dessa tela.

**3. O que é um `RenderFragment` e como o `DashboardCard` usa esse recurso para ser reutilizado por vários cards?**

O RenderFragment é um recurso do Blazor que permite passar conteúdo para dentro de um componente. No caso do DashboardCard, ele é útil porque o card pode ter uma estrutura padrão, mas permitir que o conteúdo interno seja definido de acordo com o lugar onde ele está sendo utilizado. Dessa forma, o mesmo DashboardCard pode ser usado para diferentes informações sem precisar criar um componente diferente para cada tipo de conteúdo. O RenderFragment deixa o componente mais flexível e reutilizável.

**4. Como funciona o `@bind-Valor` no `SeletorPeriodo`? Qual é o papel do `ValorChanged`?**

No SeletorPeriodo, o @bind-Valor é usado para fazer a ligação entre o valor selecionado no componente e uma variável da página que está utilizando esse componente. Quando escrevemos @bind-Valor, o Blazor utiliza a propriedade Valor junto com o ValorChanged para fazer essa comunicação automaticamente. O Valor representa o valor atual do período selecionado e o ValorChanged é responsável por avisar o componente pai quando esse valor muda. Então, quando o usuário escolhe outro período, o SeletorPeriodo dispara o ValorChanged e a variável que está ligada através do @bind-Valor é atualizada. Isso facilita bastante a comunicação entre o componente e a página.

**5. Por que os dados ficam na pasta `Data`, separados dos componentes? Que vantagem isso traz se, no futuro, os dados vierem de uma API?**

Os dados ficam na pasta Data porque essa pasta serve para organizar as informações e as classes relacionadas aos dados da aplicação, separando essa parte da interface visual. Dessa maneira, os componentes ficam mais focados em mostrar as informações, enquanto a parte relacionada aos dados fica organizada em outro lugar. Isso também facilita uma possível alteração no futuro, como trocar dados fixos por dados vindos de uma API, sem precisar modificar toda a interface.

**6. Como o `MudGrid` com `xs`, `sm` e `lg` faz os cards de KPI se reorganizarem em telas de tamanhos diferentes?**

O MudGrid é utilizado para organizar os KPIs de forma responsiva. Os valores xs, sm e lg definem quanto espaço cada item ocupa dependendo do tamanho da tela. Por exemplo, se um KPI possui xs="12", em uma tela pequena ele pode ocupar toda a largura. Com sm="6", em uma tela um pouco maior ele pode ocupar metade da largura, e com lg="3", em uma tela grande ele pode ocupar um quarto da largura. Isso faz com que os cards se reorganizem automaticamente. Em uma tela grande eles podem ficar vários lado a lado, enquanto em uma tela menor podem ficar em duas colunas ou até um embaixo do outro. Dessa forma, o Dashboard consegue ser responsivo sem precisar criar diferentes layouts para cada tamanho de tela.

**7. Como foi possível estilizar a página inteira sem escrever CSS? Explique o papel do tema (`MudTheme`) e das classes utilitárias.**

Foi possível estilizar a aplicação sem criar um arquivo CSS cheio de regras próprias principalmente por causa do MudBlazor. A biblioteca já possui componentes prontos, propriedades de estilo, classes utilitárias e um sistema de tema. Com isso, é possível controlar cores, espaçamentos, tamanhos, alinhamentos e a aparência dos componentes diretamente através dos recursos do MudBlazor. Isso evita a necessidade de criar CSS manual para cada detalhe e também deixa a aparência da aplicação mais consistente.

**8. Por que o namespace do projeto é `afya_admin` e não `afya-admin`?**

O C# não aceita hífen em nomes, porque afya-admin seria lido como "afya menos admin". Por isso o SDK troca o hífen por sublinhado, e o namespace fica afya_admin. A pasta e o arquivo do projeto continuam com hífen (afya-admin), mas no código, como em afya_admin.Data, aparece o sublinhado.

## Dificuldades e soluções

Durante o desenvolvimento também tivemos algumas dificuldades. Uma delas aconteceu quando tentamos executar o comando dotnet --version. O comando deu erro porque o SDK do .NET não estava disponível/configurado no ambiente naquele momento. Isso mostrou que, antes de executar um projeto .NET, é importante verificar se o SDK necessário está instalado e funcionando corretamente, já que comandos de desenvolvimento como dotnet build e dotnet watch dependem dele.

Outra dificuldade aconteceu quando o dotnet watch foi executado na pasta errada. Como esse comando precisa encontrar o projeto, ele procura o arquivo do projeto, como o .csproj, no diretório em que está sendo executado. Como o comando foi rodado em uma pasta que não era a pasta correta do projeto, ele não conseguiu localizar a aplicação da forma esperada. Depois foi necessário entrar na pasta correta do projeto e executar o dotnet watch novamente. Esse erro foi importante porque mostrou que não basta apenas executar o comando: também é necessário estar no diretório correto da aplicação.
