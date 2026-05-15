# Sistema de Agendamento de Equipamentos Escolares (SAEE)
**Documento Mestre do Projeto**

## 1. Visão Geral e Contexto
O **SAEE** é uma aplicação web monolítica voltada para o uso interno da Escola de Tempo Integral Vinícius de Moraes (Palmas - TO). 

O projeto nasce para resolver um problema grave de logística interna: o atual agendamento manual (em papel) de equipamentos multimídia causa conflitos de horários, perda de rastreabilidade física e inviabiliza um histórico de uso ou controle de inventário. 

A solução proposta substitui o caderno físico por um sistema centralizado, utilizando os **8 blocos rígidos de aula** (4 pela manhã, 4 pela tarde) como base de tempo, garantindo reservas sem conflitos e um painel de baixas em tempo real.

### Stack Tecnológica
- **Backend:** Java 17+, Spring Boot 3.x, Spring Security.
- **Banco de Dados:** MySQL 8.0.
- **Frontend:** Bootstrap 5 renderizado com Thymeleaf. Responsivo (Mobile-first para Professores, Desktop-first para Servidores).
- **Infraestrutura:** Docker.

---

## 2. Personas e Casos de Uso

### Personas Principais
1. **Professor (ex: Carlos Eduardo):** Usuário final. Precisa entrar rapidamente pelo celular e reservar um projetor com poucos cliques, sabendo exatamente o que está livre para o dia e bloco desejados.
2. **Servidor / Gestor (ex: Maria de Fátima):** Usuário de balcão (Almoxarifado). Precisa de uma tela de computador aberta o dia todo, com botões grandes e ágeis para dar baixa (Entregar/Devolver) nas trocas de turno, pois a fila de professores pode ser grande.

### User Stories (US)
- **US-01:** Como Professor, quero visualizar o catálogo filtrado por data e bloco para saber o que está livre.
- **US-02:** Como Professor, quero criar uma reserva para minha turma num bloco específico para garantir o item.
- **US-03:** Como Servidor, quero ver a fila do bloco atual para preparar as entregas.
- **US-04:** Como Servidor, quero dar baixa com 1 clique (Entregue/Devolvido) para manter a rastreabilidade física em tempo real.

---

## 3. Regras de Negócio e Sistema

- **Regra da Grade (Blocos Rígidos):** Diferente de agendas comuns, o SAEE tem zero flexibilidade de horários. Agendamentos são atrelados OBRIGATORIAMENTE à data, equipamento, turma e a 1 dos 8 blocos de aula.
- **Prevenção de Conflitos:** Bloqueio sistêmico rigoroso de duplicidade de reserva (mesmo `id_equipamento`, mesma `data`, mesmo `bloco_aula`).
- **Regra dos 5 Minutos:** Bloqueio sistêmico de novas reservas caso faltem 5 minutos ou menos para o início do bloco, forçando o hábito de planejamento prévio.
- **Máquina de Estados de Equipamento:** O sistema trabalhará com os status: `DISPONIVEL`, `RESERVADO`, `EM_USO`, `ATRASADO`, `MANUTENCAO`.
- **Soft Delete:** Nenhum registro é deletado fisicamente do banco de dados (obrigatoriedade de soft delete).
- **Atraso Automático:** Um rotina em background (`@Scheduled`) muda automaticamente o status para `ATRASADO` (em vermelho) se o bloco acabou e o servidor não confirmou a devolução.
- **Manutenção Súbita:** Se um equipamento for marcado como `MANUTENCAO`, todas as reservas futuras do dia são automaticamente canceladas e o servidor é notificado.

---

## 4. Escopo do MVP (Produto Mínimo Viável)

O desenvolvimento priorizará a matriz MoSCoW:

### MUST (Obrigatório - O que entra)
- Login/Autenticação nativa via Spring Security (`ROLE_PROFESSOR`, `ROLE_SERVIDOR`).
- CRUD básico manual de Usuários, Itens e Turmas (Visão Servidor).
- Motor de reserva travado nos 8 blocos.
- Painel Operacional de fila do Servidor (botões ágeis "Entregue" / "Devolvido").
- Trava sistêmica dos 5 minutos antes da aula.
- Status automático de "Atrasado".

### SHOULD (Desejável)
- Exportação de relatório CSV da tabela de agendamentos.

### COULD (Poderia ter - Fora da v1)
- Filtro avançado por "tipo" de item (Ex: notebooks, projetores).
- Campo de justificativa de cancelamento.

### WON'T (Fora do Escopo Inicial)
- Integrações complexas (SGE, Gov.br, WhatsApp, Email).
- Leitores de QR Code nas máquinas.

---

## 5. Diretrizes de UI/UX

O design será clean, funcional e focado na agilidade (evitando fadiga visual e cliques desnecessários).

### Cores e Status
- **Primária (Cabeçalho):** `#1a365d` (Azul Marinho)
- **Secundária (Ações):** `#3182ce` (Azul Interativo)
- **Background:** `#f7fafc` (Cinza Gelo)
- **Status Disponível/Sucesso:** `#2f855a` (Verde)
- **Status Ocupado:** `#c05621` (Laranja)
- **Status Atrasado/Manutenção/Alerta:** `#9b2c2c` (Vermelho)

### Componentes e Telas
- **Landing Page (Login):** Focada na conversão imediata para login interno. Lado esquerdo com logo da escola, direito com card de login. Abaixo, tabela com regras de horário e alerta vermelho sobre a "Regra dos 5 minutos". Sem viés comercial.
- **Tipografia:** Padrão do sistema (`Arial`, `Helvetica`), com títulos em peso `700` e corpo `400` na cor `#2d3748`.
- **Formas:** Componentes ligeiramente arredondados (Bootstrap `.rounded` - 4px) e sombras suaves (`.shadow-sm`) para destaque.
- **Modais Críticos:** Confirmações de devolução ou exclusão serão feitas via modais nativos, para que o Servidor não perca o contexto nem precise recarregar a tela da fila de trabalho.

---

## 6. Métricas de Sucesso
1. **Adoção:** 100% de agendamentos no sistema na primeira semana (substituição total do papel).
2. **Eficiência:** 0% de conflitos de reservas.
3. **Validação Operacional:** Comprovar que a interface desktop do servidor é rápida o suficiente para não causar atrasos no balcão nos horários de intervalo.