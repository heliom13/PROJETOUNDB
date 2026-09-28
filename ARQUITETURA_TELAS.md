# BEAST MARAGAMES - Arquitetura de Telas & Fluxos

## Mapeamento Completo de Telas, Interfaces e Fluxos

**Nota:** Esta arquitetura integra três contextos principais:
- 📱 **Participante** (aplicativo mobile)
- 👨‍💼 **Staff** (área restrita - tablet/dispositivo)
- 📊 **Monitor** (tela pública na Arena)

---

## 1. ESTRUTURA DE NAVEGAÇÃO

```
┌─────────────────────────────────────┐
│      TELA DE AUTENTICAÇÃO           │
│  (Boas-vindas, Login, Cadastro)     │
└────────────┬────────────────────────┘
             │
             ↓
┌─────────────────────────────────────┐
│    PERFIL DO PARTICIPANTE           │
│  (Questionário de Identificação)    │
└────────────┬────────────────────────┘
             │
             ↓
┌─────────────────────────────────────┐
│       HOME (TELA INICIAL)           │
│  ├─ Abas: Início | Eventos | Perfil│
│  ├─ Card principal: Entrar Evento  │
│  └─ Histórico de participações     │
└────────────┬────────────────────────┘
             │
     ┌───────┴───────┐
     ↓               ↓
  [Evento]      [Perfil]
```

---

## 2. FLUXO JORNADA DO PARTICIPANTE

### ETAPA 1: AUTENTICAÇÃO

**Tela: Boas-vindas**
- Objetivo: Apresentar aplicativo e oferecer opções de acesso
- Componentes:
  - Logo BEAST MARAGAMES
  - Tagline: "Viva a experiência dos jogos"
  - Botão: "Criar Conta"
  - Botão: "Já tenho uma conta"
- Navegação:
  - "Criar Conta" → Tela de Cadastro
  - "Já tenho uma conta" → Tela de Login

**Tela: Cadastro**
- Objetivo: Criar nova conta
- Campos:
  - Nome (obrigatório)
  - E-mail (obrigatório, com validação)
  - Senha (obrigatório, mín. 8 caracteres)
  - Confirmar Senha (obrigatório)
- Validação:
  - ❌ E-mail já cadastrado
  - ❌ Senhas não conferem
  - ❌ Campos obrigatórios vazios
- Estados:
  - ✅ Cadastro bem-sucedido → Tela Perfil
  - ❌ Erro → Mensagem e opção de tentar novamente

**Tela: Login**
- Objetivo: Autenticar usuário
- Campos:
  - E-mail (obrigatório)
  - Senha (obrigatório)
- Validação:
  - ❌ Credenciais inválidas
  - ❌ Usuário não existe
- Ações:
  - "Esqueci minha senha" → Recuperação de senha
- Estados:
  - ✅ Login bem-sucedido → Tela Home (ou Perfil se primeira vez)
  - ❌ Erro → Mensagem de erro

**Tela: Recuperação de Senha**
- Objetivo: Permitir reset de senha
- Fluxo:
  1. Usuário digita e-mail
  2. Sistema envia link de reset
  3. Usuário recebe e-mail
  4. Clica em link → Nova senha
  5. Retorna ao Login

---

### ETAPA 2: PERFIL DO PARTICIPANTE

**Tela: Questionário de Perfil - 3 Etapas**

Nota: O cadastro básico (Nome, E-mail, Senha) foi feito na tela anterior. Este questionário coleta preferências.

---

**ETAPA 2.1: SOBRE VOCÊ**

Indicador: "1/3"

**Pergunta: Idade**
```
Qual é a sua idade?
[____ ] (campo numérico)
```
Obrigatório.

**Pergunta: Gênero**
```
Como você se identifica?
○ Feminino
○ Masculino
○ Outro [Especifique: _____]
○ Prefiro não informar
```
Obrigatório. Se "Outro" selecionado, campo de especificação é OBRIGATÓRIO.

**Pergunta: Escolaridade**
```
Qual o nível mais alto de ensino que você cursa ou já cursou?
○ Ensino Fundamental
○ Ensino Médio
○ Ensino Superior
○ Pós-graduação
○ Prefiro não informar
```
Obrigatório.

---

**ETAPA 2.2: SEUS JOGOS**

Indicador: "2/3"

**Pergunta: Jogos que costuma jogar**
```
Quais jogos você costuma jogar?
[Pesquisar: ________]

Selecionados:
[Valorant ×] [Minecraft ×] [Elden Ring ×]

[+ Adicionar outro]
```
Obrigatório. Mínimo 1 jogo. Permite pesquisa, seleção de sugestões ou adição manual.

---

**ETAPA 2.3: MERCADO DE GAMES**

Indicador: "3/3"

**Pergunta 1: Conhecimento do Mercado**
```
Você já conhece o mercado de games?
○ Sim, conheço
○ Conheço um pouco
○ Não conheço
```
Obrigatório.

**Pergunta 2: Interesse Profissional**
```
Você tem interesse no mercado profissional de games?
○ Sim, tenho interesse
○ Talvez / Quero conhecer melhor
○ Não tenho interesse
```
Obrigatório.

---

**Finalização:**
- ✅ Questionário completo → Home
- Sem tela de confirmação extra
- Dados editáveis posteriormente no Perfil

---

### ETAPA 3: HOME (TELA INICIAL)

**Estrutura Principal:**
```
┌──────────────────────────┐
│ Saudação                 │
├──────────────────────────┤
│ [🎮 ENTRAR EM EVENTO]   │
│                          │
│ [QR Code] ou [Código]   │
├──────────────────────────┤
│ Participações Recentes   │
│ (máximo 2)               │
│ [Ver todas]              │
└──────────────────────────┘

ABAS INFERIORES:
[🏠 Início] [📍 Eventos] [👤 Perfil]
```

**Componente 1: Saudação**
```
Olá, [Nome]! 👋
Bem-vindo à BEAST Arena
```

**Componente 2: Card Principal - CTA Único**
```
🎮 ENTRAR EM EVENTO

[📷 Câmera (QR Code)]
ou
[⌨️ Digitar Código]
```

**Componente 3: Participações Recentes**
- 0 participações:
  ```
  Você ainda não participou de nenhum evento.
  ```

- 1 a 2 participações:
  ```
  Suas Participações Recentes:
  
  BEAST Arena - Shopping XYZ
  📅 15 set  |  ⏱️ 2h 45min  |  ⭐ 4/5
  [Ver detalhes]
  ```

- 3+ participações:
  ```
  Suas Participações Recentes:
  
  BEAST Arena - Shopping XYZ (15 set)
  BEAST Arena - Feira de Games (10 ago)
  
  [Ver todas]  ← leva à aba Eventos
  ```

---

### ETAPA 4: ENTRADA NO EVENTO

**Fluxo QR Code:**
```
Home
 ├─ [Entrar em Evento]
 ├─ [QR Code]
 ├─ Câmera abre
 ├─ Escaneia QR Code
 ├─ Sistema identifica evento
 └─ Mostra confirmação
     ├─ [Confirmar] → Entra
     └─ [Cancelar] → Volta Home
```

**Tela: Confirmação de Entrada**
```
┌──────────────────────────┐
│  Confirmar Entrada      │
│                          │
│  🏟️ BEAST Arena         │
│  📍 Shopping XYZ        │
│  📅 15 de Setembro      │
│  🎮 PlayStation, VR...  │
│                          │
│  [✅ Entrar] [❌ Cancelar]
└──────────────────────────┘
```

**Fluxo Código Manual (Fallback):**
```
[QR Code falhou]
 ├─ "Não conseguiu?"
 ├─ [Digitar Código]
 ├─ Participante digita: BEAST2024
 ├─ Sistema identifica evento
 └─ Mostra confirmação (igual acima)
```

**Tela: Entrada Confirmada**
```
✅ Você entrou no evento!

Tempo de permanência:
[Timer em tempo real]

Experiências disponíveis:
🎮 PlayStation
🥽 Realidade Virtual
🚗 Simulador

[Aproveite! 🎮]
```

---

### ETAPA 5: PARTICIPAÇÃO DURANTE EVENTO

**Tela: Arena em Andamento**
```
┌────────────────────────────┐
│  ARENA EM ANDAMENTO        │
├────────────────────────────┤
│  ⏱️ 1h 30min               │
├────────────────────────────┤
│  ESTAÇÕES & FILAS:         │
│                            │
│  🎮 PlayStation            │
│  Disponível (4 esperando)  │
│  [Entrar na fila]          │
│                            │
│  🥽 VR Reality             │
│  Você está na fila         │
│  Posição: 3º               │
│  [Sair da fila]            │
│                            │
│  🚗 Simulador              │
│  Disponível (0 esperando)  │
│  [Entrar na fila]          │
├────────────────────────────┤
│  CONCLUÍDAS:               │
│  ✅ PlayStation (14:35)    │
├────────────────────────────┤
│  [Sair da Arena]           │
└────────────────────────────┘
```

**Estados Possíveis de Estação:**

1. **Disponível:**
   ```
   PlayStation
   Disponível (2 pessoas esperando)
   [Entrar na fila]
   ```

2. **Você aguardando:**
   ```
   VR Reality
   Você está na fila
   Posição: 3º
   [Sair da fila]
   ```

3. **Chamado (É sua vez!):**
   ```
   PlayStation
   🔔 É A SUA VEZ!
   Dirija-se ao estande.
   [Já estou aqui]
   ```

4. **Concluída:**
   ```
   ✅ PlayStation (concluída às 14:35)
   ```

**Comportamento:**
- Participante pode estar em apenas UMA fila por vez
- Ao entrar em uma fila, outras ficam desabilitadas
- Ao sair da fila, fica livre novamente
- Quando chamado, recebe notificação clara

---

### ETAPA 6: ENCERRAMENTO E AVALIAÇÃO

**Tela: Resumo Automático**
```
┌────────────────────────────┐
│  ✅ Participação Finalizada│
├────────────────────────────┤
│  BEAST Arena - Shopping XYZ│
│  📅 15 de setembro         │
│  ⏱️ Permanência: 2h 45min  │
│  🕐 Entrada: 14:30         │
│  🕕 Saída: 17:15           │
│                            │
│  Experiências concluídas:  │
│  ✅ PlayStation (14:35)    │
│  ✅ VR Reality (15:10)     │
│  ✅ Simulador (16:20)      │
├────────────────────────────┤
│  [Avaliar] [Pular]         │
└────────────────────────────┘
```

**Tela: Avaliação (Simplificada)**
```
┌────────────────────────────┐
│  Avalie sua experiência    │
├────────────────────────────┤
│  Nota:                     │
│  ⭐ ⭐ ⭐ ⭐ ⭐ (clicável) │
│                            │
│  Quer contar mais sobre    │
│  sua experiência?          │
│  [Campo de texto opcional] │
│                            │
│  [Enviar] [Pular]         │
└────────────────────────────┘
```

**Após Avaliar ou Pular:**
```
✅ Obrigado por participar!

Seu histórico foi salvo.
Volte em breve! 🎮

[Voltar à Home]
```

**Nota:**
- Avaliação é opcional
- Não mostrar tela adicional de "confirmação de dados"
- Dados automáticos (entrada, saída, permanência, experiências) são registrados sem ação do participante

---

### ETAPA 7: HISTÓRICO DE PARTICIPAÇÕES

**Aba: Eventos (título interno: "Minhas Participações")**
```
Minhas Participações

Total: 5 participações

BEAST Arena - Shopping XYZ
📅 15 set 2024  |  ⏱️ 2h 45min  |  ⭐ 4/5
[Ver detalhes]

BEAST Arena - Feira de Games
📅 10 ago 2024  |  ⏱️ 1h 30min
[Ver detalhes]

[Mais participações...]
```

**Tela: Detalhes da Participação**
```
BEAST Arena - Shopping XYZ

📅 15 de setembro de 2024
🕐 Entrada: 14:30
🕕 Saída: 17:15
⏱️ Permanência: 2h 45min

Experiências concluídas:
✅ PlayStation (14:35)
✅ Realidade Virtual (15:10)
✅ Simulador de Corrida (16:20)

Sua avaliação: ⭐⭐⭐⭐ (4 estrelas)
"Muito legal! Adorei a experiência."

[Voltar]
```

---

## 3. ESTADOS DE ERRO & FALLBACKS

### Erro: Câmera não disponível
```
⚠️ Câmera não funcionando

Não conseguimos acessar sua câmera.

Opções:
[Tentar Novamente] [Digitar Código]
```

### Erro: Sem conexão internet
```
⚠️ Sem conexão

Você precisa de internet para entrar no evento.

[Tentar Novamente]
```

### Erro: QR Code inválido
```
❌ QR Code não reconhecido

O QR Code escaneado não é válido.

[Tentar Novamente] [Digitar Código]
```

### Erro: Código inválido
```
❌ Código não encontrado

Verifique o código e tente novamente.

[Tentar Novamente]
```

### Erro: Participação ativa
```
⚠️ Você já está em um evento

Você já possui uma participação ativa.
Finalize antes de entrar em outro.

[Continuar evento] [Sair do evento]
```

### Erro: Fila de acesso cheia
```
ℹ️ Fila de acesso cheia

A Arena está com capacidade máxima.
Você foi adicionado à fila.

Sua posição: 5º
Tempo estimado: ~15 min

[Aguardar]
```

---

## 4. NAVEGAÇÃO INFERIOR (ABAS)

```
┌─────────────────────────────────┐
│ [🏠 Início] [📍 Eventos] [👤 Perfil]│
└─────────────────────────────────┘
```

### Aba 1: Início
- Home principal
- Card de entrada no evento
- 2 participações recentes (máximo)

### Aba 2: Eventos
**Título interno:** "Minhas Participações"
- Histórico completo de participações
- Detalhes de cada participação
- Filtros e buscas (futuros)

### Aba 3: Perfil
- Dados pessoais
- Dados do questionário (editáveis)
- Estatísticas:
  - X Participações
  - Y Tempo total
  - Z Experiências realizadas
- Configurações
- Logout

**Exemplo de Estatísticas:**
```
5 Participações
8h Tempo total
12 Experiências realizadas
```

---

## 5. INTERFACE DO STAFF (ÁREA RESTRITA)

**Acesso:** Tablet/celular com autenticação.

**Funcionalidades Principais:**
1. Visualizar filas em tempo real
2. Chamar participante
3. Registrar ausência (no-show)
4. Confirmar conclusão de experiência
5. Controlar fila de acesso da Arena

**Telas Principais:**

**Tela: Gerenciador de Filas**
```
Filas Ativas

🎮 PlayStation
  Agora: João S.
  Próximo: Maria A.
  Esperando: 4
  [Confirmar Conclusão] [No-show]

🥽 VR Reality
  Agora: -
  Próximo: Pedro M.
  Esperando: 2
  [Chamar próximo]

[Controlar Fila de Acesso]
```

**Comportamentos:**
- Sincroniza em tempo real com app dos participantes
- Staff confirma conclusão → atualiza histórico + libera fila
- No-show → participante retorna ao final da fila
- Fila de acesso pode ser ativada/desativada dinamicamente

---

## 6. INTERFACE DO MONITOR (TELA PÚBLICA)

**Local:** Tela/monitor na Arena visível para participantes.

**Exibição em Tempo Real:**

```
┌────────────────────────────┐
│  ARENA MARAGAMES           │
│  🕐 14:35                  │
├────────────────────────────┤
│  CHAMADAS AGORA:           │
│                            │
│  🎮 PlayStation            │
│  ➜ João S.                 │
│  ⏭️ Maria A.               │
│                            │
│  🥽 VR Reality             │
│  ➜ Pedro M.                │
│  ⏭️ Ana C.                 │
│                            │
│  🚗 Simulador              │
│  ➜ Lucas P.                │
│  ⏭️ Sofia T.               │
└────────────────────────────┘
```

**Dados Exibidos:**
- Estação
- Nome do participante (primeira nome + inicial ou código)
- Próximo a ser chamado (opcional)
- Atualização em tempo real

**Privacidade:**
- Exibir apenas primeira nome + inicial (ex: "João S.")
- NÃO exibir: e-mail, idade, gênero, nome completo

---

## 7. FLUXO COMPLETO RESUMIDO

**Fluxo Completo do Participante:**
```
START
 ├─ Novo usuário?
 │   ├─ SIM → Cadastro → Questionário (3 etapas) → Home
 │   └─ NÃO → Login → Home (ou Questionário se incompleto)
 ├─ Home (saudação + 2 participações recentes)
 ├─ [Entrar em Evento]
 │   ├─ QR Code (câmera)
 │   │   ├─ Sucesso → Confirmação → Verificar fila de acesso
 │   │   └─ Falha → Digitar Código (fallback)
 │   └─ Se houver fila de acesso ativa → Aguardar chamada
 ├─ Entrada efetiva na Arena
 │   ├─ Timer começa
 │   ├─ Tela: Arena em Andamento
 │   │   ├─ Exibe estações com filas
 │   │   ├─ Participante pode entrar em UMA fila por vez
 │   │   └─ Recebe notificações quando chamado
 │   ├─ Participante aguarda → é chamado → realiza experiência
 │   ├─ Staff confirma conclusão → experiência registrada
 │   └─ Participante fica livre para outra fila
 ├─ [Sair da Arena]
 │   ├─ Confirmação
 │   ├─ Se em fila → Remove automaticamente
 │   └─ Timer para
 ├─ Resumo automático + Avaliação simplificada
 │   └─ [Avaliar] ou [Pular]
 ├─ Volta à Home
 └─ Participação aparece em "Minhas Participações"
```

**Pontos-chave:**
- Uma participação ativa por vez
- Uma fila de estação por vez
- Dados automáticos (sem ação do participante)
- Staff confirma experiências
- Monitor exibe chamadas em tempo real

---

## 8. PADRÕES DE DESIGN & PRINCÍPIOS UX

### Navegação
- Abas inferiores (padrão mobile)
- Hierarquia clara (principal + secundário)
- Volta fácil (breadcrumb ou botão voltar)

### Coleta de Dados (Baixa Fricção)
- Questionário: 3 etapas curtas (não uma por tela)
- Automático quando possível (entrada, saída, permanência)
- Opcional quando baixo valor (comentário na avaliação)

### Feedback do Sistema
- Notificações claras quando chamado
- Estados visuais distintos (aguardando, concluído, disponível)
- Confirmações para ações perigosas (sair da Arena)

### CTA Principal
- Um único CTA principal por tela ("Entrar em Evento")
- Evitar duplicidade

### Privacidade
- Monitor exibe apenas primeiro nome + inicial
- NÃO exibir dados sensíveis na tela pública

### Design Visual (Provisório)
- Estrutura: Roxo (#8B4789) + Vermelho (#C41E3A)
- Tipografia: System fonts (legível em mobile)
- Layout: Mobile-first, responsivo
- **Nota:** Identidade visual definitiva será no Figma

