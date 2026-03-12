# 🤖 Projeto 01 — Pipeline de Qualificação de Leads com IA

🌐 **[Ver demo ao vivo](https://miqueias-automacao.netlify.app/projeto-01/)** &nbsp;|&nbsp; [← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)

---

## O que é

Sistema automatizado que recebe dados de um lead e usa **GPT-4o** para analisá-lo, atribuir um score de 0 a 100 e classificá-lo como **Hot 🔥, Warm ⚡ ou Cold ❄️** — sem intervenção humana.

---

## O problema que resolve

Sem automação, um SDR precisa avaliar cada lead manualmente — processo lento, subjetivo e inconsistente. Com este pipeline, a triagem acontece em segundos e o time comercial contata apenas quem tem real chance de fechar.

---

## Fluxo de automação

```
Formulário / Landing Page
        ↓
Webhook (Make.com)
        ↓
GPT-4o analisa o lead
        ↓
JSON: score + classe + análise + próxima ação
        ↓
Supabase salva o registro
        ↓
Kommo CRM cria o lead com tags automáticas
        ↓
SDR recebe notificação
```

---

## Stack

| Ferramenta | Uso |
|---|---|
| **Make.com** | Orquestração do fluxo completo |
| **OpenAI GPT-4o** | Análise e classificação do lead |
| **Supabase** | Armazenamento dos resultados (PostgreSQL) |
| **Webhook** | Entrada de dados em tempo real |
| **Kommo API** | Criação automática do lead no CRM |

---

## Prompt enviado ao GPT-4o

```
Você é um qualificador de leads B2B especialista.
Analise o lead e retorne APENAS JSON válido:

{
  "score": 0-100,
  "classe": "hot|warm|cold",
  "potencial": "ticket estimado",
  "prioridade": "urgência de contato",
  "proxima_acao": "recomendação para o SDR",
  "analise": "resumo em 2-3 frases"
}
```

---

## Estrutura do banco (Supabase)

```sql
CREATE TABLE leads_qualificados (
  id           UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at   TIMESTAMPTZ DEFAULT now(),
  nome         TEXT NOT NULL,
  empresa      TEXT,
  cargo        TEXT,
  porte        TEXT,
  mensagem     TEXT,
  score        INT CHECK(score BETWEEN 0 AND 100),
  classe       TEXT CHECK(classe IN ('hot', 'warm', 'cold')),
  potencial    TEXT,
  prioridade   TEXT,
  proxima_acao TEXT,
  analise      TEXT,
  kommo_id     TEXT,
  status       TEXT DEFAULT 'novo'
);
```

---

## Como rodar localmente

1. Clone o repositório
2. Abra `projeto-01/index.html` no navegador
3. Preencha o formulário e clique em **Qualificar com IA**

> Não precisa instalar nada — roda direto no navegador.

---

[← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)
