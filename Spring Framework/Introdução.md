# Introdução

> Um framework é um conjunto estruturado de bibliotecas e padrões que ajudam a desenvolver aplicações de maneira mais eficiente. 

O Spring é um conjunto de framework que possuem diversas bibliotecas diferentes, como por exemplo *Spring Data*, para acesso a banco de dados, *Spring Security*, Para segurança da aplicação, entre outros. As principais funcionalidades do Spring framework são:
* O Spring MVC (Model-View-Controller)
* Suporte para JDBC, JPA
* Injeção de dependências (Dependency injection - DI)

# Injeção de Dependências com Spring

É a técnica que faz com que o Spring crie e gerencie automaticamente novas instâncias de objetos. Ou seja, não há a necessidade de criar uma instância manualmente. A injeção de dependências (DI) é um tipo de inversão de controle (IoC).

A grande vantagem de se utilizar a injeção de dependências é que nós conseguimos programar voltados inteiramente para a interface. Por exemplo, suponha o código abaixo sem utilizar a injeção de dependências:

```
public class ServicoCliente{
	private RepositorioCliente repositorio = new RepositorioCliente();
}
```

Note que no caso acima nós criamos a instância de RepositorioCliente manualmente. Uma desvantagem de utilizar o código acima é devido ao forte acoplamento que a classe ServicoCliente possui com RepositorioCliente. O problema disso é que caso desejássemos mudar a implementação, por exemplo, utilizando um RepositorioClienteBanco, nós precisaríamos modificar a classe ServicoCliente. Uma outra desvantágem é a baixa flexibilidade e a dificuldade de reutilização. Agora observe o mesmo código, porém com a injeção de dependências:

```
@Service
public class ServicoCliente{
	@Autowired
	private RepositorioCliente repositorio;
}
```

As anotações são a base do Spring Framework. Por exemplo, ao definirmos alguma anotação para as classes, como @Service ou @Repository, o Spring Framework irá escanear cada uma dessas anotações, e guardará um bean referente a cada uma, criando instâncias para cada bean. Quando a anotação @Autowired é utilizada, o Spring Framework irá buscar o bean correspondente ao tipo RepositorioCliente, e irá injetar uma instância em repositorio, sem a necessidade de criar uma instância manualmente. 

**OBS:** Caso não haja nenhum bean correspondente ao tipo que foi declarado, será retornado uma exceção. 

# Spring MVC

O Spring MVC é o framework utilizado para criação de aplicações web robustas, flexíveis e com uma divisão bem estruturada de responsabilidades no tratamento de requisições.

A sigla MVC significa Model-View-Controller e é um padrão arquitetural que divide a aplicação em três componentes principais:
* *Model*: Representa os dados da aplicação e a lógica de negócios. Ele é responsável por acessar o banco de dados, processar dados e retornar as informações necessárias.
* *View*: Responsável pela exibição dos dados aos usuários. A View é a interface com o qual o usuário interage, podendo ser uma página web, um formulário, etc.
* *Controller:* Atua como um intermediário entre o Model e o View. É responsável por receber as requisições do usuário, invocar a lógica do Model para processar os dados e decidir qual View será exibida ao usuário.

[Como as requisições são processadas no MVC]()

É necessário estar atento para não cometer erros em relação a divisão da aplicação. Por exemplo, temos que tomar cuidado para não adicionarmos lógica de negócios ou acesso ao banco de dados em um *controller*. Precisamos passar isso para a camada *Model*, que processará as informações, retornando o resultado necessário. 

No *model* é o local correto para utilizarmos o *JPA*/*Hibernate* para salvar ou consultar algo no banco de dados. Por exemplo, é aqui que ficaria o cálculo do frete de um produto.  O *view* irá 'desenhar', renderizar e transformar em HTML esses dados retornados.

A ideia por trás do MVC é separar o código de modo que fique mais legível e melhor estruturado.

# Spring Data JPA

O Spring Data JPA é um framework que tem como objetivo facilitar o acesso da aplicação a um banco de dados, podendo ele ser relacional ou não relacional. O Spring Data por si só é um framework que possui diversos outros frameworks dentro de si, sendo alguns deles:
* Spring Data JPA
* Spring Data MongoDB
* Spring Data REST
* Spring Data KeyValue
 Entre outros...

Além de servir como ponte para conexões com banco de dados, o Spring Data JPA também fornece diversas convenções, padronizando o uso de algumas funcionalidades, fazendo com que haja menos esforço para implementar a mesma coisa.

# Spring Security

É um framework que trata a segurança em nivel de aplicação. Tem um excelente suporte para autorização e autenticação. 

Em relação a autenticação, o Spring Security torna bem simples essa parte. Com algumas poucas configurações, conseguimos autenticações via banco de dados ou outros. Spring Security também possui várias integrações. 

Quanto a autorização ele também é bem flexível. Através das permissões que atribuímos a usuários autenticados, podemos proteger as requisições web, a invocação de algum método ou a instância de algum objeto. 

# Spring Boot

> O Spring Boot busca reduzir a quantidade de configuração manual e autoconfigurar a maioria das opções.

As características principais oferecidas pelo Spring Boot são descritas a seguir:
* *Autoconfiguração:* O Spring Boot analisa seu projeto e automaticamente configura as partes necessárias. Por exemplo, se você está usando o Spring Data JPA, ele vai automaticamente configurar a conexão com o banco de dados e a persistência de dados, sem precisar de uma configuração detalhada.
* *Menos código de configuração:* Podemos utilizar *starters* em Spring Boot. Ou seja, dependências pré configuradas que agrupam várias outras dependências. Por exemplo, ao adicionarmos a dependência `spring-boot-starter-data-jpa`, o Spring Boot adiciona automaticamente todas as dependências necessárias para trabalhar com JPA e Hibernate.
* *Não gera código:* Spring Boot por si só não gera código, apenas cria uma autoconfiguração que ajudará na inicialização e manutenção do projeto. 

# O Thymeleaf

> É um framework de template engine para Java, usado principalmente em aplicações web, para gerar páginas HTML dinâmicas

O Thymeleaf permite que você escreva templates HTML, criando variáveis dinâmicas e estruturas de controle, como loops e estruturas condicionais, para exibir dados com base nas variáveis passadas pela aplicação. O Thymeleaf nos fornece alguns atributos, que misturados com o código HTML, geral  apenas um HTML que será renderizado no browser do cliente. 

Por exemplo, se temos uma lista de usuários no modelo de dados e desejamos exibir essa lista de usuários, podemos usar o Thymeleaf para exibir dinamicamente uma tabela com o conteúdo da lista de usuários. 

O Thymeleaf disponibiliza diversos atributos, por exemplo, considere o exemplo abaixo:

```
<tr th:each="convidado : ${convidados}">
	<td th:text="${convidado.nome}"></td>
	<td th:text="${convidado.quantidadeAcompanhantes}"></td>
</tr>
```

A expressão ${} interpreta variáveis locais ou variáveis disponibilizadas pelo *controller*. O atributo th:each itera sobre a lista de convidados, atribuindo cada objeto na variável local 'convidado'. Isso faz com que vários elementos tr sejam renderizados na página. O texto que cada td irá exibir vem do atributo th:text, junto com ${}, onde conterão as informações referentes a variável convidado.

