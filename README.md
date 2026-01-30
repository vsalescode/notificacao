# 📧 Notificação – Microserviço de Notificação

![Java](https://img.shields.io/badge/Java-17+-red)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.x-brightgreen)
![Email](https://img.shields.io/badge/Service-Email-blue)
![Thymeleaf](https://img.shields.io/badge/Template-Thymeleaf-green)
![SMTP](https://img.shields.io/badge/Protocol-SMTP-orange)
![Build](https://img.shields.io/badge/Build-Maven-blueviolet)
![Status](https://img.shields.io/badge/Status-Completo-success)

Microserviço responsável pelo **envio de notificações por e-mail** dentro da arquitetura de **agendamento de tarefas**, utilizando **templates HTML com Thymeleaf**, integração via **REST** e foco em **baixo acoplamento** e **responsabilidade única**.

Este serviço é acionado por outros microserviços (principalmente o **Agendador**) para notificar usuários sobre **eventos, atualizações de tarefas e mudanças de status**.

---

## 🧱 Papel na Arquitetura

```text
[BFF]
  ├── Usuario Service (Autenticação / JWT)
  ├── Agendador Service (Eventos de tarefas)
  ├── Notificacao Service (Este serviço)
  └── Comunicação via REST / OpenFeign
```

- Serviço **stateless**
- Não possui persistência própria
- Responsável apenas pelo envio de notificações
- Preparado para evolução para mensageria assíncrona

---

## 📌 Funcionalidades

- Envio de e-mails transacionais
- Templates HTML profissionais com Thymeleaf
- Notificação baseada em eventos de tarefas
- Padronização visual corporativa
- Tratamento centralizado de erros de envio

---

## 🚀 Endpoint

| Método | Endpoint | Descrição |
|------|--------|---------|
| POST | /email | Enviar notificação de tarefa |

### Exemplo de Payload

```json
{
  "id": "abc123",
  "nomeTarefa": "Reunião com cliente",
  "descricao": "Discutir próximos passos do projeto",
  "emailUsuario": "usuario@email.com",
  "dataEvento": "30-01-2026 14:00:00",
  "statusNotificacaoEnum": "PENDENTE"
}
```

---

## 🧩 Estrutura Interna

### 📦 Camadas

- **Controller**
  - Exposição de endpoint REST
  - Recebimento de eventos de notificação

- **Service**
  - Construção do e-mail
  - Processamento do template HTML
  - Envio via SMTP

- **DTO**
  - Objeto de integração entre microserviços

- **Templates**
  - HTML responsivo com Thymeleaf

---

## ✉️ Template de E-mail

- Desenvolvido em **HTML responsivo**
- Layout corporativo e profissional
- Uso de:
  - Badges de status
  - Datas formatadas
  - Identidade visual padronizada

Compatível com clientes de e-mail modernos (Gmail, Outlook, etc).

---

## 🔐 Segurança

- Serviço interno (não exposto diretamente ao usuário final)
- Acesso esperado apenas por:
  - Agendador Service
  - BFF
- Pode ser protegido via:
  - Rede interna
  - Gateway
  - Autenticação por token (evolução futura)

---

## ⚙️ Configurações

Exemplo de configuração SMTP:

```yaml
spring:
  mail:
    host: smtp.gmail.com
    port: 587
    username: email.exemplo@gmail.com
    password: senha-ficticia-aqui
    protocol: smtp
    properties:
      mail:
        smtp:
          auth: true
          starttls:
            enable: true
            required: true

envio:
  email:
    remetente: email.exemplo@gmail.com
    nomeRemetente: Sistema de Notificações
```

---

## 🛠️ Tecnologias

- Java 17+
- Spring Boot
- Spring Mail
- Thymeleaf
- JavaMailSender
- Lombok
- Maven

---

## ▶️ Executando Localmente

```bash
mvn clean install
mvn spring-boot:run
```

Serviço disponível em:

```
http://localhost:8082
```

---

## 🛣️ Roadmap

- ✅ Envio de e-mails
- ✅ Templates HTML com Thymeleaf
- 🔜 Swagger

---

## 📌 Observações

Este microserviço segue o princípio de **Single Responsibility**, mantendo o ecossistema desacoplado e preparado para evolução futura, como:

- envio de SMS
- push notifications
- mensageria assíncrona

Projeto ideal para, **arquitetura real** e **cenários corporativos**.

