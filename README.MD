# Docker Manager API

Este projeto é uma API simples desenvolvida com **Spring Boot** e **Docker Java Client**, que permite realizar operações básicas com containers e imagens Docker diretamente a partir de uma aplicação Java.

---

## 📦 Funcionalidades

A API expõe um serviço chamado `DockerService` com as seguintes operações:

### 🔧 Containers
- **Listar containers** (ativos ou todos)
- **Iniciar um container**
- **Parar um container**
- **Remover um container**
- **Criar um novo container** a partir de uma imagem

### 🖼️ Imagens
- **Listar imagens locais**
- **Filtrar imagens por nome**

---

## 🚀 Tecnologias Utilizadas

- Java 21
- Spring Boot 3
- Docker Java Client (`docker-java`, `docker-java-transport-httpclient5`)
- Apache HttpClient 5
- JNA

---

## ⚙️ Configuração

### Pré-requisitos
- Docker instalado e em execução
- Java 21+
- Maven

### application.properties

Configure o caminho do socket Docker:

```properties
# Para Linux/macOS
docker.socket.path=unix:///var/run/docker.sock

# Para Windows (usando Docker Desktop com o protocolo npipe)
# docker.socket.path=npipe:////./pipe/docker_engine
```

---

## 🧪 Execução do Projeto

### Clonar o repositório
```bash
git clone https://github.com/seu-usuario/docker-manager.git
cd docker-manager
```

### Compilar e executar
```bash
mvn clean install
mvn spring-boot:run
```

---

## 🧩 Exemplo de Uso

As operações do `DockerService` podem ser expostas por controladores REST, como:

```java
@RestController
@RequestMapping("/containers")
public class DockerContainersController {

    private final DockerService dockerService;

    public DockerContainersController(DockerService dockerService) {
        this.dockerService = dockerService;
    }

    @GetMapping
    public List<Container> listAll(@RequestParam(defaultValue = "false") boolean all) {
        return dockerService.listContainers(all);
    }

    @PostMapping("/start/{id}")
    public void start(@PathVariable String id) {
        dockerService.startContainer(id);
    }

    // outros endpoints...
}
```

---

## 👨‍💻 Autor

Desenvolvido por **Fernando Rocha**  
📍 Fortaleza - CE  
🔗 [LinkedIn](https://www.linkedin.com/in/fernandorocha)

---

## 📄 Licença

Este projeto é de código aberto e está sob a licença MIT.