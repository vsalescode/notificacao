# 📧 Serviço de Notificação (Notification Service)

O **"Carteiro" do ecossistema**.\
Um microsserviço leve e stateless focado exclusivamente em converter
dados brutos em comunicações visuais elegantes e enviá-las via SMTP.

------------------------------------------------------------------------

## 🚀 Visão Geral

Diferente dos outros serviços, este componente **não possui banco de
dados**.\
Ele atua como um **Worker passivo**, aguardando requisições HTTP
contendo dados de tarefas, processando essas informações dentro de um
template HTML responsivo e realizando o envio do e-mail.

------------------------------------------------------------------------

## ✅ Principais Funcionalidades

-   **Renderização Server-Side:** Uso do Thymeleaf para injetar dados
    dinâmicos em templates HTML.
-   **E-mails Responsivos:** Template `notificacao.html` com CSS inline
    compatível com Gmail, Outlook e Apple Mail.
-   **Integração SMTP:** Compatível com Gmail, AWS SES, SendGrid e
    outros provedores.
-   **Tratamento de Erros:** Captura falhas de envio e retorna exceções
    tratadas.

------------------------------------------------------------------------

## 🛠️ Tecnologias Utilizadas

-   Java 17
-   Spring Boot 3
-   Spring Boot Starter Mail (JavaMailSender)
-   Thymeleaf
-   Lombok

------------------------------------------------------------------------

## ⚙️ Configuração SMTP

O serviço roda na porta **8082**.

Configure o arquivo:

    src/main/resources/application.yaml

### Exemplo de Configuração (Gmail)

> ⚠️ Utilize **Senha de App** e nunca sua senha normal.

``` yaml
server:
  port: 8082

spring:
  mail:
    host: smtp.gmail.com
    port: 587
    username: seu-email@gmail.com
    password: sua-senha-de-app
    protocol: smtp
    properties:
      mail:
        smtp:
          auth: true
          starttls:
            enable: true
            required: true
          connectiontimeout: 5000
          timeout: 3000
          writetimeout: 5000

envio:
  email:
    remetente: seu-email@gmail.com
    nomeRemetente: Sistema de Tarefas
```

------------------------------------------------------------------------

## 🔌 Endpoint

### 📤 Enviar E-mail de Notificação

**POST** `/email`

### Corpo da Requisição

``` json
{
  "id": "65b2f...a1b2",
  "nomeTarefa": "Reunião de Arquitetura",
  "descricao": "Discutir a implementação do padrão Saga.",
  "emailUsuario": "destinatario@exemplo.com",
  "dataEvento": "30-01-2026 14:00:00",
  "statusNotificacaoEnum": "PENDENTE"
}
```

### Respostas

-   **200 OK** → E-mail enviado com sucesso
-   **500 Internal Server Error** → Falha SMTP ou erro de template

------------------------------------------------------------------------

## 🎨 Template HTML

Arquivo:

    src/main/resources/templates/notificacao.html

### Variáveis Thymeleaf

  Variável                     Descrição
  ---------------------------- ---------------------------------
  `${nomeTarefa}`              Título da tarefa
  `${dataEvento}`              Data e hora formatada
  `${descricao}`               Detalhes da tarefa
  `${statusNotificacaoEnum}`   Define a cor da badge de status

O layout utiliza um **card centralizado**, sombras suaves e tipografia
moderna (Helvetica/Arial) para manter aparência profissional.

------------------------------------------------------------------------

## ▶️ Como Executar

### Pré-requisitos

-   Java 17+
-   Maven

### Executar

``` bash
mvn spring-boot:run
```

O serviço ficará disponível em:

    http://localhost:8082

------------------------------------------------------------------------

## 👨‍💻 Autor

Desenvolvido por **João Victor**

🔗 [LinkedIn](https://www.linkedin.com/in/vsalescode/)
🌐 [Portfólio](https://portfolio-vsalescode.vercel.app/)

