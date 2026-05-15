# Sistema de Agendamento de Equipamentos Escolares (SAEE)

## Descrição Preliminar
O SAEE é um sistema web que visa facilitar e centralizar o agendamento de equipamentos para uso em aulas, eventos e outras atividades que necessitem de recursos tecnológicos na escola.

## Contexto e Realidade da Escola
A escola alvo é a **Escola de Tempo Integral Vinícius de Moraes**, localizada em Palmas - TO. 
As aulas são divididas em 8 tempos diários (4 pela manhã e 4 pela tarde), onde cada aula tem a duração de 1 hora.

### Grade de Horários
- **Manhã:**
  - 1ª Aula: 08:00 - 09:00
  - 2ª Aula: 09:00 - 10:00
  - 3ª Aula: 10:00 - 11:00
  - 4ª Aula: 11:00 - 12:00
- **Tarde:**
  - 1ª Aula: 13:00 - 14:00
  - 2ª Aula: 14:00 - 15:00
  - 3ª Aula: 15:00 - 16:00
  - 4ª Aula: 16:00 - 17:00

## O Problema
Atualmente, o agendamento de equipamentos multimídia (projetores, caixas de som, notebooks, etc.) é feito de forma manual no papel. Esse processo causa:
- Conflitos de horário (duas reservas para o mesmo equipamento no mesmo momento).
- Equipamentos "perdidos" na escola devido à falta de rastreamento de quem está com o aparelho.
- Falta de histórico de agendamentos e dificuldades no controle do estado de conservação dos itens.

## A Solução
O SAEE substituirá o controle em papel por uma plataforma web centralizada. 

- **Visão do Professor:** Terá acesso a um painel (dashboard) onde poderá reservar os equipamentos baseando-se diretamente na grade de aulas da escola, visualizando apenas o que está disponível para o horário desejado.
- **Visão do Servidor (Responsável):** Terá uma visão geral para gerenciar inventário, estado de conservação, entregas/devoluções do dia e controle de usuários do sistema.

## Diferencial
Diferente de uma agenda comum baseada em horas ou minutos (que permite reservas em horários "quebrados"), o sistema é **moldado na rotina da escola de tempo integral**, trabalhando exclusivamente com blocos de "tempos de aula" (1º ao 4º horário da manhã/tarde). Isso simplifica a interface, agiliza a reserva e evita conflitos.

## Métricas de Sucesso
- Redução a zero dos conflitos de reserva.
- Geração de relatórios mensais de utilização (por professor e por equipamento).
- Controle e redução no índice de perda ou dano de equipamentos não rastreados.

## Requisitos e Funcionalidades

### Requisitos Funcionais
- **Autenticação:** Login baseado em perfis com níveis de acesso diferentes (Professor, Servidor).
- **Gestão de Grade:** Bloqueio e liberação de reservas baseado nos 8 tempos de aula definidos.
- **Prevenção de Conflitos:** O sistema não pode permitir sobreposição de agendamentos para o mesmo item e horário.
- **Gestão de Estado de Equipamento:** Equipamentos marcados como "em manutenção" ou "quebrados" ficam ocultos na listagem de reserva.
- **Relatórios:** Geração de relatórios de agendamento por período (em formato PDF e/ou CSV).

### Casos de Uso por Perfil

#### 👨‍🏫 Professor
- Fazer login no sistema.
- Visualizar um dashboard com seu histórico pessoal e reservas futuras.
- Visualizar catálogo de equipamentos disponíveis na escola.
- Realizar e cancelar suas reservas.

#### 👨‍💻 Servidor (Gestor de Equipamentos)
- Fazer login no sistema.
- Visualizar dashboard com a fila de trabalho diária (entregas e recolhas previstas para o dia).
- Gerenciar (Criar, Ler, Atualizar, Deletar) os usuários do tipo Professor.
- Gerenciar Turmas e Horários.
- Gerenciar Equipamentos (cadastro, edição, exclusão e alteração de status de conservação).
- Gerar relatórios gerenciais.