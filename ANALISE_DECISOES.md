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

Uma vez dentro do evento, como o app sabe quais experiências o participante fez?

Isso determina:
- Dados que BEAST coleta
- Valor que app oferece ao participante
- Complexidade de uso

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

#### **ALTERNATIVA C: QR Code por Estação**

**Modelo:**
```
Cada estação tem um QR Code próprio:

🎮 PlayStation: QR Code A
🥽 VR Reality: QR Code B
🚗 Simulador: QR Code C

Quando participante termina uma experiência:
1. Aponta câmera para QR Code da estação
2. App registra automaticamente
3. Mostra: "✅ PlayStation registrado às 14:35"
4. Participante volta a aproveitar

Resultado: Mesmo que Alternativa B, mas automático
```

**Vantagens:**
- ✅ BEAST sabe quais experiências
- ✅ Automático (2 segundos)
- ✅ Sem possibilidade de erro
- ✅ Sem possibilidade de duplicação
- ✅ Histórico detalhado
- ✅ Pouco atrito (rápido)

**Desvantagens:**
- ❌ Requer QR Code em cada estação
- ❌ Depende de câmera (pode falhar)
- ❌ Requer conexão internet por múltiplas vezes
- ❌ Implementação complexa (múltiplos QR Codes)
- ❌ Pode confundir (escanear QR Code de saída ao invés de estação)
- ❌ Custo maior (mais QR Codes)

**Valor para BEAST:** ⭐⭐⭐⭐⭐ Excelente (dados detalhados + confiáveis)  
**Valor para Participante:** ⭐⭐⭐⭐ Bom (histórico automático)  
**Complexidade:** ⭐⭐⭐⭐ Alta  

---

#### **ALTERNATIVA D: Monitor Registra**

**Modelo:**
```
Monitor (funcionário da Arena) registra:

Monitor vê participante usando PlayStation:
1. Abre app no seu tablet
2. Busca participante por nome/código
3. Clica: "PlayStation ✅"
4. Sistema registra automaticamente

Participante não faz nada.
```

**Vantagens:**
- ✅ Participante não faz nada (zero atrito)
- ✅ Dados validados (monitor confirma)
- ✅ Impossível duplicação
- ✅ Menos risco de erro

**Desvantagens:**
- ❌ Requer monitor em CADA estação
- ❌ Custo operacional alto
- ❌ Monitor pode esquecer de registrar
- ❌ Monitor pode registrar errado
- ❌ Scalability ruim (não funciona com muitos participantes)
- ❌ Participante não vê seu histórico em tempo real
- ❌ Depende de terceiros (monitor pode estar ausente)

**Valor para BEAST:** ⭐⭐⭐⭐ Bom (dados confiáveis)  
**Valor para Participante:** ⭐ Mínimo (não sabe seu histórico)  
**Complexidade:** ⭐⭐⭐⭐⭐ Muito alta (operacional)  

---

### 2.3 Matriz de Comparação

| Critério | Entrada/Saída | Código Manual | QR Code | Monitor |
|----------|---------------|---------------|---------|---------|
| **Dados Detalhados** | ❌ | ✅ | ✅ | ✅ |
| **Atrito (UX)** | ⭐⭐⭐⭐⭐ | ⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Confiabilidade** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Complexidade Dev** | ⭐ | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Valor Participante** | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐ |
| **Scalability** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ❌ |

---

### 2.4 Alinhamento com Princípios

**Princípio: "Simplicidade"**
- ✅ Entrada/Saída: Simples demais (sem valor)
- ⚠️ Código Manual: Simples mas repetitivo
- ✅ QR Code: Simples e automático
- ❌ Monitor: Complexo operacionalmente

**Princípio: "Oferecer Valor ao Participante"**
- ❌ Entrada/Saída: Mínimo valor
- ✅ Código Manual: Bom valor (histórico)
- ✅ QR Code: Bom valor (histórico automático)
- ❌ Monitor: Sem valor para participante

**Princípio: "Não Atrapalhar Experiência"**
- ✅ Entrada/Saída: Zero atrito
- ❌ Código Manual: Alto atrito (múltiplas digitações)
- ✅ QR Code: Baixo atrito (rápido)
- ✅ Monitor: Zero atrito

---

### 2.5 RECOMENDAÇÃO

**Escolha: ALTERNATIVA C - QR Code por Estação**

**Justificativa:**
1. Oferece valor ao participante (histórico detalhado)
2. Baixo atrito (automático e rápido)
3. Dados confiáveis (impossível duplicar)
4. Alinha com fluxo de entrada (QR Code já é familiar)
5. Oferece dados estratégicos para BEAST

**Alternativa Secundária (se QR Codes custarem muito):**
Começar com Alternativa A (Entrada/Saída) e evoluir para QR Code depois.

---

## 3. ANÁLISE DA DECISÃO #3: BENEFÍCIO AO PARTICIPANTE

### 3.1 Contexto

Além de registrar dados, o app deve oferecer valor ao participante. Que valor é esse?

Opções consideradas:
- Histórico simples (o que fez)
- Progresso/Conquistas
- Pontuação/Gamificação
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

#### **ALTERNATIVA B: Progresso/Nível**

**O que mostra:**
```
Meu Progresso

🎮 Explorador de Experiências
Nível 3 de 10

Progresso:
████████░░ 80%

Próximo nível em: 2 experiências

Estatísticas:
- Experiências realizadas: 12
- Tempo total em Arenas: 8h
- Eventos visitados: 3

Próximas metas:
🔓 "Desbloqueável": Fazer 5 experiências VR
```

**Vantagens:**
- ✅ Incentiva retorno
- ✅ Oferece progresso visível
- ✅ Gamificação leve
- ✅ Aumenta engajamento

**Desvantagens:**
- ❌ Mais complexo de implementar
- ❌ Pode parecer artificial
- ❌ Requer lógica de progressão
- ❌ Pode confundir (muitas abas/seções)

**Engajamento:** ⭐⭐⭐⭐ Alto  
**Valor Participante:** ⭐⭐⭐⭐ Bom  

---

#### **ALTERNATIVA C: Pontuação/Ranking**

**O que mostra:**
```
Ranking de Experiências

Você: Posição #127 Global

Seus Pontos: 450

Ranking semanal:
1. João Silva - 1.200 pts
2. Maria Santos - 980 pts
3. Você - 450 pts
...

Como ganhar pontos:
- Usar experiência Nova: +50 pts
- Usar 5 experiências diferentes: +100 pts
```

**Vantagens:**
- ✅ Alto engajamento competitivo
- ✅ Incentiva uso múltiplo
- ✅ Viral (pessoas querem ser top)

**Desvantagens:**
- ❌ Pode criar competição não saudável
- ❌ Muito complexo
- ❌ Pode prejudicar experiência real (foco em pontos)
- ❌ Requer servidor de ranking
- ❌ Pode desmotivar quem não está no top

**Engajamento:** ⭐⭐⭐⭐⭐ Muito alto  
**Valor Participante:** ⭐⭐⭐ Médio (artificial)  

---

#### **ALTERNATIVA D: Recompensas**

**O que mostra:**
```
Minhas Recompensas

Pontos disponíveis: 450

Resgate:
🎁 10% desconto - próxima Arena (100 pts)
🎁 Adesivo exclusivo (50 pts)
🎁 Voucher R$50 (500 pts)

Seus cupons:
✅ Desconto 10% - BEAST Arena (válido até Dez/24)
```

**Vantagens:**
- ✅ Máximo engajamento
- ✅ Valor real ao participante
- ✅ Incentiva retorno

**Desvantagens:**
- ❌ Muito complexo (economia, cupons, validade)
- ❌ Requer parceria com eventos
- ❌ Custo operacional
- ❌ Pode não funcionar bem em primeiro evento
- ❌ Fora do escopo educacional

**Engajamento:** ⭐⭐⭐⭐⭐ Máximo  
**Valor Participante:** ⭐⭐⭐⭐⭐ Máximo  
**Complexidade:** ⭐⭐⭐⭐⭐ Muito alta  

---

### 3.3 Matriz de Comparação

| Critério | Histórico | Progresso | Ranking | Recompensas |
|----------|-----------|-----------|---------|-------------|
| **Engajamento** | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Valor Real** | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Simplicidade** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐ |
| **Complexidade Dev** | ⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Alinhamento Princípios** | ✅ | ✅ | ⚠️ | ❌ |

---

### 3.4 Alinhamento com Princípios

**Princípio: "Simplicidade"**
- ✅ Histórico: Simples
- ✅ Progresso: Simples (visual claro)
- ⚠️ Ranking: Não é simples
- ❌ Recompensas: Complexo

**Princípio: "Oferecer Valor"**
- ⭐ Histórico: Valor básico
- ⭐⭐⭐⭐ Progresso: Bom valor (engajamento)
- ⭐⭐ Ranking: Valor questionável
- ⭐⭐⭐⭐⭐ Recompensas: Máximo valor

---

### 3.5 RECOMENDAÇÃO

**Escolha: ALTERNATIVA A + B - Histórico + Progresso Leve**

**Justificativa:**
1. Oferece valor sem complexidade excessiva
2. Alinha com princípios (simplicidade)
3. Engajamento moderado (sem ser artificial)
4. Implementação viável para MVP
5. Histórico oferece rastreabilidade
6. Progresso oferece motivação

**Implementação Faseada:**
- **MVP**: Histórico simples + Avaliação
- **V2**: Adicionar nível de progressão leve
- **V3** (Futuro): Considerar recompensas se houver parceria

---

## 4. RESUMO DAS DECISÕES

| Decisão | Recomendação | Justificativa |
|---------|--------------|---------------|
| **Entrada no Evento** | QR Code + Código Manual | Rápido + Robusto + Confiável |
| **Registro Experiências** | QR Code por Estação | Automático + Dados Detalhados |
| **Benefício Participante** | Histórico + Progresso Leve | Simples + Valor Real + Engajamento |

---

## 5. PRÓXIMAS ETAPAS

✅ DECISÕES CONSOLIDADAS  
⏭️ Definir Arquitetura de Telas  
⏭️ Criar Fluxos Detalhados  
⏭️ Desenvolver Protótipo HTML  
⏭️ Mapear Estados de Erro  

