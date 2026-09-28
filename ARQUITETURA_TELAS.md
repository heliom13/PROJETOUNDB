# BEAST MARAGAMES - Arquitetura de Telas & Fluxos

## Mapeamento de Telas, Interfaces e Fluxos de Navegação

> **Sobre este documento**
> - Esta página documenta as telas, interfaces, navegação, estados e fluxos previstos para o sistema.
> - O **protótipo HTML** é um protótipo **estrutural/funcional**: demonstra os principais fluxos, estados, regras, navegação e comportamento do sistema. Ele não representa o design visual definitivo e não precisa conter todas as telas secundárias.
> - O **Figma** será responsável pelo design completo das interfaces e pela identidade visual. Telas como Login, Cadastro e Recuperação de Senha constam nesta arquitetura e serão desenhadas no Figma, mesmo que não estejam no protótipo HTML.
> - Algumas telas listadas aqui são estados de uma mesma tela, e não telas independentes. Por isso, não há uma contagem fixa de telas.

---

## 1. VISÃO GERAL DO SISTEMA

O sistema é composto por três interfaces que participam do funcionamento do evento e, principalmente, das filas:

```
                      SISTEMA BEAST ARENA
                              │
         ┌────────────────────┼────────────────────┐
         ↓                    ↓                    ↓
 APP DO PARTICIPANTE    ÁREA DO STAFF       MONITOR PÚBLICO
    (mobile)          (área restrita)      (tela da Arena)
         │                    │                    │
         └────────────────────┼────────────────────┘
                              ↓
              ┌───────────────────────────────┐
              │  ESTADO OPERACIONAL DO EVENTO │
              │  • Fila de acesso à Arena     │
              │  • Filas das estações         │
              │  • Chamadas e conclusões      │
              └───────────────────────────────┘
```

**Terminologia:**
- **EVENTO** = evento/Arena promovido pela BEAST
- **PARTICIPAÇÃO** = registro específico de um usuário naquele evento

"Evento" e "participação" não são sinônimos.

---

## 2. ESTRUTURA DE NAVEGAÇÃO DO PARTICIPANTE

```
┌─────────────────────────────────────┐
│      AUTENTICAÇÃO                   │
│  (Boas-vindas, Cadastro, Login,     │
│   Recuperação de senha)             │
└────────────┬────────────────────────┘
             │ (novo usuário ou perfil
             │  ainda não preenchido)
             ↓
┌─────────────────────────────────────┐
│    QUESTIONÁRIO DE PERFIL           │
│  (3 etapas curtas)                  │
└────────────┬────────────────────────┘
             │
             ↓
┌─────────────────────────────────────┐
│       HOME (TELA INICIAL)           │
│  ├─ Abas: Início | Eventos | Perfil │
│  ├─ CTA: Entrar em Evento           │
│  └─ Até 2 participações recentes    │
└────────────┬────────────────────────┘
             │
     ┌───────┼────────────┐
     ↓       ↓            ↓
[Entrar em  [Eventos:    [Perfil]
 Evento]    Minhas
            Participações]
```

---

## 3. JORNADA DO PARTICIPANTE

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
- Campos (somente):
  - Nome (obrigatório)
  - E-mail (obrigatório, com validação)
  - Senha (obrigatório, mín. 8 caracteres)
  - Confirmar Senha (obrigatório)
- Observações:
  - "Confirmar senha" é uma validação do cadastro, não um dado de perfil armazenado
  - Informações demográficas e de games **não** são coletadas no cadastro, e sim no questionário de perfil
- Validação:
  - ❌ E-mail já cadastrado
  - ❌ Senhas não conferem
  - ❌ Campos obrigatórios vazios
- Estados:
  - ✅ Cadastro bem-sucedido → Questionário de Perfil
  - ❌ Erro → Mensagem e opção de tentar novamente

**Tela: Login**
- Objetivo: Autenticar usuário
- Campos:
  - E-mail (obrigatório)
  - Senha (obrigatório)
- Ações:
  - "Esqueci minha senha" → Recuperação de senha
- Validação:
  - ❌ Credenciais inválidas
- Estados:
  - ✅ Usuário com perfil preenchido → Home
  - ✅ Usuário com perfil inicial ainda não preenchido → Questionário de Perfil → Home
  - ❌ Erro → Mensagem de erro

**Tela: Recuperação de Senha**
- Objetivo: Permitir redefinição de senha
- Fluxo conceitual:
  1. "Esqueci minha senha"
  2. Usuário informa o e-mail
  3. Recebe mecanismo/link de recuperação
  4. Define nova senha
  5. Retorna ao Login
- Faz parte da arquitetura e do futuro Figma; não precisa ser representada no protótipo HTML estrutural.

---

### ETAPA 2: QUESTIONÁRIO DE PERFIL

**Objetivo:** coletar dados relevantes para a BEAST com o menor atrito possível.

**Estrutura:**
- 3 etapas curtas, com indicador de progresso ("Etapa 1 de 3")
- Botões: "Continuar" | "Voltar"
- O nome **não** é perguntado novamente (já coletado no cadastro)
- Ao terminar: **Questionário concluído → Home** (sem tela adicional de confirmação dos dados)
- Os dados podem ser alterados posteriormente no Perfil

**Regra geral para "Outro":** sempre que uma pergunta possuir a opção "Outro", selecioná-la abre um campo para especificação, que passa a ser obrigatório para validar a resposta. Isso não significa que todas as perguntas tenham a opção "Outro".

**Etapa 1 — Sobre você**
```
Qual é a sua idade?
[ campo numérico ]                    (obrigatório)

Como você se identifica?              (obrigatório)
○ Feminino
○ Masculino
○ Outro  → [ especifique ]            (obrigatório se "Outro")
○ Prefiro não informar

Qual o nível mais alto de ensino que você cursa ou já cursou?
○ Ensino Fundamental                  (obrigatório)
○ Ensino Médio
○ Ensino Superior
○ Pós-graduação
○ Prefiro não informar
```
- Idade é coletada como número, não como faixa etária
- "Prefiro não informar" é resposta válida em gênero e escolaridade
- Escolaridade **não** possui "Outro" e **não** separa completo/incompleto/cursando. Exemplos:
  - Atualmente no Ensino Médio → Ensino Médio
  - Cursando ou já concluiu faculdade → Ensino Superior
  - Fez faculdade e atualmente não estuda → Ensino Superior
  - Cursando ou já cursou pós-graduação → Pós-graduação

**Etapa 2 — Seus jogos**
```
Quais jogos você costuma jogar?

[ 🔍 Pesquisar jogo...            ]
  Resultados/sugestões para seleção
  Não encontrou? [+ Adicionar "nome digitado"]

Selecionados:
[Valorant ×] [Minecraft ×]
```
- Evita um grande campo de texto livre: pesquisa → sugestões → seleção → tags/chips
- Obrigatório informar **pelo menos 1 jogo**; com um jogo selecionado a pergunta já é válida
- Jogo informado manualmente (quando não está na lista) conta como seleção válida
- Não há número máximo de jogos definido neste momento

**Etapa 3 — Mercado de games**
```
Você já conhece o mercado de games?    (obrigatório)
○ Sim, conheço
○ Conheço um pouco
○ Não conheço

Você tem interesse no mercado profissional de games?   (obrigatório)
○ Sim, tenho interesse
○ Talvez / Quero conhecer melhor
○ Não tenho interesse
```
- A BEAST informou que essas duas perguntas poderão ser usadas futuramente para direcionar participantes a conhecer sua plataforma
- **Pendente:** o mecanismo desse direcionamento ainda não foi definido; nenhuma tela, popup, link ou CTA específico faz parte desta arquitetura por enquanto

---

### ETAPA 3: HOME (TELA INICIAL)

**Estrutura Principal:**
```
┌─────────────────────────────┐
│ Saudação                    │
├─────────────────────────────┤
│ [CTA PRINCIPAL]             │
│ Entrar em Evento            │
├─────────────────────────────┤
│ Participações Recentes      │
│ (até 2)          [Ver todas]│
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

**Componente 2: CTA Principal**
```
┌──────────────────────────┐
│  🎮 ENTRAR EM EVENTO     │
└──────────────────────────┘
```
- Único CTA principal de entrada na Home (não há um segundo botão como "Iniciar Participação")
- A escolha entre QR Code e código manual acontece na tela seguinte (Identificação do Evento)

**Componente 3: Participações Recentes**
- 0 participações → estado vazio:
  ```
  Você ainda não participou de nenhum evento.
  Toque em "Entrar em Evento" para começar!
  ```
- 1 participação → mostra uma
- 2 ou mais → mostra somente as duas mais recentes:
  ```
  Participações Recentes              [Ver todas]

  🎮 BEAST Arena - Shopping XYZ
  📅 15 de setembro
  ⏱️ 2h 45min
  ⭐ 4/5
  ```
- "Ver todas" → aba Eventos → Minhas Participações

---

### ETAPA 4: ENTRADA NO EVENTO

**Fluxo:**
```
Home
 ├─ [Entrar em Evento]
 ├─ Identificação do evento
 │   ├─ QR Code (principal)
 │   └─ Código manual (alternativa)
 ├─ Sistema identifica o evento
 └─ Confirmar Entrada
     ├─ [Confirmar] → Entrada efetiva ou Fila de acesso
     └─ [Cancelar]  → Volta Home
```

**Tela: Identificação do Evento**
```
┌──────────────────────────┐
│  Entrar em Evento        │
│                          │
│  [📷 Escanear QR Code]   │
│                          │
│  Não conseguiu?          │
│  [Digitar Código]        │
└──────────────────────────┘
```
- QR Code e código manual são duas formas de **identificar o evento**
- O código manual **não** é uma solução offline; o comportamento sem conexão depende da arquitetura técnica, ainda não definida

**Tela: Confirmar Entrada**
```
┌──────────────────────────┐
│  Confirmar Entrada       │
│                          │
│  🏟️ BEAST Arena          │
│  📍 Shopping XYZ         │
│  📅 15 de Setembro       │
│  🎮 PlayStation, VR...   │
│                          │
│  [✅ Entrar] [❌ Cancelar]│
└──────────────────────────┘
```
- Após identificar um QR/código válido, a entrada **não** é registrada imediatamente
- O participante vê as informações do evento e só então confirma

**Regra: somente uma participação ativa**
- Um participante pode possuir somente **uma participação ativa por vez**
- Enquanto estiver participando de um evento/Arena, não pode iniciar participação em outro evento
- Evita conflitos de tempo de permanência, filas, experiências e estado atual do participante
- Tentativa de entrar em outro evento com participação ativa → mensagem (ver Estados de Erro)

---

### ETAPA 5: FILA DE ACESSO À ARENA (OPCIONAL)

A fila de acesso **não** é uma configuração fixa do evento. O Staff pode ativá-la ou desativá-la durante o evento conforme a lotação.

```
Fila de acesso: NÃO
 → Confirmar Entrada
 → Entrada efetiva na Arena
 → Arena em andamento

Fila de acesso: SIM
 → Confirmar Entrada
 → Fila de acesso (acompanha espera/posição)
 → Liberação
 → Entrada efetiva na Arena
 → Arena em andamento
```

**Tela: Fila de Acesso**
```
┌────────────────────────────┐
│  Fila de acesso à Arena    │
├────────────────────────────┤
│  🏟️ BEAST Arena            │
│  Sua posição: 5º           │
│                            │
│  Você será liberado para   │
│  entrar em breve.          │
└────────────────────────────┘
```

**Regras:**
- O tempo aguardando na fila de acesso **não** conta como tempo de permanência
- O timer de permanência começa somente quando a entrada efetiva é liberada/registrada
- **Desativação com pessoas aguardando:** se o Staff desativar a fila, **todos** os participantes aguardando são liberados automaticamente (sem liberação individual). Nesse momento a espera termina, a entrada efetiva é registrada e o tempo de permanência começa
- Participantes que já estavam dentro da Arena não são afetados

---

### ETAPA 6: ARENA EM ANDAMENTO E FILAS DAS ESTAÇÕES

**Tela: Arena em Andamento**
```
┌─────────────────────────────────────┐
│  ARENA EM ANDAMENTO                 │
│  BEAST Arena - Shopping XYZ         │
├─────────────────────────────────────┤
│  ⏱️ Tempo na Arena: 1h 30min        │
├─────────────────────────────────────┤
│  Experiências:                      │
│  ✅ PlayStation — Concluída às 14:35│
│  ⏳ VR — Na fila · Posição: 3º      │
│     [Sair da fila]                  │
│  🚗 Simulador — [Entrar na fila]    │
│     (indisponível: você já está     │
│      na fila de VR)                 │
├─────────────────────────────────────┤
│  [Sair da Arena]                    │
└─────────────────────────────────────┘
```

- Mostra: nome do evento, tempo de permanência, experiências/estações disponíveis, estado de cada experiência e a ação "Sair da Arena"
- O timer representa **tempo dentro da Arena** (não inclui a fila de acesso)
- Não existe botão de registro manual de experiência nem QR Code por estação: a experiência é registrada pela confirmação do Staff

**Filas das estações**
- Cada estação/estande possui sua própria fila (ex.: PlayStation, VR, Simulador)
- **Regra:** um participante pode estar em apenas **uma fila de estação por vez**

```
Arena em andamento
 → escolhe uma estação
 → [Entrar na fila]
 → aguarda e acompanha posição
 → é chamado
 → dirige-se ao estande
 → realiza a experiência
 → Staff confirma conclusão
 → participante fica livre para entrar em outra fila
```

**Enquanto estiver em uma fila:**
- Mostra a estação e a posição
- Permite "Sair da fila"
- As demais experiências continuam visíveis, mas a ação de entrar em outra fila fica indisponível, com mensagem explicando que o participante já está em outra fila

**Chamada do participante**
```
┌────────────────────────────┐
│  🔔 É a sua vez!           │
│                            │
│  Dirija-se ao estande VR.  │
└────────────────────────────┘
```
- A chamada fica claramente visível no app e é refletida no monitor público
- O participante não precisa escanear QR Code para comprovar que realizou a experiência

**Ausência na chamada**
```
Chamado → não compareceu → Staff registra ausência
 → participante volta para o FINAL DA FILA daquela estação
```
- O participante não é removido definitivamente da experiência
- **Pendentes:** tempo de tolerância, número máximo de ausências, penalidades e bloqueios ainda não foram definidos

**Sair da fila**
- Remove o participante apenas daquela fila
- Ele continua dentro da Arena e o tempo de permanência segue normalmente
- Depois disso, pode entrar em outra fila

---

### ETAPA 7: SAÍDA DA ARENA

```
[Sair da Arena]
 → Confirmação: "Deseja sair da Arena?"  [Sair] [Cancelar]
 → Se estiver em uma fila de estação: removido automaticamente
 → Registro automático de saída
 → Participação finalizada
```

- A confirmação evita saída acidental
- **Regra:** se o participante estiver em uma fila e confirmar a saída, é removido automaticamente dessa fila (não precisa usar "Sair da fila" antes) e sua participação é encerrada
- Registrado automaticamente:
  - Horário de saída
  - Tempo total de permanência
  - Experiências concluídas
  - Demais informações operacionais disponíveis
- Nenhum desses dados é solicitado ao participante

---

### ETAPA 8: FINALIZAÇÃO E AVALIAÇÃO

**Tela: Participação Finalizada**
```
┌────────────────────────────────────┐
│  ✅ Participação finalizada        │
├────────────────────────────────────┤
│  BEAST Arena - Shopping XYZ        │
│  📅 15 de setembro                 │
│  ⏱️ Permanência: 2h 45min          │
│                                    │
│  Experiências concluídas:          │
│  ✅ PlayStation                    │
│  ✅ VR                             │
├────────────────────────────────────┤
│  Como foi sua experiência?         │
│  ⭐ ⭐ ⭐ ⭐ ⭐                     │
│                                    │
│  Quer contar mais sobre sua        │
│  experiência? (Opcional)           │
│  [Campo de texto]                  │
│                                    │
│  [Enviar avaliação]                │
│  [Pular avaliação]                 │
└────────────────────────────────────┘
```

- Avaliação opcional: nota geral de 1 a 5 estrelas + comentário opcional
- Sem questionários adicionais (atendimento, estação favorita, retorno, satisfação por experiência etc.), para minimizar atrito
- Após enviar ou pular → Home
- A participação passa a constar no histórico (Participações Recentes e Minhas Participações)

---

### ETAPA 9: MINHAS PARTICIPAÇÕES E DETALHES

**Aba: Eventos → Minhas Participações**
```
Minhas Participações

📍 BEAST Arena - Shopping XYZ
📅 15 de setembro de 2024
⏱️ Permanência: 2h 45min
⭐ Avaliação: 4/5
[Ver detalhes]

📍 BEAST Arena - Feira de Games
📅 10 de agosto de 2024
⏱️ Permanência: 1h 30min
⭐ Não avaliado
[Ver detalhes]
```
- A aba inferior continua se chamando "Eventos"; o título interno é "Minhas Participações"
- Representa o histórico completo do usuário

**Tela: Detalhes da Participação**

Fluxo: Eventos → Minhas Participações → Ver detalhes → Detalhes da Participação
```
BEAST Arena - Shopping XYZ
📅 15 de setembro de 2024

⏱️ Permanência: 2h 45min
   Entrada: 14:30
   Saída: 17:15

🎮 Experiências concluídas:
   ✅ PlayStation — Concluída às 14:35
   ✅ Realidade Virtual — Concluída às 15:10
   ✅ Simulador — Concluída às 16:20

⭐ Sua avaliação: 4/5
💬 Comentário: "Muito legal!"

[Voltar]
```
- Sem avaliação → "Não avaliado"
- Histórico de posições/filas **não** é exibido ao participante; esses dados podem existir internamente para análise

---

### ETAPA 10: PERFIL

```
┌────────────────────────────┐
│  👤 [Nome]                 │
│  [e-mail]                  │
├────────────────────────────┤
│  3 Participações           │
│  8h Tempo total            │
├────────────────────────────┤
│  Dados pessoais            │
│  Dados do questionário     │
│  Configurações             │
│  Sair (logout)             │
└────────────────────────────┘
```
- Permite visualizar e editar os dados pessoais e as informações do questionário
- Estatísticas: **Participações** e **Tempo total**

---

## 4. ÁREA RESTRITA DO STAFF

Interface operacional usada pela equipe da Arena.

**Funções:**
- Visualizar as filas das estações
- Visualizar participantes aguardando
- Realizar chamadas
- Identificar o participante chamado
- Registrar ausência (no-show)
- Confirmar conclusão da experiência
- Controlar a fila de acesso à Arena
- Ativar/desativar a fila de acesso

```
┌─────────────────────────────────────┐
│  STAFF — Estação VR                 │
├─────────────────────────────────────┤
│  Chamado agora: João S.             │
│  [✅ Concluir] [🚫 Ausente]         │
├─────────────────────────────────────┤
│  Aguardando:                        │
│  1. Maria A.                        │
│  2. Pedro M.                        │
│  [Chamar próximo]                   │
├─────────────────────────────────────┤
│  Fila de acesso à Arena: [SIM|NÃO]  │
└─────────────────────────────────────┘
```

**Quando o Staff confirma a conclusão:**
1. A experiência é registrada no histórico do participante
2. O atendimento daquela estação é concluído
3. A fila pode avançar
4. O participante deixa de estar vinculado àquela fila
5. Ele fica livre para entrar em outra fila

- O Staff não precisa procurar manualmente o participante: a própria fila já associa participante e estação
- A arquitetura prevê a possibilidade de alertar/lembrar o Staff para realizar o check de conclusão (mecanismo a definir)

---

## 5. MONITOR PÚBLICO DA ARENA

Interface pública exibida na Arena. **Não** faz parte das abas do aplicativo do participante.

**Objetivo:** mostrar as chamadas das filas em tempo real.

```
┌──────────────────────────────────────┐
│          BEAST ARENA — CHAMADAS      │
├──────────────────┬───────────────────┤
│  VR              │  PlayStation      │
│  Agora: João S.  │  Agora: Pedro M.  │
│  Próximo: Maria A│  Próximo: Ana C.  │
└──────────────────┴───────────────────┘
```
- Sincronizado com o aplicativo do participante e com a área do Staff
- Participantes representados de forma abreviada (primeiro nome + inicial), evitando exposição desnecessária de dados pessoais

---

## 6. SINCRONIZAÇÃO DOS TRÊS CONTEXTOS

```
App do participante
        ↕
   Área do Staff
        ↕
  Monitor público
```

As três interfaces são **visões diferentes do mesmo estado operacional das filas**, e não sistemas independentes.

**Exemplo:**
```
Staff chama João
 → estado da fila é atualizado
 → app de João mostra "É a sua vez!"
 → monitor público mostra João como chamado
```

A estratégia técnica de sincronização em tempo real ainda não foi definida.

---

## 7. ORIGEM DOS DADOS

| Origem | Dados |
|--------|-------|
| **Automáticos (sistema)** | Entrada, saída, tempo de permanência, experiências concluídas, horários de conclusão, interações operacionais com filas (quando disponíveis) |
| **Informados pelo participante** | Nome, e-mail, idade, gênero, escolaridade, jogos que costuma jogar, conhecimento do mercado de games, interesse profissional no mercado, avaliação, comentário opcional (a senha é dado de autenticação, não dado analítico de perfil) |
| **Confirmados pelo Staff** | Chamadas, ausência/no-show, conclusão de experiência, controle da fila de acesso |

**Princípio:** não pedir ao participante informações que o próprio sistema pode registrar.

---

## 8. ESTADOS DE ERRO

### Erro: Câmera indisponível
```
⚠️ Câmera não disponível

Não conseguimos acessar sua câmera.

[Tentar Novamente] [Digitar Código]
```

### Erro: QR Code inválido
```
❌ QR Code não reconhecido

O QR Code escaneado não foi reconhecido ou não é válido.

[Tentar Novamente]
```

### Erro: Código inválido
```
❌ Código inválido

Confira o código e tente novamente.

[Tentar Novamente]
```

### Aviso: Participação ativa
```
⚠️ Você já tem uma participação em andamento

Não é possível entrar em outro evento enquanto
sua participação atual não for encerrada.

[OK]
```

**Observação:** o comportamento sem conexão com a internet será definido junto com a arquitetura técnica. O código manual não é uma solução offline garantida.

---

## 9. NAVEGAÇÃO INFERIOR (ABAS)

```
┌─────────────────────────────────────┐
│ [🏠 Início] [📍 Eventos] [👤 Perfil] │
└─────────────────────────────────────┘
```

### Aba 1: Início
- Entrada no evento
- Até duas participações recentes
- Acesso a "Ver todas"

### Aba 2: Eventos
- Minhas Participações
- Histórico completo
- Detalhes das participações

### Aba 3: Perfil
- Dados pessoais
- Dados do questionário
- Estatísticas
- Configurações
- Logout

---

## 10. FLUXO COMPLETO RESUMIDO

```
START
 ├─ Novo usuário → Cadastro → Questionário de Perfil → Home
 └─ Usuário existente → Login → Home

HOME
 └─ [Entrar em Evento]
     ├─ QR Code OU Código Manual
     └─ Confirmar Entrada
         ├─ Fila de acesso DESATIVADA
         │   → Entrada efetiva → Arena em andamento
         └─ Fila de acesso ATIVADA
             → Fila de acesso → Liberação → Entrada efetiva
             → Arena em andamento

ARENA EM ANDAMENTO
 ├─ Escolher estação → Entrar na fila → Acompanhar posição
 │   → Ser chamado → Realizar experiência
 │   → Staff confirma conclusão → Experiência concluída
 │   → Pode entrar em outra fila
 ├─ Não compareceu à chamada → volta ao final da fila da estação
 ├─ [Sair da fila] → sai somente da fila, continua na Arena
 └─ [Sair da Arena]
     → Confirmar saída
     → Se estiver em fila, removido automaticamente
     → Registrar saída e calcular permanência
     → Resumo da participação
     → Avaliar OU Pular avaliação
     → Home
     → Histórico atualizado
```

---

## 11. PADRÕES DE DESIGN

Princípios que orientam a arquitetura:
- **Simplicidade**: cada tela com objetivo claro
- **Baixa fricção**: mínimo de ações e digitação
- **Clareza**: estados e próximas ações sempre compreensíveis
- **Feedback de estados**: fila, posição, chamada e conclusão sempre visíveis
- **Navegação mobile consistente**: abas inferiores
- **CTAs claros**: um CTA principal por contexto
- **Legibilidade**: em dispositivos pequenos e no monitor público
- **Coleta integrada**: dados coletados naturalmente durante a experiência

**Identidade visual:** as cores e estilos usados no protótipo HTML são provisórios. A identidade visual definitiva será desenvolvida no Figma.

---

## 12. QUESTÕES AINDA NÃO DEFINIDAS

- Tempo de tolerância após uma chamada
- Quantidade máxima de ausências (no-shows)
- Penalidades por ausência
- Comportamento completo em queda de internet
- Estratégia técnica de sincronização em tempo real
- Backend e banco de dados definitivos
- Formato dos alertas/lembretes ao Staff para o check de conclusão
- Papel técnico definitivo do Google Drive (mencionado pela empresa como preferência de armazenamento; não é, por ora, decisão de arquitetura operacional nem banco de dados em tempo real)
- Mecanismo exato de direcionamento para a plataforma da BEAST
- Identidade visual final

