# Sistem de Agendamento de Equipamentos Escolar (SAEE)

## Descrição Preliminar
O SAEE é um sistema que visa facilitar o agendamento de equipamentos para uso em aulas, eventos e outras atividades que necessitem de recursos tecnológicos na escola.

## Usuários
- Professor
- Servidor 

## Realizade da escola
A escola se chama Escola de Tempo Integral Vinícius de Moraes e fica localizada em Palmas - TO. As aulas são dividias em 4 horários pela manhã e 4 horários pela tarde. Cada aula tem o periodo de 1 hora. 

## Problema
Atualmente, o agendamento de equipamentos multimédia (projetores, caixas de som, notebooks, etc) é feito manualmente em papel. Isso causa conflitos de horário, equipamentos "perdidos" na escola e falta de histórico dos agendamentos.

## Solução
Um sistema web centralizado onde no dashboard do professor ele possa reservar o equipamento baseado na grade de aulas da escola e na disponibilidade do equipamento. No dashboard do servidor responsável pelos equipamentos ele deve ter uma lista dos agendamentos, controle do inventário, controle do estado de conservação dos equipamentos e das entregas e devoluções. Ele tem uma visão geral de todos os equipamentos e agendamentos, podendo adicionar novos equipamentos, editar equipamentos existentes, adicionar novos usuários, editar usuários existentes e excluir usuários.

## Diferencial
Diferente de uma agenda comum, o sistema é moldado na rotina de uma escola de tempo integral, trabalhando com "tempos de aula" (1º ao 8º horário) em vez de horas quebradas.

## Horários de aula
- Manhã
    - 1º Aula: 08:00 - 09:00
    - 2º Aula: 09:00 - 10:00
    - 3º Aula: 10:00 - 11:00
    - 4º Aula: 11:00 - 12:00
- Tarde
    - 1º Aula: 13:00 - 14:00
    - 2º Aula: 14:00 - 15:00
    - 3º Aula: 15:00 - 16:00
    - 4º Aula: 16:00 - 17:00

## Métricas de Sucesso
- Redução a zero de conflitos de reserva (duas pessoas no mesmo horário).
- Relatórios mensais de utilização por professor e equipamento.

## Requisitos Funcionais
- **Autenticação:** Login por perfil (PROFESSOR, SERVIDOR).
- **Grade de Horários:** Permitir reserva nos horários: Manhã (1, 2, 3, 4) e Tarde (1, 2, 3, 4).
- **Bloqueio de Conflitos:** O sistema não deve permitir dois agendamentos para o mesmo item no mesmo horário.
- **Gestão de Estado:** Equipamentos em conserto ficam ocultos para reserva.
- **Relatórios:** O servidor deve gerar relatório de agendamentos por período (PDF/CSV).
- **Dashboard Servidor:** Lista cronológica de entregas e recolhas do dia.
- **Dashboard Professor:** Lista cronológica de reservas realizadas e pendentes.

## O que o sistema deve ter
- Professor
    - Fazer login no sistema
    - Dashboard do Professor com histórico pessoal.
    - Ver todos os equipamentos
    - Ver todas as reservas pendentes
- Servidor
    - Fazer login no sistema
    - Dashboard do Servidor com fila de trabalho diária.
    - Ver todos os equipamentos
    - Ver todas as reservas pendentes
    - Dashboard do servidor com fila de trabalho diária.
    - CRUD de Professores
    - CRUD de Horários
    - CRUD de Turmas
    - CRUD de Equipamentos com status.
    - Relatórios gerenciais