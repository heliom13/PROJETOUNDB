# BEAST MARAGAMES - Análise de Decisões & Arquitetura UX

## 📋 Documento de Trabalho de Conclusão de Curso

**Projeto**: Aplicativo Mobile para Arena Itinerante - BEAST MARAGAMES  
**Fase**: Design Thinking & Arquitetura de UX  
**Objetivo**: Consolidar decisões de produto e definir fluxos de experiência do usuário  

---

## 1. ANÁLISE DA DECISÃO #1: ENTRADA NO EVENTO

### 1.1 Contexto

A entrada no evento é o ponto de partida da experiência. É nela que:
- O registro do participante é iniciado
- O evento é identificado
- O participante começa a ser rastreado

**Princípios orientadores:**
- Simplicidade: não deve exigir muito tempo do participante
- Confiabilidade: dados devem ser precisos (evitar duplicação)
- Robustez: funcionamento em qualquer contexto (conexão fraca, multidão)
- Acessibilidade: qualquer participante consegue entrar

### 1.2 Alternativas Consideradas

#### **ALTERNATIVA A: QR Code**

**Fluxo de Uso:**
```
1. Participante abre app (já autenticado)
2. Clica em "Entrar em Evento"
3. App abre câmera
4. Participante aponta para QR Code na Arena
5. Sistema identifica evento automaticamente
6. Mostra confirmação: "Entrar em [NOME DO EVENTO]?"
7. Participante confirma
8. Entrada registrada → Tela do evento
```

**Vantagens:**
- ✅ Velocidade: ~2 segundos (automático)
- ✅ Impossível duplicar (cada scan único)
- ✅ Experiência "mágica" (tecnologia visível)
- ✅ Sem necessidade de memorização
- ✅ Rastreamento preciso (QR Code registra horário)

**Desvantagens:**
- ❌ Dependência de câmera (pode não funcionar)
- ❌ Requer conexão internet no momento
- ❌ QR Code precisa estar bem visível/legível
- ❌ Pode falhar em locais com pouca luz
- ❌ Participante precisa encontrar o QR Code

**Confiabilidade de Dados:** ⭐⭐⭐⭐⭐ Muito alta (scan único)  
**Experiência UX:** ⭐⭐⭐⭐⭐ Excelente (rápido e automático)  
**Robustez:** ⭐⭐⭐ Média (depende de câmera)  

---

#### **ALTERNATIVA B: Código Manual**

**Fluxo de Uso:**
```
1. Participante abre app (já autenticado)
2. Clica em "Entrar em Evento"
3. Vê campo para digitar código
4. Monitor/placa na Arena exibe: "BEAST2024"
5. Participante digita o código
6. Sistema identifica evento
7. Mostra confirmação: "Entrar em [NOME DO EVENTO]?"
8. Participante confirma
9. Entrada registrada → Tela do evento
```

**Vantagens:**
- ✅ Funciona offline (sincroniza depois)
- ✅ Funciona em qualquer celular (não precisa câmera)
- ✅ Código pode ser visualizado de longe (placa grande)
- ✅ Fallback se câmera quebrar
- ✅ Participante pode entrar depois (se esquecer no começo)

**Desvantagens:**
- ❌ Lento (~30 segundos com digitação)
- ❌ Risco de erro na digitação
- ❌ Possibilidade de duplicação (digitar 2x)
- ❌ Participante pode esquecer código
- ❌ UX menos intuitiva (tediosa)
- ❌ Requer código memorável (fácil de digitar)

**Confiabilidade de Dados:** ⭐⭐ Baixa (risco de duplicação)  
**Experiência UX:** ⭐⭐ Fraca (lenta e tediosa)  
**Robustez:** ⭐⭐⭐⭐⭐ Muito alta (funciona sempre)  

---

#### **ALTERNATIVA C: QR Code + Código Manual (Híbrida)**

**Fluxo de Uso:**
```
FLUXO PRINCIPAL (QR Code):
1-8. [Mesmo que Alternativa A]

FLUXO FALLBACK (se QR Code falhar):
- Sistema detecta que câmera não funciona
- Oferece opção: "Não conseguiu? Digite o código"
- Participante digita código (como Alternativa B)
- Entrada registrada
```

**Vantagens:**
- ✅ Experiência principal é rápida (QR Code)
- ✅ Sempre há alternativa se câmera falhar
- ✅ Combina o melhor dos dois mundos
- ✅ Alta confiabilidade (validação inteligente)
- ✅ Robusta e resiliente
- ✅ Funciona offline + online

**Desvantagens:**
- ❌ Implementação mais complexa
- ❌ Duas formas de entrada pode confundir participante
- ❌ Código precisa ser simples e memorável
- ❌ Validação dupla (evitar duplicação entre QR e manual)

**Confiabilidade de Dados:** ⭐⭐⭐⭐⭐ Muito alta (validação inteligente)  
**Experiência UX:** ⭐⭐⭐⭐⭐ Excelente (rápido + fallback)  
**Robustez:** ⭐⭐⭐⭐⭐ Muito alta (sempre funciona)  

---

### 1.3 Matriz de Comparação

| Critério | QR Code | Código Manual | Híbrida |
|----------|---------|---------------|---------|
| **Velocidade** | ⭐⭐⭐⭐⭐ | ⭐ | ⭐⭐⭐⭐⭐ |
| **Confiabilidade** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Robustez** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Simplicidade** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **UX Participante** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Complexidade Dev** | ⭐⭐⭐ | ⭐ | ⭐⭐⭐⭐ |

---

### 1.4 Alinhamento com Princípios do Projeto

**Princípio: "Simplicidade"**
- ✅ Híbrida: Participante vê opção simples (QR) + fallback se falhar
- ❌ QR Code: Falha se câmera não funcionar
- ⚠️ Manual: Simples mas lenta

**Princípio: "Oferecer Valor ao Participante"**
- ⭐ Híbrida: Experiência rápida + sem frustração
- ⭐ QR Code: Experiência rápida mas pode falhar
- ⭐ Manual: Sempre funciona mas frustrante

**Princípio: "Dados Confiáveis"**
- ✅ Híbrida: Validação dupla impede duplicação
- ✅ QR Code: Cada scan é único (não duplica)
- ❌ Manual: Risco de duplicação

---

### 1.5 RECOMENDAÇÃO

**Escolha: ALTERNATIVA C - QR Code + Código Manual (Híbrida)**

**Justificativa:**
1. Atende ao princípio de simplicidade (fluxo principal rápido)
2. Oferece valor sem frustração (sempre há fallback)
3. Dados confiáveis (validação inteligente)
4. Robusta em qualquer contexto
5. Melhor equilíbrio entre UX e confiabilidade

**Implementação:**
- Fluxo padrão: QR Code (rápido)
- Fluxo alternativo: Código Manual (fallback)
- Validação: Impedir duplicação entre os dois fluxos

---

## 2. ANÁLISE DA DECISÃO #2: REGISTRO DE EXPERIÊNCIAS

### 2.1 Contexto

Uma vez dentro do evento, como o sistema registra quais experiências o participante realizou?

O modelo deve:
- Associar participante + experiência/estação
- Gerar dados confiáveis para BEAST
- Minimizar atrito para o participante
- Permitir acompanhamento em tempo real (filas)

### 2.2 Alternativas Consideradas

#### **ALTERNATIVA A: Apenas Entrada e Saída**

**Modelo:**
```
O app registra APENAS:
- Horário de entrada: 14:30
- Horário de saída: 16:45
- Tempo total: 2h 15min
- Evento: Arena Itinerante - Shopping XYZ

NÃO registra quais experiências específicas foram feitas.
```

**Fluxo da Tela do Evento:**
```
┌────────────────────────┐
│  Arena em Andamento    │
│                        │
│  Horário de entrada:   │
│  14:30                 │
│                        │
│  Tempo aqui:           │
│  2h 15min              │
│                        │
│  [Sair da Arena]       │
└────────────────────────┘
```

**Vantagens:**
- ✅ Super simples (zero ação do participante)
- ✅ Dados muito confiáveis (baseados em tempo)
- ✅ Sem necessidade de QR Code nas estações
- ✅ Sem risco de duplicação
- ✅ Participante não precisa fazer nada
- ✅ Implementação mínima

**Desvantagens:**
- ❌ BEAST não sabe quais experiências foram feitas
- ❌ Sem dados de preferência
- ❌ Sem informações sobre engajamento
- ❌ App oferece pouco valor ao participante (apenas timer)
- ❌ Não responde "quem usou VR?" ou "PS teve mais uso?"

**Valor para BEAST:** ⭐⭐ Básico (só tempo de permanência)  
**Valor para Participante:** ⭐⭐ Mínimo (timer apenas)  
**Complexidade:** ⭐ Mínima  

---

#### **ALTERNATIVA B: Código Manual por Estação**

**Modelo:**
```
Cada estação/experiência tem um código:

🎮 PlayStation: PLAY2024
🥽 Realidade Virtual: VROC2024
🚗 Simulador de Corrida: RACE2024

Quando participante usa uma estação:
1. Encontra o código (placa/adesivo)
2. Abre app → "Registrar Experiência"
3. Digita código: PLAY2024
4. App registra: "PlayStation às 14:35"
5. Participante volta a aproveitar

Resultado no histórico:
- PlayStation ✅ 14:35
- Realidade Virtual ✅ 15:10
- Simulador ✅ 16:20
```

**Fluxo da Tela do Evento:**
```
┌────────────────────────┐
│  Arena em Andamento    │
│                        │
│  Experiências:         │
│  ✅ PlayStation 14:35  │
│  ✅ VR Reality 15:10   │
│  ⭕ Simulador          │
│  ⭕ Outras...          │
│                        │
│ [+ Registrar Experiên.]│
│ [Sair da Arena]        │
└────────────────────────┘
```

**Vantagens:**
- ✅ BEAST sabe exatamente quais experiências
- ✅ Dados de preferência (qual experiência mais usada?)
- ✅ Histórico detalhado para participante
- ✅ Informações para melhorar Arena
- ✅ Maior engajamento (participante vê seu histórico)
- ✅ Fácil identificar experiências populares

**Desvantagens:**
- ❌ Participante precisa digitar código múltiplas vezes (3-5x)
- ❌ Atrito na experiência (tirar atenção do evento)
- ❌ Risco de esquecer de registrar
- ❌ Possibilidade de duplicação (digitar 2x por acidente)
- ❌ Risco de erro na digitação
- ❌ Código precisa ser simples e único
- ❌ Impacto negativo na UX (muito atrito)

**Valor para BEAST:** ⭐⭐⭐⭐⭐ Excelente (dados detalhados)  
**Valor para Participante:** ⭐⭐⭐⭐ Bom (histórico detalhado)  
**Complexidade:** ⭐⭐⭐ Média + Risco alto  

---

#### **ALTERNATIVA C: Fila Virtual por Estação + Confirmação pelo Staff**

**Modelo:**
```
Cada estação tem sua própria FILA VIRTUAL:

🎮 PlayStation: fila virtual
🥽 VR Reality: fila virtual
🚗 Simulador: fila virtual

Fluxo:
1. Participante escolhe estação na tela do app
2. Entra na fila (apenas uma fila por vez)
3. Acompanha posição em tempo real
4. É chamado pelo sistema (notificação)
5. Dirigir-se à estação
6. Staff confirma conclusão no tablet/celular
7. Experiência registrada automaticamente
8. Participante fica livre para entrar em outra fila

Resultado: Fila gerida pelo app + Validação pelo Staff
```

**Vantagens:**
- ✅ BEAST sabe exatamente quais experiências (Staff confirma)
- ✅ Participante acompanha posição em tempo real
- ✅ Sem necessidade de QR Code em cada estação
- ✅ Fila gerida digitalmente (melhor operacional)
- ✅ Participante + Estação já associados na fila
- ✅ Staff confirma ocorrência real (validação)
- ✅ Dados muito confiáveis
- ✅ Experiência melhorada (participante sabe seu lugar)
- ✅ Impacto operacional positivo (Staff controla fluxo)

**Desvantagens:**
- ❌ Requer Staff com dispositivo (tablet/celular)
- ❌ Implementação de sincronização em tempo real
- ❌ Coordenação operacional (Staff deve confirmar)

**Valor para BEAST:** ⭐⭐⭐⭐⭐ Excelente (dados + operacional)  
**Valor para Participante:** ⭐⭐⭐⭐⭐ Excelente (acompanhamento + transparência)  
**Complexidade:** ⭐⭐⭐ Média (sincronização)  

  

---

### 2.3 Matriz de Comparação

| Critério | Entrada/Saída | Código Manual | Fila Virtual + Staff |
|----------|---------------|---------------|---------|
| **Dados Detalhados** | ❌ | ✅ | ✅✅ |
| **Atrito (UX)** | ⭐⭐⭐⭐⭐ | ⭐ | ⭐⭐⭐⭐⭐ |
| **Confiabilidade** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Complexidade Dev** | ⭐ | ⭐⭐ | ⭐⭐⭐ |
| **Valor Participante** | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Gerenciamento Operacional** | ❌ | ❌ | ✅⭐⭐⭐⭐⭐ |
| **Scalability** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

---

### 2.4 Alinhamento com Princípios

**Princípio: "Coleta Transparente (Não Atrapalhar)"**
- ✅ Entrada/Saída: Participante não faz nada
- ❌ Código Manual: Alto atrito (múltiplas digitações)
- ✅ Fila Virtual: Participante acompanha (valor) + Staff confirma

**Princípio: "Oferecer Valor ao Participante"**
- ❌ Entrada/Saída: Mínimo valor (timer apenas)
- ✅ Código Manual: Bom valor (histórico)
- ✅✅ Fila Virtual: Máximo valor (posição em tempo real + transparência)

**Princípio: "Dados Confiáveis"**
- ✅ Entrada/Saída: Muito confiável (automaticamente)
- ⚠️ Código Manual: Risco de duplicação
- ✅✅ Fila Virtual: Muito confiável (fila digital + Staff valida)

---

### 2.5 RECOMENDAÇÃO

**Escolha: ALTERNATIVA C - Fila Virtual por Estação + Confirmação pelo Staff**

**Justificativa:**
1. Máximo valor ao participante (acompanha posição em tempo real)
2. Zero atrito durante participação (Staff confirma, não participante)
3. Dados muito confiáveis (fila digital + validação do Staff)
4. Elimina necessidade de QR Code em cada estação (reduz custo)
5. Melhora experiência operacional (Staff gerencia melhor)
6. Oferece dados estratégicos + operacionais para BEAST
7. Escalável (funciona com qualquer número de participantes)

**Implementação:**
- Fila virtual para cada estação/experiência
- Participante pode estar em apenas 1 fila por vez
- Staff confirma conclusão em dispositivo (tablet/celular)
- Sistema sincroniza em tempo real (App + Staff + Monitor)

---

## 3. ANÁLISE DA DECISÃO #3: BENEFÍCIO AO PARTICIPANTE

### 3.1 Contexto

Além de registrar dados, o app deve oferecer valor ao participante ao longo do tempo.

O valor deve ser:
- Transparente (participante vê dados reais)
- Significativo (não artificial ou inflacionado)
- Não obtrusivo (não gamificação pesada)
- Alinhado com objetivos educacionais da BEAST

Opções consideradas:
- Histórico simples (o que fez)
- Histórico + Estatísticas (dados consolidados)
- Progresso/Níveis
- Pontuação/Ranking
- Recompensas

### 3.2 Alternativas Consideradas

#### **ALTERNATIVA A: Histórico Simples**

**O que mostra:**
```
Minha Participação - Arena 2024

📍 BEAST Arena - Shopping XYZ
📅 15 de Setembro de 2024
⏱️ Permanência: 2h 45min

Experiências realizadas:
✅ PlayStation
✅ Realidade Virtual
✅ Simulador de Corrida

Avaliação: ⭐⭐⭐⭐ (4/5)
Comentário: "Muito legal!"
```

**Vantagens:**
- ✅ Simples de implementar
- ✅ Oferece algum valor (ver o que fez)
- ✅ Não "incha" a UX com gamificação
- ✅ Alinha com princípio de simplicidade
- ✅ Permite participante acompanhar
- ✅ Data histórica completa

**Desvantagens:**
- ❌ Valor limitado (apenas registro)
- ❌ Sem incentivo para retornar
- ❌ Menos engajamento

**Engajamento:** ⭐⭐ Baixo  
**Valor Participante:** ⭐⭐⭐ Médio  

---

#### **ALTERNATIVA B: Histórico + Estatísticas Pessoais**

**O que mostra:**
```
Meu Perfil & Estatísticas

3 Participações
8h Tempo total
12 Experiências realizadas

Últimas participações:
- BEAST Arena - Shopping XYZ (15 set)
- BEAST Arena - Feira de Games (10 ago)

Preferências observadas:
- Experiências mais usadas: VR (3x), PS (2x)
- Horário preferido: Manhã
- Duração média: 2h 45min

Avaliações:
⭐⭐⭐⭐⭐ (4.5 média)
```

**Vantagens:**
- ✅ Valor real ao participante (dados pessoais)
- ✅ Simples e transparente
- ✅ Sem elementos artificiais
- ✅ Fácil de implementar
- ✅ Educacional (participante vê seus padrões)
- ✅ Alinha com propósito de coleta de dados

**Desvantagens:**
- ⚠️ Engajamento menor que gamificação

**Engajamento:** ⭐⭐⭐ Moderado  
**Valor Participante:** ⭐⭐⭐⭐ Excelente (dados reais)  

---

#### **ALTERNATIVA C: Progresso/Nível com Gamificação**

**O que mostra:**
```
Meu Progresso

🎮 Explorador de Experiências
Nível 3 de 10

Progresso:
████████░░ 80%

Próximo nível em: 2 experiências

Desbloqueáveis:
🔓 "Veterano": Completar 5 eventos
🔒 "Fã de VR": Usar VR 5 vezes
```

**Vantagens:**
- ✅ Incentiva retorno
- ✅ Oferece progresso visível
- ✅ Engajamento moderado

**Desvantagens:**
- ❌ Mais complexo de implementar
- ❌ Pode parecer artificial/inflacionado
- ❌ Requer lógica de progressão
- ❌ Nem sempre alinha com objetivo educacional

**Engajamento:** ⭐⭐⭐⭐ Alto  
**Valor Participante:** ⭐⭐⭐ Médio  

---

#### **ALTERNATIVA D: Ranking/Pontuação**

**O que mostra:**
```
Ranking Global

Você: Posição #127

Seus Pontos: 450

Ranking semanal:
1. João Silva - 1.200 pts
2. Maria - 980 pts
3. Você - 450 pts
```

**Vantagens:**
- ✅ Alto engajamento competitivo
- ✅ Incentiva uso múltiplo

**Desvantagens:**
- ❌ Pode criar competição não saudável
- ❌ Pode desmotivar quem não está no top
- ❌ Foco em pontos vs. experiência real
- ❌ Muito artificial

**Engajamento:** ⭐⭐⭐⭐⭐ Muito alto  
**Valor Real:** ⭐ Mínimo (artificial)  

---

### 3.3 Matriz de Comparação

| Critério | Histórico | Histórico + Estatísticas | Progresso/Nível | Ranking |
|----------|-----------|---------|---------|---------|
| **Engajamento** | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Valor Real** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐ |
| **Simplicidade** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **Complexidade Dev** | ⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Alinhamento Princípios** | ✅ | ✅✅ | ⚠️ | ❌ |

---

### 3.4 Alinhamento com Princípios

**Princípio: "Simplicidade"**
- ✅✅ Histórico + Estatísticas: Muito simples
- ✅ Histórico simples: Básico
- ⚠️ Progresso/Nível: Moderado
- ❌ Ranking: Complexo

**Princípio: "Oferecer Valor Real (Não Artificial)"**
- ⭐ Histórico: Valor básico
- ⭐⭐⭐⭐⭐ Histórico + Estatísticas: Máximo valor (dados reais)
- ⭐⭐⭐ Progresso/Nível: Valor artificial/inflacionado
- ⭐ Ranking: Valor artificial

**Princípio: "Coleta Educacional"**
- ✅ Histórico + Estatísticas: Alinha com objetivo (entender comportamento do participante)
- ⚠️ Progresso/Nível: Desvia do foco (gamificação)
- ❌ Ranking: Desvia do foco (competição)

---

### 3.5 RECOMENDAÇÃO

**Escolha: ALTERNATIVA B - Histórico + Estatísticas Pessoais**

**Justificativa:**
1. Oferece valor real ao participante (dados pessoais, não artificial)
2. Alinha com princípios (simplicidade + transparência)
3. Educacional (participante entende seus padrões)
4. Implementação simples e viável
5. Suporta objetivos principais da BEAST (coleta de dados com propósito)
6. Não cria pressão artificial (sem gamificação pesada)
7. Escalável

**O que mostra:**
- Número de participações
- Tempo total em Arenas
- Experiências mais usadas
- Preferências observadas
- Avaliações antigas
- Histórico detalhado

**Implementação:**
- MVP: Histórico básico + Estatísticas simples
- V2: Melhorar visualização de estatísticas (gráficos, tendências)
- Futuro: Insights (ex: "Você gasta mais tempo em VR que outros participantes")

---

## 4. RESUMO DAS DECISÕES PRINCIPAIS

| Decisão | Recomendação | Justificativa |
|---------|--------------|---------------|
| **Entrada no Evento** | QR Code + Código Manual | Rápido + Robusto + Confiável |
| **Registro Experiências** | Fila Virtual + Staff Confirma | Transparência + Valor + Operacional |
| **Benefício Participante** | Histórico + Estatísticas | Simples + Valor Real + Educacional |

---

## 5. DECISÕES ESTRUTURANTES COMPLEMENTARES

### D1: Uma Fila por Vez
**Decisão:** Participante pode estar em apenas UMA fila de estação por vez.
**Justificativa:** Evita conflitos operacionais (timer, posição, notificações).

### D2: No-Show Retorna ao Final
**Decisão:** Se chamado e não comparecer, participante vai para o final da fila (não é removido).
**Justificativa:** Oferece segunda chance; escalável.

### D3: Fila de Acesso Dinâmica
**Decisão:** Staff pode ativar/desativar fila de acesso à Arena em tempo real.
**Justificativa:** Gerencia lotação; transparente.

### D4: Espera não Conta como Permanência
**Decisão:** Timer de permanência começa apenas na ENTRADA EFETIVA.
**Justificativa:** Dados precisos (permanência = tempo aproveitado).

### D5: Uma Participação Ativa por Vez
**Decisão:** Cada usuário pode ter apenas UMA participação ativa por evento.
**Justificativa:** Evita conflitos; clareza de estado.

---

## 6. PRÓXIMAS ETAPAS

✅ DECISÕES CONSOLIDADAS  
⏭️ Atualizar Arquitetura de Telas  
⏭️ Protótipo Estrutural HTML  
⏭️ Desenvolvimento Figma (Identidade Visual)  

