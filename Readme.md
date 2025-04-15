### Projeto: Sistema de Processamento de Pedidos (Order Processing System)

**Contexto**

Um sistema onde um serviço cria pedidos (Order Service) e outro serviço (Order Processor) os processa de forma assíncrona via RabbitMQ.

---

### Microserviços

1. **Order API (Producer)**

   1. API Rest para criar pedidos
   2. Envia o pedido como mensagem para uma fila do RabbitMQ
   3. Responsável só por receber e publicar o pedido na fila

2. **Order Processor (Consumer)**
   1. Fica escutando a fila do RabbitMQ
   2. Processa os pedidos recebidos (Estou vendo o que irei fazer, persistir em banco ou disparar um email)

---

### Funcionalidades

1. Criar um novo pedido (nome cliente, itens, valor)
2. Processar o pedido
3. Armazenar logs de pedidos processados

---

### **Onde entra o SOLID?**

- **S** (Single Responsibility): Cada classe tem uma única responsabilidade (ex: envio da mensagem, validação, persistência)
- **O** (Open/Closed): Você pode estender regras de processamento sem modificar código existente
- **L** (Liskov Substitution): Usar abstrações como interfaces corretamente
- **I** (Interface Segregation): Interfaces pequenas e específicas (ex: `IMessagePublisher`, `IMessageConsumer`)
- **D** (Dependency Inversion): Injetar dependências com abstrações (ex: repositórios, serviços de fila)

---

### **Tecnologias**

- .NET 9 (API + Worker Service)
- RabbitMQ (mensageria)
- Swagger (documentação da API)
- Docker (para subir RabbitMQ localmente)
