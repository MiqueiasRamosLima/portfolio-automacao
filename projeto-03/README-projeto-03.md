# 📊 Projeto 03 — Monitor de Falhas e Dashboard

🌐 **[Ver demo ao vivo](https://miqueias-automacao.netlify.app/projeto-03/)** &nbsp;|&nbsp; [← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)

---

## O que é

Dashboard em tempo real que monitora a saúde de todas as automações em execução — exibindo taxa de sucesso, logs detalhados, alertas de erro e métricas de uptime integradas ao Supabase.

---

## O problema que resolve

Sem monitoramento, falhas em automações passam despercebidas por horas ou dias. Este dashboard detecta erros em tempo real, registra o histórico completo e alerta o time automaticamente — antes que o negócio seja impactado.

---

## Funcionalidades

- **Cards de estatística** — execuções do dia, taxa de sucesso, erros e tempo médio
- **Gráfico de barras** — execuções por hora nas últimas 8h
- **Gráfico de rosca** — distribuição por fluxo
- **Tabela de logs** — 10 execuções mais recentes com status, duração e detalhe
- **Banner de alerta** — aparece automaticamente quando erros excedem o limite
- **Atualização automática** — dados refreshados a cada 30 segundos

---

## Fluxo de monitoramento

```
Cenário Make.com executa
        ↓
Sucesso → INSERT na tabela logs (status: ok)
Erro    → INSERT na tabela logs (status: erro)
        ↓
Supabase armazena com payload completo
        ↓
Dashboard consulta via API REST
        ↓
Se erros > limite → alerta no Slack/WhatsApp
```

---

## Stack

| Ferramenta | Uso |
|---|---|
| **Make.com** | Error handler em cada cenário |
| **Supabase** | Banco de logs (PostgreSQL) |
| **SQL** | Queries de agregação para métricas |
| **Slack API** | Alertas em tempo real |
| **JavaScript** | Dashboard interativo |

---

## Estrutura da tabela de logs

```sql
CREATE TABLE logs_automacoes (
  id          UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at  TIMESTAMPTZ DEFAULT now(),
  fluxo       TEXT NOT NULL,
  status      TEXT CHECK(status IN ('ok', 'erro', 'aviso')),
  duracao_ms  INT,
  payload     JSONB,
  detalhe     TEXT
);

CREATE INDEX idx_logs_status    ON logs_automacoes(status);
CREATE INDEX idx_logs_created   ON logs_automacoes(created_at DESC);
```

---

## Como rodar localmente

1. Clone o repositório
2. Abra `projeto-03/index.html` no navegador
3. Os dados simulados carregam automaticamente
4. Clique em **Atualizar** para simular nova consulta ao banco

> Não precisa instalar nada — roda direto no navegador.

---

[← Voltar ao portfólio](https://github.com/MiqueiasRamosLima/portfolio-automacao)
