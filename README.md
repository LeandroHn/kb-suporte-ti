# Base de Conhecimento — Suporte Técnico (Help Desk)

**Projeto | Área: Suporte Técnico / Help Desk**

## Sobre este documento

Esta é uma base de conhecimento (Knowledge Base / KB) criada como projeto de
portfólio para demonstrar capacidade de documentação técnica — uma das
habilidades mais valorizadas em vagas de Help Desk júnior.

Cada artigo segue um padrão usado em bases de conhecimento reais de suporte
técnico: sintomas, causa provável, passo a passo de resolução, tempo estimado
e critério de quando escalar o chamado. O objetivo é que qualquer pessoa do
time de suporte — inclusive alguém no primeiro dia de trabalho — consiga
resolver o problema seguindo o documento, sem precisar perguntar a um colega
mais experiente.

**Formato usado em cada artigo:**
- Categoria e nível de prioridade típico
- Sintomas relatados pelo usuário
- Causa provável
- Passo a passo de resolução
- Tempo médio estimado
- Quando escalar para o Nível 2 (suporte mais avançado)

---

## Índice

1. [KB-001 — Wi-Fi não conecta](#kb-001--wi-fi-não-conecta)
2. [KB-002 — Impressora não imprime](#kb-002--impressora-não-imprime)
3. [KB-003 — Senha do Active Directory (AD) expirada / bloqueada](#kb-003--senha-do-active-directory-ad-expirada--bloqueada)
4. [KB-004 — Computador lento / travando](#kb-004--computador-lento--travando)
5. [KB-005 — Sem acesso a pasta compartilhada na rede](#kb-005--sem-acesso-a-pasta-compartilhada-na-rede)

---

## KB-001 — Wi-Fi não conecta

**Categoria:** Rede | **Prioridade típica:** Média

### Sintomas relatados pelo usuário
- "Meu Wi-Fi não conecta"
- "Aparece 'sem internet' mesmo com o Wi-Fi conectado"
- "Conecta mas cai toda hora"

### Causa provável
Na maioria dos casos: cache de rede desatualizado, driver de Wi-Fi
desatualizado, ou o dispositivo está tentando conectar a uma rede salva com
senha antiga (comum após troca de senha do roteador).

### Passo a passo de resolução

1. **Confirme o escopo do problema.** Pergunte ao usuário se outros
   dispositivos (celular, outro notebook) também estão sem conexão. Se sim,
   o problema é do roteador/provedor, não do computador — pule para o passo 6.
2. **Verifique se o Wi-Fi está fisicamente ativado** no computador (tecla de
   atalho ou ícone de avião no Windows — `Configurações > Rede e Internet`).
3. **Esqueça a rede e reconecte:**
   - `Configurações > Rede e Internet > Wi-Fi > Gerenciar redes conhecidas`
   - Selecione a rede com problema → **Esquecer**
   - Reconecte digitando a senha novamente
4. **Reinicie o adaptador de rede:**
   - `Configurações > Rede e Internet > Alterar opções do adaptador`
   - Clique com o botão direito no adaptador Wi-Fi → **Desativar** → aguarde
     5 segundos → **Ativar**
5. **Atualize o driver de rede**, se os passos acima não resolverem:
   - `Gerenciador de Dispositivos > Adaptadores de rede`
   - Botão direito no adaptador Wi-Fi → **Atualizar driver**
6. **Se o problema for no roteador**, reinicie-o (desligar da tomada por
   10 segundos) e aguarde a reinicialização completa (~1-2 minutos).

### Tempo médio estimado
5-10 minutos

### Quando escalar para o Nível 2
Se após os passos 1-6 o problema persistir, ou se o roteador/provedor
apresentar falha recorrente (mais de 2 ocorrências na semana) — encaminhar
para a equipe de infraestrutura de rede.

---

## KB-002 — Impressora não imprime

**Categoria:** Hardware/Periféricos | **Prioridade típica:** Baixa a Média

### Sintomas relatados pelo usuário
- "Mandei imprimir e não sai nada"
- "Fica 'na fila' e não avança"
- "Aparece erro ao tentar imprimir"

### Causa provável
Fila de impressão travada, impressora offline, driver desatualizado ou
problema de conexão (rede/USB).

### Passo a passo de resolução

1. **Verifique se a impressora está ligada e com papel/toner.** Parece óbvio,
   mas é a causa mais comum registrada em chamados reais.
2. **Confirme se a impressora aparece como "Pronta"** (não "Offline"):
   - `Configurações > Dispositivos > Impressoras e scanners`
   - Se estiver "Offline", clique nela → **Usar impressora online**
3. **Limpe a fila de impressão travada:**
   - Abra a fila de impressão (clique na impressora → **Abrir fila**)
   - Cancele todos os documentos travados
   - Se não cancelar pela interface, reinicie o serviço de spooler:
     `services.msc` → localizar **"Spooler de Impressão"** → botão direito →
     **Reiniciar**
4. **Teste com uma página de teste:**
   `Configurações > Impressoras e scanners > [impressora] > Imprimir página
   de teste`
5. **Verifique a conexão:**
   - Impressora de rede: confirme se está na mesma rede que o computador
   - Impressora USB: teste outro cabo/porta USB
6. **Reinstale o driver** se o problema persistir após os passos acima.

### Tempo médio estimado
5-15 minutos

### Quando escalar para o Nível 2
Se a fila trava repetidamente mesmo após reiniciar o spooler, ou se o
problema afeta todos os usuários de um mesmo setor (indica falha física da
impressora ou do servidor de impressão) — acionar suporte de infraestrutura
ou o fornecedor do equipamento.

---

## KB-003 — Senha do Active Directory (AD) expirada / bloqueada

**Categoria:** Acesso/Segurança | **Prioridade típica:** Alta
*(bloqueia o usuário de trabalhar completamente)*

### Sintomas relatados pelo usuário
- "Não consigo fazer login, diz que minha senha expirou"
- "Minha conta foi bloqueada depois de várias tentativas"
- "Esqueci minha senha"

### Causa provável
Política de expiração de senha do AD (geralmente a cada 60-90 dias) ou
bloqueio automático por excesso de tentativas incorretas de login.

### Passo a passo de resolução

1. **Confirme a identidade do usuário** antes de qualquer ação — solicitar
   nome completo, setor e, se a política da empresa exigir, outro dado de
   confirmação. *(Este passo é obrigatório: redefinir senha para a pessoa
   errada é uma falha grave de segurança.)*
2. **Verifique o status da conta** no Active Directory Users and Computers
   (ADUC) ou ferramenta equivalente:
   - Conta bloqueada → aparece o ícone de cadeado/bloqueio
   - Senha expirada → aparece aviso de expiração no perfil
3. **Se a conta estiver bloqueada:**
   - Botão direito no usuário → **Desbloquear conta**
4. **Se a senha estiver expirada ou o usuário esqueceu:**
   - Botão direito no usuário → **Redefinir senha**
   - Gere uma senha temporária seguindo a política de complexidade da empresa
   - Marque a opção **"Usuário deve alterar a senha no próximo logon"**
5. **Oriente o usuário** a fazer login com a senha temporária e criar uma
   nova senha pessoal imediatamente.
6. **Registre o atendimento** no sistema de chamados, incluindo motivo
   (expiração ou bloqueio) — isso ajuda a identificar padrões, como um
   usuário que erra a senha com frequência.

### Tempo médio estimado
5 minutos

### Quando escalar para o Nível 2
Se a conta continuar bloqueada mesmo após o desbloqueio manual (pode indicar
um dispositivo ou aplicativo tentando logar com credencial antiga em segundo
plano), ou se houver suspeita de tentativa de acesso não autorizado —
encaminhar para a equipe de segurança da informação.

---

## KB-004 — Computador lento / travando

**Categoria:** Software/Hardware | **Prioridade típica:** Média

### Sintomas relatados pelo usuário
- "Meu computador está muito lento"
- "Trava toda hora, principalmente de manhã"
- "Demora pra abrir qualquer programa"

### Causa provável
Excesso de programas iniciando junto com o Windows, pouco espaço em disco,
processos consumindo muita memória, ou atualizações pendentes acumuladas.

### Passo a passo de resolução

1. **Pergunte quando o problema começou** e se coincide com alguma instalação
   recente — isso já direciona a investigação.
2. **Abra o Gerenciador de Tarefas** (`Ctrl + Shift + Esc`) e verifique:
   - Uso de CPU e memória (algum processo consumindo acima de 80%
     constantemente?)
   - Aba **Inicializar** — muitos programas com impacto "Alto" no boot
3. **Desative programas desnecessários na inicialização:**
   - Gerenciador de Tarefas → aba **Inicializar** → botão direito nos
     programas não essenciais → **Desativar**
4. **Verifique espaço em disco:**
   - `Este Computador` → disco C: — se estiver abaixo de 10-15% de espaço
     livre, isso já explica boa parte da lentidão
   - Execute a **Limpeza de Disco** do Windows para remover arquivos
     temporários
5. **Confirme se há atualizações do Windows pendentes** acumuladas
   (`Configurações > Windows Update`) — atualizações grandes não instaladas
   podem deixar o sistema lento em segundo plano.
6. **Reinicie o computador** (parece básico, mas resolve boa parte dos casos
   de lentidão por acúmulo de processos em memória).
7. **Rode uma verificação de antivírus**, caso ainda não tenha sido feita
   recentemente — processo desconhecido consumindo CPU pode ser malware.

### Tempo médio estimado
15-30 minutos

### Quando escalar para o Nível 2
Se o disco estiver com uso saudável, sem processos anormais, e o problema
persistir mesmo após reinicialização — pode ser hardware com defeito
(memória RAM ou HD/SSD), o que exige diagnóstico físico da equipe de suporte
avançado.

---

## KB-005 — Sem acesso a pasta compartilhada na rede

**Categoria:** Acesso/Rede | **Prioridade típica:** Média a Alta
*(depende de quão crítica é a pasta para o trabalho do usuário)*

### Sintomas relatados pelo usuário
- "Não consigo abrir a pasta do setor"
- "Aparece 'acesso negado' quando tento entrar na pasta compartilhada"
- "A pasta sumiu do meu computador"

### Causa provável
Permissão de acesso não concedida (ou revogada) no AD, unidade de rede
desconectada, ou problema de conectividade com o servidor de arquivos.

### Passo a passo de resolução

1. **Confirme o caminho exato da pasta** que o usuário está tentando acessar
   (ex: `\\servidor\financeiro`) — muitos chamados de "acesso negado" na
   verdade são caminho digitado errado.
2. **Verifique a conectividade básica**: o usuário consegue acessar outras
   pastas de rede? Se nenhuma funciona, o problema é de rede/VPN, não de
   permissão específica — trate como problema de conexão primeiro.
3. **Confirme as permissões do usuário no Active Directory:**
   - Verifique se o usuário pertence ao grupo de segurança correto
     associado àquela pasta (ex: grupo `GRP_Financeiro`)
   - Se não pertencer, adicione o usuário ao grupo apropriado (respeitando
     a política de aprovação da empresa, se houver)
4. **Peça para o usuário tentar reconectar a unidade de rede:**
   - `Este Computador > Mapear unidade de rede`
   - Inserir novamente o caminho da pasta
5. **Aguarde a propagação da permissão**, se acabou de ser adicionada ao
   grupo — em ambientes AD isso pode levar alguns minutos; oriente o usuário
   a fazer logoff e login novamente para atualizar.
6. **Teste o acesso** junto com o usuário antes de encerrar o chamado.

### Tempo médio estimado
10-20 minutos (pode variar se depender de aprovação de acesso)

### Quando escalar para o Nível 2
Se o usuário já pertence ao grupo correto e mesmo assim recebe "acesso
negado", ou se o problema afeta vários usuários do mesmo setor ao mesmo
tempo — pode ser falha do servidor de arquivos, encaminhar para
infraestrutura.

---

## Habilidades demonstradas neste projeto

- Documentação técnica clara e estruturada, seguindo padrão real de base de
  conhecimento usado em empresas
- Capacidade de diagnóstico passo a passo (do sintoma à causa raiz)
- Definição de critérios objetivos de escalonamento (Nível 1 → Nível 2)
- Pensamento em processo, não só em solução pontual — cada artigo inclui
  verificação de identidade, tempo estimado e critério de quando pedir ajuda

**Autor:** [Leandro]
**Data:** setembro de 2026
