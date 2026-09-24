# BEAST MARAGAMES - Arquitetura de Telas & Fluxos

## Mapeamento Completo de Telas e Fluxos de Navegação

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

**Tela: Questionário de Perfil**
- Objetivo: Coletar informações sobre o participante
- Estrutura:
  - Indicador de progresso: "1/4"
  - Pergunta única por tela
  - Botões: "Próxima" | "Voltar"

**Pergunta 1: Faixa Etária**
```
Qual é sua idade?
○ 13-17 anos
○ 18-25 anos
○ 26-35 anos
○ 36-50 anos
○ 50+ anos
```

**Pergunta 2: Relação com Games**
```
Com que frequência você joga?
○ Jogo frequentemente
○ Jogo ocasionalmente
○ Tenho interesse mas jogo pouco
○ Estou conhecendo esse universo agora
```

**Pergunta 3: Interesse em Gêneros** (opcional)
```
Quais gêneros você gosta? (Selecione quantos quiser)
☐ Ação
☐ RPG
☐ Estratégia
☐ Esportes
☐ Puzzle
☐ Outros
```

**Pergunta 4: Confirmação**
```
Seus dados estão corretos?
[Dados coletados]

[Confirmar] [Editar]
```

- Validação:
  - Faixa etária é obrigatória
  - Outras perguntas opcionais
- Estados:
  - ✅ Questionário completo → Tela Home
  - ❌ Faixa etária vazia → Mensagem de erro

---

### ETAPA 3: HOME (TELA INICIAL)

**Estrutura Principal:**
```
┌─────────────────────────────┐
│ Saudação + Informações      │
├─────────────────────────────┤
│ [CARD PRINCIPAL]            │
│ Entrar em Evento            │
│ [QR Code] ou [Digitar Código]
├─────────────────────────────┤
│ Histórico / Eventos Próximos│
└─────────────────────────────┘

ABAS INFERIORES:
[Início] [Eventos] [Perfil]
```

**Componente 1: Saudação Personalizada**
```
Olá, [Nome]! 👋

Bem-vindo à BEAST Arena
Pronto para explorar?
```

**Componente 2: Card Principal - Entrar em Evento**
```
┌──────────────────────────┐
│  🎮 ENTRAR EM EVENTO    │
│                          │
│ [QR Code - Câmera]       │
│       ou                 │
│ [Digitar Código]         │
└──────────────────────────┘
```

**Componente 3: Histórico**
- Se primeira vez:
  ```
  Você ainda não participou de nenhum evento.
  Aperte "Entrar em Evento" para começar!
  ```

- Se já participou:
  ```
  Suas Participações:
  
  🎮 BEAST Arena - Shopping XYZ
  📅 15 de setembro de 2024
  ⏱️ 2h 45min
  ⭐ Avaliação: 4/5
  
  [Ver Detalhes]
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

**Tela: Evento em Andamento**
```
┌────────────────────────────┐
│  ARENA EM ANDAMENTO        │
├────────────────────────────┤
│  ⏱️ Tempo: 1h 30min        │
├────────────────────────────┤
│  Experiências:             │
│  ✅ PlayStation 14:35      │
│  ✅ VR Reality 15:10       │
│  ⭕ Simulador              │
│  ⭕ Outras...              │
├────────────────────────────┤
│  [Registrar Experiência]   │
│  [Sair da Arena]           │
└────────────────────────────┘
```

**Tela: Registrar Experiência (QR Code)**
```
┌────────────────────────────┐
│  Registrar Experiência     │
├────────────────────────────┤
│  [📷 Escanear QR Code]    │
│       ou                   │
│  Não conseguiu?            │
│  Peça ajuda ao monitor     │
├────────────────────────────┤
│  [Voltar]                  │
└────────────────────────────┘
```

**Estados da Tela durante Evento:**
- Sem experiências registradas
- Com algumas experiências
- Com todas experiências

---

### ETAPA 6: ENCERRAMENTO E AVALIAÇÃO

**Tela: Resumo do Evento**
```
┌────────────────────────────┐
│  ✅ Evento Finalizado      │
├────────────────────────────┤
│  BEAST Arena - Shopping XYZ│
│  Permanência: 2h 45min     │
│                            │
│  Experiências realizadas:  │
│  ✅ PlayStation            │
│  ✅ Realidade Virtual      │
│  ✅ Simulador de Corrida   │
├────────────────────────────┤
│  [Avaliar Experiência]     │
│  [Voltar à Home]           │
└────────────────────────────┘
```

**Tela: Avaliação**
```
┌────────────────────────────┐
│  Como foi sua experiência? │
├────────────────────────────┤
│  Nota:                     │
│  ⭐ ⭐ ⭐ ⭐ ⭐           │
│                            │
│  O que você mais gostou?   │
│  [Campo de texto opcional] │
│                            │
│  [Enviar] [Pular]         │
└────────────────────────────┘
```

**Após Avaliação:**
```
✅ Obrigado por participar!

Seu histórico foi salvo.
Volte em breve! 🎮

[Voltar à Home]
```

---

### ETAPA 7: HISTÓRICO E PÓS-EVENTO

**Aba: Eventos**
```
Meus Eventos

Participações:

📍 BEAST Arena - Shopping XYZ
📅 15 de setembro de 2024
⏱️ Permanência: 2h 45min
⭐ Avaliação: 4/5
[Ver Detalhes]

📍 BEAST Arena - Feira de Games
📅 10 de agosto de 2024
⏱️ Permanência: 1h 30min
[Ver Detalhes]
```

**Tela: Detalhes da Participação**
```
Arena: BEAST Arena - Shopping XYZ
Data: 15 de setembro de 2024

⏱️ Permanência: 2h 45min
   Entrada: 14:30
   Saída: 17:15

🎮 Experiências:
   ✅ PlayStation (14:35)
   ✅ Realidade Virtual (15:10)
   ✅ Simulador (16:20)

⭐ Sua Avaliação: 4/5
💬 Comentário: "Muito legal!"

[Voltar]
```

---

## 3. ESTADOS DE ERRO

### Erro: Câmera não funciona
```
⚠️ Câmera não disponível

Não conseguimos acessar sua câmera.

Opções:
[Tentar Novamente] ou [Digitar Código]
```

### Erro: Sem conexão internet
```
⚠️ Sem conexão

Você precisa de internet para registrar entrada.
Código do evento pode ser registrado offline.

[Tentar Novamente] [Digitar Código]
```

### Erro: QR Code inválido
```
❌ QR Code não reconhecido

O QR Code escaneado não é válido ou expirou.

[Tentar Novamente]
```

### Erro: Já registrado
```
⚠️ Você já está neste evento

Você já tem um registro ativo.

Opções:
[Continuar] [Sair do Evento]
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
- Histórico recente

### Aba 2: Eventos
- Lista de todos os eventos
- Detalhes de cada participação
- Estatísticas agregadas

### Aba 3: Perfil
- Dados pessoais
- Preferências
- Configurações
- Logout

---

## 5. FLUXO COMPLETO RESUMIDO

```
START
 ├─ Novo usuário?
 │   ├─ SIM → Cadastro → Perfil → Home
 │   └─ NÃO → Login → Home
 ├─ Home (saudação + histórico)
 ├─ [Entrar em Evento]
 │   ├─ QR Code
 │   │   ├─ Sucesso → Confirmação → Entra
 │   │   └─ Falha → Digitar Código
 │   └─ Código Manual → Confirmação → Entra
 ├─ Evento em andamento (timer + experiências)
 │   ├─ Registra experiências (QR Code)
 │   └─ [Sair da Arena]
 ├─ Resumo + Avaliação
 │   └─ [Avaliar] ou [Pular]
 ├─ Volta à Home
 └─ Histórico atualizado
```

---

## 6. PADRÕES DE DESIGN

- **Navegação**: Abas inferiores (padrão mobile)
- **Entrada de Dados**: Campos simples, validação clara
- **Feedback**: Mensagens de sucesso/erro sempre visíveis
- **CTA Principal**: Card grande destacado na Home
- **Cores**: Roxo e vermelho (identidade BEAST)
- **Tipografia**: Clean e legível em dispositivos pequenos

