# 🔗 Projeto 04 — Integração Kommo CRM via API REST

🌐 **[Ver demo ao vivo](https://miqueias-automacao.netlify.app/projeto-04/)** &nbsp;|&nbsp; [← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)

---

## O que é

Integração bidirecional entre Make.com e Kommo CRM usando a **API REST v4 oficial**. Cria leads automaticamente no CRM com todas as informações e tags, e sincroniza mudanças de status de volta para o Supabase via webhook reverso.

---

## O problema que resolve

Sem integração, o SDR precisa criar manualmente cada lead no CRM após receber a qualificação — trabalho repetitivo e sujeito a erros. Com esta integração, o lead aparece no CRM automaticamente, já com tag de prioridade e atribuído ao responsável certo.

---

## Fluxo de integração

```
Lead qualificado (Projeto 01)
        ↓
Make.com prepara requisição
        ↓
OAuth 2.0 — token renovado automaticamente
        ↓
POST /api/v4/leads → Kommo cria o lead
        ↓
Kommo retorna ID do lead criado
        ↓
Supabase salva o kommo_id para rastreio
        ↓
[Webhook reverso]
SDR muda status no Kommo
        ↓
Kommo dispara webhook → Make.com
        ↓
Supabase atualizado com novo status
```

---

## Stack

| Ferramenta | Uso |
|---|---|
| **Kommo API v4** | Criação e atualização de leads |
| **OAuth 2.0** | Autenticação com renovação automática |
| **Make.com** | Orquestração das chamadas REST |
| **Supabase** | Rastreio bidirecional dos leads |
| **Webhooks** | Sincronização reversa Kommo → Make |

---

## Endpoints utilizados

```
POST  /api/v4/leads              → Criar lead
GET   /api/v4/leads/{id}         → Buscar lead
PATCH /api/v4/leads/{id}         → Atualizar lead
POST  /oauth2/access_token       → Renovar token OAuth
```

---

## Exemplo de payload enviado

```json
[{
  "name": "Ana Paula Ferreira",
  "price": 3500,
  "pipeline_id": 1284756,
  "_embedded": {
    "companies": [{ "name": "TechVentures" }],
    "tags": [{ "name": "Hot Lead" }]
  }
}]
```

---

## Como rodar localmente

1. Clone o repositório
2. Abra `projeto-04/index.html` no navegador
3. Vá na aba **Demo API** → preencha o formulário → clique em **Enviar para o CRM**
4. Veja o JSON de resposta simulado da API
5. Explore as abas **Leads no CRM** e **Fluxo Técnico**

> Não precisa instalar nada — roda direto no navegador.

---

[← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)
