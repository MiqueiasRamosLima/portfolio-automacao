# ✍️ Projeto 02 — Gerador de Conteúdo Automático

🌐 **[Ver demo ao vivo](https://miqueias-automacao.netlify.app/projeto-02/)** &nbsp;|&nbsp; [← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)

---

## O que é

Sistema que recebe um briefing (assunto, tipo, tom de voz) e gera automaticamente textos prontos para publicação — posts de LinkedIn, e-mails de vendas, legendas de Instagram ou descrições de produto.

---

## O problema que resolve

Times de marketing gastam horas escrevendo conteúdo repetitivo. Com este gerador, um briefing de 30 segundos produz um texto publicável em segundos, com tom de voz consistente em todos os canais.

---

## Tipos de conteúdo suportados

| Tipo | Descrição |
|---|---|
| **Post LinkedIn** | Texto profissional com storytelling e CTA |
| **E-mail de Vendas** | Assunto + corpo persuasivo focado em conversão |
| **Post Instagram** | Legenda criativa com hashtags otimizadas |
| **Descrição de Produto** | Texto focado em benefícios e CTA de compra |

---

## Fluxo de automação

```
Briefing (formulário / webhook)
        ↓
Make.com monta prompt dinâmico
        ↓
GPT-4o gera conteúdo + hashtags
        ↓
Supabase salva histórico completo
        ↓
Router entrega no canal certo:
  ├── LinkedIn → Google Sheets (fila de aprovação)
  ├── E-mail   → Gmail / SMTP
  └── Produto  → Atualiza CRM
```

---

## Stack

| Ferramenta | Uso |
|---|---|
| **Make.com** | Orquestração e roteamento |
| **OpenAI GPT-4o** | Geração de conteúdo |
| **Supabase** | Histórico de conteúdos gerados |
| **Google Sheets** | Fila de aprovação de conteúdo |
| **Gmail / SMTP** | Entrega de e-mails gerados |

---

## Controle de tom de voz

O sistema aceita um parâmetro de tom de 1 a 5:

```
1 → Muito formal
2 → Formal
3 → Equilibrado
4 → Casual
5 → Muito casual
```

---

## Como rodar localmente

1. Clone o repositório
2. Abra `projeto-02/index.html` no navegador
3. Escolha o tipo de conteúdo, preencha o briefing e clique em **Gerar conteúdo**

> Não precisa instalar nada — roda direto no navegador.

---

[← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)
