## NL2Metrics: Pipeline de Intelligence Analytics para Feedback Bancário

## Visão Geral do Solução
Este projeto implementa um pipeline de dados baseado em LLM (Large Language Model) para transformar feedbacks não estruturados de clientes bancários em métricas acionáveis (NL2Metrics). A solução aplica o framework **ABSA (Aspect-Based Sentiment Analysis)**, garantindo conformidade rigorosa com **LGPD / BACEN** através de sanitização automatizada de PII.

---

## Arquitetura de Dados (Medalhão)

1. **Bronze (Raw Ingestion):** Captura feedbacks multicanal (Play Store, NPS, Reclame Aqui, Redes Sociais) mantendo metadados brutos e textos não sanitizados.
2. **Silver (Enriched & Sanitized):** Processamento via LLM aplicando o `system_prompt.md`. Os dados são higienizados (remoção de PII), categorizados na taxonomia ABSA de 3 níveis e persistidos em formato estruturado (JSON/SQL).
3. **Gold (Analytics & Dashboards):** Tabela analítica agregada com pesos de urgência (1 a 4) direcionada para os Sponsors de **SRE/Infra**, **Product Managers (Mobile/UX)** e **Atendimento/Ops**.

---

## Governança e Segurança de Dados (LGPD / BACEN)
- **Substituição Determinística:** Mascaramento de nomes, CPFs, CNPJs, dados bancários e chaves Pix.
- **Auditoria:** Flag `pii_detectado: boolean` para rastreabilidade de compliance.
- **Zero-Data Leakage:** Garantia de que a Camada Silver e Gold contenham apenas dados anonimizados.

---

## Arquivos do Repositório
- [`system_prompt.md`](./system_prompt.md): Prompt de Engenharia completo com System Instructions, Contratos de Dados e Exemplos Few-Shot.
