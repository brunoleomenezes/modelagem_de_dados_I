# Projeto de Banco de Dados
**Disciplina:** Modelagem de Dados I (MD I)  

---

## Objetivo
Construir, em grupo, um **projeto de banco de dados completo**, passando pelas etapas:

1. Levantamento de requisitos.
2. Modelo Entidade-Relacionamento (DER).
3. Modelo Relacional (MR).
4. Implementação em SQL no OneCompiler PostgreSQL.
5. Execução de consultas.

---

## Situação-Problema
Vocês são **analistas de sistemas** contratados para informatizar uma **pequena empresa**.  
Cada grupo poderá escolher ou receber um dos cenários descritos a seguir.  

---

## Etapas da Atividade

### 1. Levantamento de Requisitos
- Identificar os principais atores do sistema (clientes, funcionários, produtos, pedidos, etc.).
- Listar os dados que precisam ser armazenados.

### 2. Modelo Conceitual (DER)
- Construir o Diagrama Entidade-Relacionamento (DER) usando **dbdiagram.io**, **draw.io** ou no papel.
- Incluir entidades, atributos, relacionamentos e cardinalidades.

### 3. Modelo Relacional (MR)
- Migrar o DER para tabelas relacionais.
- Definir tabelas, atributos, chaves primárias e estrangeiras.
- Normalizar até a 3FN, justificando brevemente.

### 4. Implementação em SQL (OneCompiler PostgreSQL)
- Criar as tabelas usando `CREATE TABLE`.
- Definir corretamente tipos de dados, `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`.
- Inserir pelo menos 5 registros por tabela usando `INSERT INTO`.

### 5. Consultas SQL
Criar pelo menos 5 consultas que respondam a perguntas do negócio. Exemplos:
- Listar todos os clientes cadastrados.
- Mostrar pedidos feitos em determinada data.
- Encontrar o produto mais vendido.
- Calcular o total de vendas de um cliente.
- Listar serviços realizados por um funcionário específico.

---

## Entregáveis
Cada grupo deverá entregar:

1. DER (imagem ou desenho).
2. Modelo Relacional (tabelas com atributos e chaves).
3. Script SQL usado no OneCompiler (CREATE + INSERT).
4. Consultas SQL com resultados exibidos.
5. Relatório final em PDF ou apresentação curta (5 a 10 min) explicando as escolhas.

---

## Critérios de Avaliação
- Clareza e organização do DER (20%).
- Correção do Modelo Relacional e normalização (20%).
- Implementação em SQL correta no OneCompiler (20%).
- Qualidade das consultas SQL (20%).
- Apresentação e defesa do projeto (20%).

---

## Cenário 1 — E-commerce de Eletrônicos "TechStore RJ"

### Contexto
A **TechStore RJ** é uma loja virtual especializada em venda de eletrônicos (celulares, notebooks, periféricos e acessórios).  
A empresa precisa organizar seus dados em um banco de dados relacional para controlar clientes, pedidos, estoque, entregas e pagamentos.

### Requisitos levantados
1. **Clientes**: cada cliente possui nome, CPF, e-mail, telefone, endereço completo (rua, número, bairro, cidade, estado, CEP). Um cliente pode ter mais de um telefone e mais de um endereço de entrega.  
2. **Produtos**: cadastrados com código, nome, descrição, preço unitário, marca, categoria (ex.: celular, notebook, periférico) e quantidade em estoque. Podem ter desconto promocional.  
3. **Pedidos**: cada pedido possui data, status (em aberto, pago, enviado, entregue, cancelado) e forma de pagamento (cartão, boleto, pix). Um cliente pode ter vários pedidos, e cada pedido pertence a um único cliente. Um pedido pode ter vários itens (produto + quantidade).  
4. **Pagamentos**: cada pedido gera um pagamento: data, valor total, status (pago, pendente, recusado). Se cartão: registrar número parcial (últimos 4 dígitos) e bandeira. Se pix: chave pix usada. Se boleto: código de barras.  
5. **Entregas**: cada pedido pago gera uma entrega: transportadora, código de rastreio, prazo estimado, data de entrega. Status: em transporte, entregue, devolvido.  

### Entidades sugeridas
Clientes, TelefonesCliente, EnderecosCliente, Produtos, Categorias, Pedidos, ItensPedido, Pagamentos, Entregas.

### Regras de negócio
- O estoque deve ser reduzido quando o pedido é confirmado.
- Não pode haver pedido sem pelo menos 1 item.
- Um cliente pode cadastrar até 3 endereços diferentes de entrega.
- O pagamento precisa estar **pago** para liberar a entrega.

### Exemplos de dados
- Cliente: João Silva, CPF 123.456.789-10, e-mail joao@email.com, 2 telefones, 1 endereço.
- Produto: Notebook Dell Inspiron 15, R$ 3.500,00, estoque 20.
- Pedido: 02/09/2025, status = pago, cliente João.
- Itens: 1 notebook Dell + 2 mouses sem fio.
- Pagamento: cartão Visa, final 1234, valor total R$ 3.960,00.
- Entrega: Transportadora Correios, código BR123456, entregue em 05/09/2025.

---

## Cenário 2 — Clínica Médica "Vida & Saúde"

### Contexto
A **Clínica Vida & Saúde** oferece consultas médicas e exames laboratoriais.  
O objetivo é criar um banco de dados para organizar pacientes, médicos, consultas, exames, receitas e faturamento.

### Requisitos levantados
1. **Pacientes**: nome, CPF, RG, sexo, data de nascimento, telefone, e-mail, endereço completo. Um paciente pode ter plano de saúde ou ser particular. Deve haver registro de histórico de alergias.  
2. **Médicos**: nome, CRM, especialidade (cardiologia, ortopedia, pediatria, etc.), telefone, e-mail. Um médico pode atender em vários horários e dias da semana.  
3. **Consultas**: data, hora, paciente, médico, sala, status (agendada, realizada, cancelada). Cada consulta pode gerar uma receita médica.  
4. **Receitas médicas**: associadas a uma consulta. Contêm medicamentos (nome, dosagem, instruções).  
5. **Exames**: associados a uma consulta (opcional). Tipo de exame (sangue, raio-x, ultrassom, etc.), data do exame, resultado e médico responsável.  
6. **Faturamento**: cada consulta/exame gera uma cobrança: valor, forma de pagamento (dinheiro, cartão, convênio), status do pagamento. Convênios precisam registrar número da carteirinha e operadora.  

### Entidades sugeridas
Pacientes, TelefonesPaciente, Médicos, Consultas, Receitas, ItensReceita, Exames, Pagamentos, Convenios.

### Regras de negócio
- Um paciente pode agendar várias consultas, mas uma consulta é sempre com um único médico.
- Uma consulta pode gerar múltiplos exames.
- Receita médica está sempre vinculada a uma consulta.
- O pagamento pode ser particular ou via convênio.
- Exames só podem ser realizados após a consulta.

### Exemplos de dados
- Paciente: Maria Souza, CPF 987.654.321-00, convênio Unimed, carteirinha 11223344.
- Médico: Dr. Carlos Mendes, CRM 12345, especialidade cardiologia.
- Consulta: 10/09/2025 às 14h, status realizada.
- Receita: Dipirona 500mg (1 comprimido a cada 8h por 5 dias).
- Exame: Eletrocardiograma, resultado normal, realizado em 11/09/2025.
- Pagamento: convênio Unimed, autorizado, valor R$ 150,00 repassado pela operadora.

---

**© 2025 — Professor Bruno Menezes**
