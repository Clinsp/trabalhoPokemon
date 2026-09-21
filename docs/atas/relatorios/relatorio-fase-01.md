# Relatório da Fase 01 - Projeto PokeSal

**Equipe:** Pukemon (Caio Lins e João Marcelo)

## 1. Relatório de Análise Estática de Requisitos

Ao examinar os requisitos, encontramos algumas incertezas que precisariam ser esclarecidas antes do início da programação:

### 1. Empate de Velocidade (SPD)

A documentação afirma que a ordem de ataque é determinada unicamente pela Velocidade (SPD), porém, não detalha o que ocorre quando os dois pokesals atingem o mesmo valor de SPD.

- Solução que a equipe escolheu: Se houver um empate na SPD, o sistema irá sortear entre os dois pokesals. Cada um terá 50% de probabilidade de atacar primeiro.

### 2. Valores de Cura dos Itens

A seção sobre "Gerenciamento de Mochila" menciona itens como Potion e Super Potion, mas esquece de dizer a quantidade exata de HP recuperada por cada um.

- Solução que a equipe escolheu: Potion vai recuperar 20 HP e Super Potion vai recuperar 50 HP.

### 3. Duração de Efeitos de Status

O documento cita efeitos ao fim do turno (Queimado, Envenenado e Paralisado), mas não revela se eles ficam para sempre ou se desaparecem após um certo número de turnos.

- Solução que a equipe escolheu: Os efeitos de status vão durar até que um item de cura específico seja usado.
- Algo diferente — Paralisia: Se o efeito for paralisia, o pokesal perderá o estado automaticamente após 4 turnos. A paralisia também terá uma chance de 40% de impedir o pokesal de atacar durante o turno.

### 4. Limite de HP Máximo

Não fica evidente se o HP pode passar do valor máximo ao receber cura de um efeito do ambiente ou pelo uso de itens.

- Solução que a equipe escolheu: A cura jamais poderá fazer o HP atual passar do HP máximo inicial do pokesal.

---

## 2. Definição dos Requisitos Autorais

Os 3 requisitos elaborados pela equipe:

### Requisito Autoral 1: Mecânica de "Ataque Crítico"

- Descrição: Cada ataque tem uma chance de 10% de infligir 50% de dano extra.
- Regra de Negócio: No momento da contabilização do dano, o sistema gera um número aleatório. Se o número se enquadrar na janela de 10%, o valor final do dano do ataque receberá uma multiplicação de `1,5x`.

### Requisito Autoral 2: Item "Bebida Energética UCSal"

- Descrição: Um consumivel do inventário que o atributo VEL do pokesal em 10 pontos durante a batalha.
- Regra de Negócio: A utilização consome o turno do treinador, respeitando o teto de 2 itens aplicados por confronto, e acrescenta `+10` ao atributo de velocidade do pokesal até o fim da batalha.

### Requisito Autoral 3: Mecânica de "Esquiva Perfeita"

- Descrição:Uma probabilidade baixa de o pokesal desviar do ataque do adversário.
- Regra de Negócio: Antes do cálculo do dano recebido, o sistema efetua um sorteio com 5% de chance de esquiva. Caso a esquiva aconteça, o ataque falha, o pokesal recebe 0 de dano e o painel apresenta a notificação "Esquiva Perfeita!".