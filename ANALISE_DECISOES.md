# BEAST MARAGAMES - Análise de Decisões & Arquitetura UX

## 📋 Documento de Trabalho de Conclusão de Curso

**Projeto**: Aplicativo Mobile para Arena Itinerante - BEAST MARAGAMES  
**Fase**: Definição estrutural e fluxos (em revisão/consolidação)  
**Objetivo**: Registrar as decisões de produto, as alternativas consideradas e os trade-offs de cada escolha  

> Esta análise foi atualizada após novos levantamentos de requisitos com a empresa. O projeto deixou de se organizar em torno de "3 decisões estratégicas principais": as decisões sobre filas, chamadas e controle de acesso passaram a ser centrais. Pontos ainda não definidos estão marcados como **pendentes**.

---

## 1. DECISÃO: ENTRADA NO EVENTO

### 1.1 Contexto

A entrada no evento é o ponto de partida da experiência. É nela que:
- A participação é iniciada
- O evento é identificado
- O participante visualiza as informações do evento antes de confirmar

**Fluxo esperado:**
```
Home → Entrar em Evento → QR Code ou Código Manual
     → identificação do evento → tela de confirmação → confirmar entrada
```

O participante deve visualizar as informações do evento antes de efetivamente confirmar sua participação.

**Princípios orientadores:**
- Simplicidade: não deve exigir muito tempo do participante
- Confiabilidade: dados devem ser precisos (evitar entradas duplicadas)
- Acessibilidade: qualquer participante deve conseguir entrar, mesmo sem câmera funcional

**Sobre duplicidade:** a proteção contra entradas duplicadas vem das **regras do sistema** (confirmação explícita e uma participação ativa por usuário — ver Decisão 8), e não do simples fato de usar QR Code.

**Observação:** QR Code e código manual são duas formas de **identificar o evento**. Nenhuma das duas, por si só, garante funcionamento sem internet: a disponibilidade offline depende da arquitetura de dados/backend, que ainda não foi definida.

### 1.2 Alternativas Consideradas

#### **ALTERNATIVA A: QR Code**

**Fluxo de Uso:**
```
1. Participante abre app (já autenticado)
2. Toca em "Entrar em Evento"
3. App abre câmera
4. Participante aponta para QR Code na Arena
5. Sistema identifica o evento
6. Mostra confirmação com as informações do evento
7. Participante confirma
8. Entrada registrada
```

**Vantagens:**
- ✅ Velocidade: identificação praticamente imediata
- ✅ Elimina erros de digitação
- ✅ Sem necessidade de memorização
- ✅ Padrão já familiar em eventos

**Desvantagens:**
- ❌ Dependência de câmera
- ❌ QR Code precisa estar visível e legível
- ❌ Pode falhar em locais com pouca luz ou com QR danificado
- ❌ Participante precisa encontrar o QR Code

---

#### **ALTERNATIVA B: Código Manual**

**Fluxo de Uso:**
```
1. Participante abre app (já autenticado)
2. Toca em "Entrar em Evento"
3. Vê campo para digitar código
4. Placa/monitor na Arena exibe o código do evento
5. Participante digita o código
6. Sistema identifica o evento
7. Mostra confirmação com as informações do evento
8. Participante confirma
9. Entrada registrada
```

**Vantagens:**
- ✅ Não depende de câmera
- ✅ Funciona em qualquer celular
- ✅ Código pode ser exibido em placa grande, visível de longe

**Desvantagens:**
- ❌ Mais lento (exige digitação)
- ❌ Risco de erro na digitação
- ❌ Código precisa ser simples de digitar
- ❌ Experiência menos fluida

---

#### **ALTERNATIVA C: QR Code + Código Manual (Híbrida)**

**Fluxo de Uso:**
```
FLUXO PRINCIPAL (QR Code):
[Mesmo que Alternativa A]

FLUXO ALTERNATIVO (câmera indisponível ou QR ilegível):
- App oferece: "Não conseguiu? Digite o código"
- Participante digita o código (como Alternativa B)
- Segue para a mesma tela de confirmação
```

**Vantagens:**
- ✅ Experiência principal rápida (QR Code)
- ✅ Alternativa disponível quando a câmera ou o QR falham
- ✅ Ambos os caminhos levam à mesma confirmação

**Desvantagens:**
- ❌ Implementação um pouco mais extensa (dois caminhos de identificação)
- ❌ Duas formas de entrada precisam ser apresentadas com clareza
- ❌ Controle de entrada duplicada precisa valer para os dois caminhos

---

### 1.3 Matriz de Comparação

| Critério | QR Code | Código Manual | Híbrida |
|----------|---------|---------------|---------|
| **Velocidade** | Alta | Baixa | Alta (caminho principal) |
| **Risco de erro de identificação** | Baixo | Médio (digitação) | Baixo no principal, médio no alternativo |
| **Depende de câmera** | Sim | Não | Não (há alternativa) |
| **Funcionamento offline** | Depende do backend | Depende do backend | Depende do backend |
| **Complexidade de desenvolvimento** | Média | Baixa | Média |

---

### 1.4 Decisão Adotada

**✅ Decisão adotada: entrada híbrida — QR Code principal + código manual alternativo.**

**Justificativa:**
1. Mantém o caminho mais rápido como padrão (QR Code)
2. Evita que o participante fique impedido de entrar quando a câmera ou o QR falham
3. Os dois caminhos convergem para a mesma tela de confirmação, na qual o participante vê o evento antes de confirmar

**Pendente:** comportamento sem conexão com a internet, a ser definido junto com a arquitetura de dados/backend.

---

## 2. DECISÃO: REGISTRO DAS EXPERIÊNCIAS

### 2.1 Contexto

**Pergunta central:** como registrar as experiências realizadas pelo participante com baixo atrito e dados confiáveis?

Novo requisito levantado junto à empresa: **cada estande/estação possui sua própria fila, e o staff gerencia essas filas.** Isso muda a análise, pois o registro das experiências pode aproveitar a operação de fila que já precisa existir.

A decisão anterior (QR Code em cada estação) foi abandonada. Não haverá QR Code por estação para o participante registrar que realizou uma experiência.

### 2.2 Alternativas Consideradas

#### **ALTERNATIVA A: Somente Entrada e Saída**

O sistema registra entrada, saída e permanência, mas não identifica quais experiências foram realizadas.

**Vantagens:**
- ✅ Nenhuma ação adicional do participante
- ✅ Implementação mínima

**Desvantagens:**
- ❌ A empresa não sabe quais experiências foram realizadas
- ❌ Sem dados sobre preferência e interação com as estações
- ❌ Histórico do participante fica pobre (apenas tempo)

---

#### **ALTERNATIVA B: Autorregistro por Código da Estação**

O participante informa manualmente um código após realizar uma experiência.

**Vantagens:**
- ✅ Identifica as experiências realizadas
- ✅ Não depende de câmera

**Desvantagens:**
- ❌ Exige ação repetitiva do participante após cada experiência
- ❌ Risco de esquecimento ou erro de digitação
- ❌ Dados dependem da disciplina do participante

---

#### **ALTERNATIVA C: Autorregistro por QR Code da Estação**

Cada estação possui QR próprio e o participante o escaneia para registrar a experiência.

**Vantagens:**
- ✅ Reduz a digitação em relação à Alternativa B
- ✅ Identifica as experiências realizadas

**Desvantagens:**
- ❌ Continua exigindo ação deliberada do participante após cada experiência
- ❌ Necessidade de manter QR Codes em todas as estações
- ❌ O escaneamento indica presença na estação, não confirma que a experiência foi realizada

---

#### **ALTERNATIVA D: Registro Manual Isolado pelo Staff**

O funcionário identifica/procura o participante e registra manualmente qual experiência ele realizou.

**Vantagens:**
- ✅ Reduz a ação do participante
- ✅ Experiência confirmada por quem acompanhou a estação

**Desvantagens:**
- ❌ Aumenta o trabalho operacional do staff
- ❌ Staff precisa localizar o participante no sistema a cada atendimento
- ❌ Risco de registro esquecido ou atribuído à pessoa errada

---

#### **ALTERNATIVA E: Fila Virtual por Estação + Confirmação pelo Staff**

**Funcionamento:**
```
Participante escolhe uma experiência
   → entra na fila da estação
   → sistema associa participante à estação
   → participante acompanha sua posição
   → participante é chamado
   → realiza a experiência
   → staff confirma a conclusão
   → sistema registra automaticamente a experiência na participação
```

**Diferença em relação à Alternativa D:** o funcionário não precisa procurar manualmente o participante para descobrir quem realizou a experiência. O sistema já conhece o participante atendido, porque ele veio da própria fila daquela estação.

**O check do staff possui duas funções:**
- **Operacional:** concluir aquele atendimento e permitir o avanço da fila
- **Coleta de dados:** confirmar que aquela experiência foi efetivamente realizada

Após a conclusão pelo staff, o participante fica livre para entrar na fila de outra estação.

**Vantagens:**
- ✅ Integra gestão das filas e registro das experiências em uma única ação
- ✅ Nenhuma ação extra do participante para registrar a experiência
- ✅ Experiência registrada somente quando confirmada pelo staff
- ✅ Gera dados adicionais pelo próprio fluxo (espera, chamada, conclusão)

**Desvantagens:**
- ❌ Depende de o staff confirmar cada conclusão
- ❌ Exige sincronização em tempo real entre app, staff e monitor
- ❌ Maior complexidade de backend

---

### 2.3 Matriz de Comparação

| Critério | A: Entrada/Saída | B: Código estação | C: QR estação | D: Staff isolado | E: Fila + staff |
|----------|------------------|-------------------|---------------|------------------|-----------------|
| **Identifica experiências** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **Ação extra do participante** | Nenhuma | Alta | Média | Nenhuma | Nenhuma |
| **Confirmação de realização** | — | ❌ | ❌ | ✅ | ✅ |
| **Esforço do staff** | Nenhum | Nenhum | Nenhum | Alto | Baixo (já opera a fila) |
| **Organiza a espera** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Complexidade técnica** | Baixa | Baixa | Média | Média | Alta |

---

### 2.4 Decisão Adotada

**✅ Decisão adotada: fila virtual por estação + confirmação pelo staff (Alternativa E).**

**Justificativa:**
1. Responde ao requisito da empresa de filas por estação gerenciadas pelo staff
2. Reduz ações desnecessárias do participante (princípio de baixa fricção)
3. O registro é confiável, pois depende da confirmação de quem conduziu a experiência
4. O staff não tem trabalho adicional de busca: o participante já está identificado pela fila
5. O mesmo check que registra o dado também faz a fila avançar
6. Elimina a necessidade de QR Code individual por estação

**Pendente:** o sistema deve prever alertas/lembretes para o Staff realizar o check de conclusão; formato, tempo e canal desses alertas ainda serão definidos.

---

## 3. DECISÃO: BENEFÍCIO AO PARTICIPANTE

### 3.1 Contexto

Além de registrar dados para a empresa, o app deve oferecer valor ao participante. Que valor é esse?

### 3.2 Alternativas Consideradas

#### **ALTERNATIVA A: Histórico Simples**

Lista das participações, com o que foi feito em cada uma.

**Vantagens:**
- ✅ Simples de implementar
- ✅ Não "incha" a UX com gamificação

**Desvantagens:**
- ❌ Visão apenas por evento, sem consolidação

---

#### **ALTERNATIVA B: Histórico + Estatísticas Pessoais**

Histórico detalhado das participações + indicadores consolidados.

**Vantagens:**
- ✅ Oferece visão consolidada sem lógica de progressão
- ✅ Usa apenas dados que o próprio fluxo já registra
- ✅ Implementação viável

**Desvantagens:**
- ❌ Menor apelo de engajamento que gamificação

---

#### **ALTERNATIVA C: Progresso/Nível (Gamificação)**

Níveis, XP, barra de progresso, conquistas.

**Vantagens:**
- ✅ Pode incentivar retorno

**Desvantagens:**
- ❌ Requer lógica de progressão e regras de pontuação
- ❌ Pode parecer artificial
- ❌ Fora do escopo desta versão

---

#### **ALTERNATIVA D: Pontuação/Ranking**

Pontos e posição comparativa entre participantes.

**Vantagens:**
- ✅ Alto engajamento competitivo

**Desvantagens:**
- ❌ Pode criar competição não saudável e desmotivar quem não está no topo
- ❌ Pode desviar o foco da experiência para os pontos
- ❌ Fora do escopo desta versão

---

#### **ALTERNATIVA E: Recompensas**

Pontos resgatáveis por descontos, brindes ou vouchers.

**Vantagens:**
- ✅ Valor tangível ao participante

**Desvantagens:**
- ❌ Complexidade alta (economia de pontos, cupons, validade)
- ❌ Custo operacional e dependência de parcerias
- ❌ Fora do escopo desta versão

---

### 3.3 Matriz de Comparação

| Critério | Histórico | Histórico + Estatísticas | Progresso | Ranking | Recompensas |
|----------|-----------|--------------------------|-----------|---------|-------------|
| **Valor ao participante** | Médio | Bom | Bom | Questionável | Alto |
| **Simplicidade** | Alta | Alta | Média | Baixa | Baixa |
| **Complexidade de desenvolvimento** | Baixa | Baixa | Média | Alta | Muito alta |
| **Alinhamento com princípios** | ✅ | ✅ | ⚠️ | ❌ | ❌ |

---

### 3.4 Decisão Adotada

**✅ Decisão adotada: Histórico + Estatísticas Pessoais.**

**O participante terá como benefício:**
- Histórico de suas participações
- Eventos dos quais participou
- Horário de entrada e saída
- Tempo de permanência
- Experiências realizadas
- Avaliação feita
- Quantidade total de participações
- Tempo total acumulado nas Arenas

**Indicadores no Perfil:**
- **Participações**
- **Tempo total**

**Não haverá, nesta versão:** níveis, XP, barra de progresso, conquistas, ranking, pontos ou recompensas. A BEAST possui uma plataforma gamificada separada, o que não significa que o aplicativo da Arena precise ter esse tipo de sistema.

**Justificativa:**
1. Oferece valor sem complexidade excessiva
2. Reaproveita dados que o sistema já coleta (princípio de coleta transparente)
3. Evita engajamento artificial

---

## 4. DECISÃO: ORGANIZAÇÃO DAS FILAS DAS ESTAÇÕES

### 4.1 Contexto

Com o registro das experiências baseado em filas (Decisão 2), é preciso definir como as filas se organizam e quantas um participante pode ocupar.

### 4.2 Alternativas Consideradas

| Alternativa | Vantagens | Desvantagens |
|-------------|-----------|--------------|
| **Fila única para todas as estações** | Simples de exibir | Não reflete a operação real; estações com ritmos diferentes ficam presas umas às outras |
| **Uma fila por estação, várias filas simultâneas por participante** | Participante "reserva" vários lugares | Chamadas simultâneas para estações diferentes; posições ocupadas por quem não virá; gestão difícil para o staff |
| **Uma fila por estação, uma fila por participante por vez** | Chamadas sem conflito; filas refletem quem realmente está esperando | Participante espera uma experiência de cada vez |

### 4.3 Decisão Adotada

**✅ Decisão adotada: cada estação possui sua própria fila.**

Exemplos:
- PlayStation → fila própria
- Realidade Virtual → fila própria
- Simulador → fila própria
- Demais experiências → suas respectivas filas

O participante visualiza pelo aplicativo sua situação/posição na fila em que estiver.

**✅ Restrição obrigatória: um participante só pode estar em uma fila de estação por vez.**

- Enquanto estiver aguardando, chamado ou sendo atendido em determinada estação, não pode entrar simultaneamente em outra fila
- Após o staff concluir sua experiência, ele fica novamente disponível para entrar em outra fila

**Justificativa operacional:** evita chamadas simultâneas para diferentes experiências e simplifica o gerenciamento da participação pelo staff.

---

## 5. DECISÃO: CHAMADA DO PARTICIPANTE

### 5.1 Contexto

Quando chega a vez do participante, ele precisa saber que foi chamado e para onde ir. O staff precisa saber quem está sendo chamado, e o público da Arena se beneficia de uma visualização coletiva.

### 5.2 Alternativas Consideradas

| Alternativa | Vantagens | Desvantagens |
|-------------|-----------|--------------|
| **Chamada somente no app** | Individual e direta | Participante pode não estar olhando o celular |
| **Chamada somente em monitor/voz** | Visível para todos | Participante precisa estar perto do monitor; sem registro no app |
| **App + monitor + área do staff sincronizados** | Várias formas de o participante perceber a chamada; staff acompanha o mesmo estado | Exige sincronização em tempo real |

### 5.3 Decisão Adotada

**✅ Decisão adotada: chamada sincronizada entre app, monitor público e área do staff.**

- **App do participante:** informa claramente que ele foi chamado e para qual estação deve se dirigir
- **Monitor público da Arena:** apresenta as chamadas em tempo real
- **Área do staff:** apresenta quem está sendo atendido/chamado e permite gerenciar o avanço da fila

O monitor público e o aplicativo **não representam filas diferentes**. São visualizações diferentes do mesmo estado da fila.

---

## 6. REQUISITO OPERACIONAL: NÃO COMPARECIMENTO

### 6.1 Contexto

A empresa informou que, quando um participante for chamado e não estiver presente, ele deverá ser movido para o final da fila.

### 6.2 Fluxo

```
Participante chamado → não compareceu → staff marca ausência
   → participante retorna ao final da fila daquela estação
```

**Justificativa:** a fila continua andando para quem está presente, sem excluir quem se ausentou momentaneamente.

### 6.3 Pendentes

As regras abaixo ainda **não estão definidas** e não fazem parte desta decisão:
- Número máximo de ausências
- Remoção definitiva após determinado número de chamadas
- Penalizações
- Tempo limite exato para comparecimento

---

## 7. DECISÃO: FILA DE ACESSO À ARENA

### 7.1 Contexto

Além das filas individuais das estações, pode ser necessária uma fila de acesso à própria Arena quando houver excesso de público. Esse excesso não acontece durante todo o evento.

**Não confundir:**
- **Fila da Arena** = controle de acesso ao espaço
- **Fila de estação** = espera para uma experiência específica

### 7.2 Alternativas Consideradas

| Alternativa | Vantagens | Desvantagens |
|-------------|-----------|--------------|
| **Sem fila de acesso** | Entrada direta | Sem controle quando a Arena lota |
| **Fila de acesso permanente** | Controle constante | Etapa desnecessária quando há pouco público |
| **Fila ativável/desativável pelo staff** | Controle apenas quando necessário | Exige que o estado mude em tempo real para todos |

### 7.3 Decisão Adotada

**✅ Decisão adotada: fila da Arena ativável/desativável pelo staff durante o evento** (Fila da Arena: SIM / NÃO, ou mecanismo equivalente).

**Quando desativada:**
```
QR/código → confirmação → entrada na Arena
```

**Quando ativada:**
```
QR/código → confirmação → entrada na fila da Arena
   → acompanhamento da posição → liberação → entrada efetiva na Arena
```

Isso permite que um evento comece sem fila de acesso e que o staff a ative posteriormente caso o fluxo de pessoas aumente. Da mesma forma, ela pode ser desativada quando deixar de ser necessária.

**✅ Regra de permanência:** o tempo aguardando na fila de acesso **não** conta como tempo de permanência na Arena. O timer de permanência começa somente quando a entrada efetiva do participante for liberada.

**✅ Desativação com pessoas aguardando:** se o Staff desativar a fila de acesso enquanto existem participantes aguardando, **todos são liberados automaticamente**, sem liberação individual. Para essas pessoas a espera termina, a entrada efetiva é registrada e o tempo de permanência começa. Quem já estava dentro da Arena não é afetado.

**Justificativa:** a desativação significa que a lotação deixou de ser um problema; manter pessoas esperando uma liberação manual criaria atraso sem motivo operacional.

---

## 8. DECISÃO: UMA PARTICIPAÇÃO ATIVA POR USUÁRIO

### 8.1 Contexto

A participação é o registro de um usuário em um evento, com timer, filas e experiências próprios. Se um usuário pudesse manter duas participações abertas ao mesmo tempo, o sistema não saberia a qual evento atribuir tempo, filas e experiências.

### 8.2 Alternativas Consideradas

| Alternativa | Vantagens | Desvantagens |
|-------------|-----------|--------------|
| **Várias participações simultâneas** | Nenhuma restrição ao usuário | Conflito de timer, permanência, filas, experiências e estado do participante; dados pouco confiáveis |
| **Uma participação ativa por vez** | Estado sempre claro; dados de permanência confiáveis; evita entrada duplicada | Usuário precisa encerrar a participação atual antes de entrar em outro evento |

### 8.3 Decisão Adotada

**✅ Decisão adotada: cada usuário pode possuir apenas uma participação ativa por vez.**

- Enquanto existir uma participação ativa, o usuário não pode iniciar participação em outro evento
- Ao tentar, o app informa que já existe uma participação em andamento
- Nenhuma penalidade está associada a essa tentativa

---

## 9. DECISÃO: COLETA DO PERFIL DO PARTICIPANTE

### 9.1 Contexto

Conhecer o perfil do público é parte central do problema da BEAST: a experiência presencial acontece, mas a empresa não sabe quem são os participantes nem qual é a relação deles com games e com o mercado de games. Ao mesmo tempo, um questionário longo contraria o princípio de baixa fricção.

### 9.2 Dados Solicitados pela Empresa

- Idade
- Gênero
- Escolaridade
- Jogos que costuma jogar
- Se já conhece o mercado de games
- Se tem interesse no mercado profissional de games

O **nome** e o **e-mail** já são coletados no cadastro e não são perguntados novamente.

### 9.3 O que foi removido do questionário anterior

| Item antigo | Motivo da remoção |
|-------------|-------------------|
| Idade por faixa etária | A empresa quer a idade; o campo numérico é igualmente rápido |
| Frequência com que joga | Não foi solicitado pela empresa |
| Gêneros favoritos | Substituído pelos jogos que a pessoa realmente joga |
| Uma pergunta obrigatória por tela | Aumentava o número de telas sem necessidade |
| Tela final "Seus dados estão corretos?" | Etapa extra; os dados podem ser editados no Perfil |

### 9.4 Decisão Adotada

**✅ Decisão adotada: questionário em 3 etapas curtas, logo após o cadastro.**

1. **Sobre você:** idade (numérica), gênero (com "Outro" + especificação e "Prefiro não informar"), escolaridade ("Qual o nível mais alto de ensino que você cursa ou já cursou?")
2. **Seus jogos:** pesquisa + sugestões + seleção em chips, com adição manual; pelo menos 1 jogo
3. **Mercado de games:** conhecimento do mercado e interesse profissional

**Como o atrito é reduzido:** poucas etapas, seleções rápidas em vez de texto livre, nenhuma pergunta redundante, remoção de frequência e gêneros favoritos, ausência de tela de confirmação e edição posterior no Perfil.

### 9.5 Finalidade Específica

A empresa informou que as respostas sobre conhecimento e interesse no mercado de games poderão ser usadas futuramente para direcionar o participante a conhecer a plataforma da BEAST.

**Pendente:** o mecanismo desse direcionamento (momento, formato e regra de segmentação) ainda será definido. Nenhum popup, botão, link ou redirecionamento faz parte desta decisão.

---

## 10. RESUMO DAS DECISÕES

| Tema | Decisão atual |
|------|---------------|
| **Entrada no evento** | QR Code principal + código manual alternativo, seguidos de confirmação |
| **Registro das experiências** | Fila virtual por estação + confirmação pelo Staff |
| **Benefício ao participante** | Histórico + Estatísticas Pessoais (sem XP, níveis ou ranking) |
| **Filas das experiências** | Cada estação possui sua própria fila |
| **Participação em filas** | Uma fila de estação por participante por vez |
| **Chamada** | App + Staff + monitor público refletem o mesmo estado |
| **Não comparecimento** | Retorno ao final da fila da estação |
| **Controle de acesso** | Fila da Arena ativável/desativável pelo Staff |
| **Permanência** | Espera na fila de acesso não conta como permanência |
| **Desativação da fila de acesso** | Todos que aguardam são liberados automaticamente |
| **Participação ativa** | Uma participação ativa por usuário |
| **Perfil do participante** | Questionário em 3 etapas com os dados solicitados pela empresa |

### Questões em Aberto
- Comportamento sem conexão com a internet (depende da arquitetura técnica)
- Tempo de tolerância após uma chamada
- Quantidade máxima de ausências e eventuais penalidades
- Tecnologia de sincronização em tempo real
- Backend e banco de dados definitivos
- Papel técnico do Google Drive (informado pela empresa como armazenamento; não assumido como banco operacional)
- Mecanismo de direcionamento para a plataforma da BEAST
- Formato dos alertas ao Staff para o check de conclusão
- Identidade visual definitiva (Figma)

---

## 11. ESTADO ATUAL DO PROJETO

| Etapa | Estado |
|-------|--------|
| Estrutura, fluxos e interfaces | ✅ Consolidados |
| Regras de negócio principais | ✅ Definidas |
| Protótipo estrutural HTML | ✅ Fluxos principais navegáveis |
| Identidade visual / Figma | ⏳ A desenvolver |
| Regras técnicas (backend, sincronização, offline) | 🔍 Em avaliação |

