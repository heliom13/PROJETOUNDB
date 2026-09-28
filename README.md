# 🎮 BEAST MARAGAMES

Aplicativo da Arena Gamer itinerante da BEAST: participante, área do Staff e monitor público | Projeto Acadêmico

Site publicado: https://projetoundb.onrender.com/

---

## 📋 Arquivos

| Arquivo | Conteúdo |
|---------|----------|
| `index.html` | Página inicial com as quatro áreas do projeto |
| `beast_arena_prototipo_integrado.html` | Protótipo estrutural + abas Documentação Completa, Análise de Decisões e Arquitetura de Telas |
| `DELIVERABLE_COMPLETO.html` | Documentação Completa (exibida na aba "Documentação Completa") |
| `ANALISE_DECISOES.md` | Análise de Decisões em Markdown (mesmo conteúdo da aba "Análise de Decisões") |
| `ARQUITETURA_TELAS.md` | Arquitetura de Telas & Fluxos em Markdown (mesmo conteúdo da aba "Arquitetura de Telas") |
| `prototipo.html` | Redireciona para o protótipo integrado (mantém links antigos funcionando) |

A Análise e a Arquitetura exibidas no site ficam embutidas em `beast_arena_prototipo_integrado.html` (blocos `md-analise` e `md-arquitetura`). Ao editar os `.md`, atualize também esses blocos.

---

## 📱 Protótipo Estrutural

O protótipo HTML demonstra estrutura, fluxos principais, estados e regras. **Não** é o design visual final e não contém todas as telas secundárias (Login, Cadastro e Recuperação de senha serão desenhadas no Figma).

Representa: questionário de perfil em 3 etapas, Home, Minhas Participações, Perfil, entrada por QR Code ou código, confirmação, fila de acesso à Arena, Arena em andamento, filas das estações, chamada, conclusão pelo Staff, saída com confirmação, avaliação opcional, detalhes, área do Staff e monitor público — todos compartilhando o mesmo estado.

---

## 🎨 Identidade Visual

As cores e a tipografia do protótipo são provisórias. A identidade visual definitiva será desenvolvida no **Figma**.

---

## 📊 Status

- ✅ Estrutura, fluxos e interfaces consolidados
- ✅ Regras de negócio principais definidas
- ⏳ Identidade visual e telas completas no Figma
- 🔍 Em avaliação: backend, banco de dados, sincronização em tempo real, comportamento offline, papel do Google Drive (informado pela empresa como armazenamento)

---

## 🚀 Deploy

Site estático no Render (`render.yaml`, publish path `.`). Cada `git push` na branch `main` dispara um novo deploy.
