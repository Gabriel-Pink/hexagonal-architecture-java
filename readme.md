```
src/main/java/com/seusite/seuapp
├── domain
│   └── model           ← Modelos de domínio e entidades.
│   └── service         ← Serviços de domínio (lógica de negócios pura).
│
├── application
│   ├── port
│   │   ├── in          ← Casos de uso (interfaces de entrada).
│   │   └── out         ← Interfaces de saída (para persistência, etc).
│   └── service         ← Implementação dos casos de uso.
│
├── adapter
│   ├── in
│   │   └── rest        ← Adapters para a entrada (ex: controladores REST).
│   └── out
│       ├── persistence ← Implementações de persistência (ex: repositórios JPA).
│       └── jwt         ← Adapters para geração e validação de JWT.
│
├── config              ← Configurações gerais (ex: Spring Security).
└── SeuAppApplication.java ← A classe principal que inicia o Spring Boot.
```

### **Explicando as pastas:**

1. **`domain`**: A camada central da arquitetura hexagonal, onde ficam **as regras de negócio**. Aqui você coloca toda a lógica de domínio do sistema.
    
    - **`model`**: Contém as **entidades** do sistema. Por exemplo, um **usuário**, **produto** ou **pedido**. Essas entidades são o núcleo da lógica de negócios.
        
    - **`service`**: Contém os **serviços de domínio**, que implementam a lógica mais complexa que se aplica às entidades. Por exemplo, métodos que verificam regras específicas ou orquestram interações entre várias entidades.
        
    
    Exemplos de classes:
    
    - `User.java` (entidade)
        
    - `OrderService.java` (serviço de domínio)
        
2. **`application`**: A camada de **aplicação** orquestra a comunicação entre o **domínio** e o **mundo externo**. É onde os **casos de uso** (ou interações) do sistema são definidos.
    
    - **`port/in`**: São as **interfaces de entrada**, ou seja, os **casos de uso** que o sistema expõe. Isso pode incluir coisas como "fazer login", "criar um novo pedido" ou "consultar um produto".
        
    - **`port/out`**: São as **interfaces de saída**. Elas definem o que o sistema precisa de **dependências externas**, como repositórios de banco de dados, serviços de autenticação, etc.
        
    - **`service`**: Aqui você implementa os casos de uso, ou seja, a lógica que **orquestra** as interações entre a entrada e a saída, utilizando a lógica de domínio.
        
    
    Exemplos de classes:
    
    - `AuthUseCase.java` (interface de entrada)
        
    - `AuthService.java` (implementação do caso de uso)
        
    - `UserRepositoryPort.java` (interface de saída)
        
3. **`adapter`**: São as **implementações reais** de como a aplicação interage com o mundo externo. Eles **adaptam** as interfaces definidas nas camadas de **entrada** e **saída** para as tecnologias específicas.
    
    - **`in/rest`**: São os **adapters de entrada**, ou seja, como o sistema vai interagir com o usuário ou com outras aplicações (ex: controladores REST, fila de mensagens, CLI, etc).
        
    - **`out/persistence`**: São os **adapters de saída** para **persistência de dados**, como um repositório de banco de dados (ex: JPA, MongoDB).
        
    - **`out/jwt`**: Aqui ficam os adapters relacionados ao uso de tokens JWT ou qualquer outra tecnologia que envolva a geração ou validação de tokens.
        
    
    Exemplos de classes:
    
    - `AuthController.java` (adapter de entrada - controlador REST)
        
    - `UserRepositoryImpl.java` (adapter de saída - implementação do repositório JPA)
        
    - `JwtTokenService.java` (adapter de saída - geração e validação de JWT)
        
4. **`config`**: Essa pasta contém **configurações específicas** do Spring Boot ou de outras tecnologias. Aqui ficam, por exemplo, a configuração do **Spring Security**, a configuração de banco de dados, a configuração de JWT, etc.
    
5. **`SeuAppApplication.java`**: O ponto de entrada do Spring Boot. A classe principal que inicia o contexto do Spring e configura o servidor.