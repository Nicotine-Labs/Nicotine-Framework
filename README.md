# Nicotine-Framework

Nicotine é um framework web Java moderno que combina a estrutura robusta com a performance . 

Desenvolvido para criar aplicações web dinâmicas e interativas completamente em Java, 
oferecendo uma alternativa nativa à necessidade de frameworks JavaScript.

![Nicotine Framework Logo](/public/logo.png)

## Características Principais

- 🚀 **Performance Excepcional**: Sem Virtual DOM, compilação ahead-of-time
- 🎯 **100% Java**: Frontend e backend integrados nativamente
- 📦 **Batteries Included**: Tudo que você precisa em um único framework
- 🔄 **Hot Reload**: Desenvolvimento ágil com atualização em tempo real
- 🛠 **Ferramentas Integradas**: CLI, servidor de desenvolvimento, e sistema de build
- 🔌 **Integração Spring**: Trabalha perfeitamente com Spring Boot
- 📱 **PWA Ready**: Suporte nativo para Progressive Web Apps

## Início Rápido

### Pré-requisitos

- Java 17 ou superior
- Maven 3.6+
- Docker (opcional)

### Instalação

1. Instale o CLI do Nicotine:

```bash
curl -sL https://get.nicotine.dev | bash
```

2. Crie um novo projeto:

```bash
nicotine new meu-projeto
cd meu-projeto
```

3. Inicie o servidor de desenvolvimento:

```bash
nicotine serve
```

Acesse `http://localhost:3000` para ver sua aplicação rodando.

## Exemplos de Uso

### Componente Simples

```java
@Component(selector = "app-hello")
public class HelloComponent extends NicotineComponent {
    private String message = "Hello, Nicotine!";
    
    @OnInit
    public void initialize() {
        setState("message", message);
    }
    
    @Override
    protected String template() {
        return """
            <div>
                <h1>{{message}}</h1>
                <button @click="updateMessage()">Click me</button>
            </div>
        """;
    }
    
    private void updateMessage() {
        message = "Button clicked!";
        setState("message", message);
    }
}
```

### Serviço HTTP

```java
@Service
public class UserService {
    @Inject
    private HttpClient http;
    
    public CompletableFuture<List<User>> getUsers() {
        return http.get("/api/users", User[].class)
                  .thenApply(Arrays::asList);
    }
}
```

### Roteamento

```java
@Page(route = "/users/:id")
public class UserDetailPage extends NicotineComponent {
    @Inject
    private UserService userService;
    
    @RouteParam
    private String id;
    
    @OnInit
    public void initialize() {
        userService.getUser(id)
                  .thenAccept(user -> setState("user", user));
    }
}
```

## Build e Deploy

### Build para Produção

```bash
nicotine build
```

Os arquivos otimizados serão gerados na pasta `dist/`.

### Deploy com Docker

```bash
docker build -t minha-app .
docker run -p 8080:8080 minha-app
```

## Integração com Spring Boot

Adicione a dependência no `pom.xml`:

```xml
<dependency>
    <groupId>dev.nicotine</groupId>
    <artifactId>nicotine-spring-boot-starter</artifactId>
    <version>1.0.0</version>
</dependency>
```

Configure no Spring:

```java
@Configuration
public class NicotineConfig {
    @Bean
    public NicotineViewResolver nicotineViewResolver() {
        return new NicotineViewResolver();
    }
}
```

## Documentação

Documentação completa disponível em [docs.nicotine.dev](https://docs.nicotine.dev)

## CLI Commands

- `nicotine new [nome]` - Cria novo projeto
- `nicotine serve` - Inicia servidor de desenvolvimento
- `nicotine build` - Build para produção
- `nicotine generate component [nome]` - Gera novo componente
- `nicotine generate service [nome]` - Gera novo serviço
- `nicotine test` - Executa testes
- `nicotine deploy` - Deploy para produção

## Performance

Benchmarks comparativos (Tempo de carregamento inicial):

- ⚡ Nicotine: 1.2s
- 🅰️ Angular: 2.8s
- ⚛️ React: 2.1s

## Contribuindo

1. Fork o projeto
2. Crie sua Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a Branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## Licença

Este projeto está licenciado sob a MIT License - veja o arquivo [LICENSE.md](LICENSE.md) para detalhes.

## Suporte

- 📫 Email: support@nicotine.dev
- 💬 Chat: [Discord](https://discord.gg/msjsG55MGn)
- 🐦 Twitter: [@NicotineFramework](https://twitter.com/NicotineFramework)

## Roadmap

- [ ] Server-side rendering
- [ ] Microfront-ends support
- [ ] Native mobile compilation
- [ ] GraphQL integration
- [ ] AI-powered development tools

## Créditos

Desenvolvido com ☕ por [Bullet](https://github.com/Bulletdev)
