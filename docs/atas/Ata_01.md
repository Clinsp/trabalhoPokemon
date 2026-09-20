# Relatório da Fase 01 - Projeto PokeSal
**Equipe:** Pukemon (Caio Lins e Joao Marcelo)

## 1. Relatório de Análise Estática de Requisitos

Durante a análise dos requisitos fornecidos, a dupla identificou as seguintes ambiguidades que precisam ser definidas antes da codificação:

1. **Empate de Velocidade (SPD):** O documento diz que a ordem de ataque é definida estritamente pela Velocidade (SPD), mas não especifica o que acontece se ambos os pokesals tiverem o mesmo valor de SPD.
   - **Solução adotada pela equipe:** Em caso de empate na SPD, o pokesal controlado pelo jogador 1 terá a iniciativa ou um sitema de randomizacao.

2. **Valores de Cura dos Itens:** O requisito "Gerenciamento de Mochila" cita itens como Potion e Super Potion, mas omite a quantidade exata de HP que cada um recupera.
   - **Solução adotada pela equipe:** *Potion* recuperará 20 HP e *Super Potion* recuperará 50 HP.

3. **Duração de Efeitos de Status:** O documento menciona efeitos no final do turno (Queimado, Envenenado, Paralisado), mas não informa se eles são permanentes ou se expiram após X turnos.
   - **Solução adotada pela equipe:** Os efeitos de status durarão até que um item de cura específico seja utilizado.
  - **Exceção (Paralisia):** Caso o efeito seja paralisia, o pokesal perderá o status de paralisado automaticamente após 4 rodadas. a paralisia terá 40% de chance de impedir o pokesal de atacar no turno.

4. **Limite de HP Máximo:** Não está claro se o HP pode ultrapassar o valor base ao sofrer cura do efeito de terreno ou uso de itens.
   - **Solução adotada pela equipe:** A cura nunca poderá ultrapassar o HP máximo inicial do pokesal.

---

## 2. Definição dos Requisitos Autorais

Abaixo estão os 3 requisitos novos e completamente autorais criados pela equipe:

### Requisito Autoral 1: Mecânica de "Ataque Crítico" (Sorte)
- **Descrição:** Todo ataque tem 10% de chance de causar 50% de dano adicional.
- **Regra de Negócio:** No momento do cálculo de dano, o sistema gera um número aleatório. Se o número cair na margem de 10%, o dano final do ataque sofre um multiplicador de `1.5x`.

### Requisito Autoral 2: Item "Bebida Energética UCSal"
- **Descrição:** Um novo item na mochila que não cura HP, mas aumenta permanentemente o atributo SPD do pokesal em 10 pontos pela duração daquela batalha.
- **Regra de Negócio:** O uso consome o turno do treinador (respeitando o limite de 2 itens por batalha) e soma `+10` no atributo de velocidade daquele pokesal até o combate encerrar.

### Requisito Autoral 3: Mecânica de "Esquiva Perfeita"
- **Descrição:** Existe uma pequena chance do pokesal desviar completamente do golpe inimigo.
- **Regra de Negócio:** Antes de calcular o dano recebido, o sistema rola uma chance de 5%. Se o desvio ocorrer, o ataque erra, o pokesal recebe 0 de dano e o console exibe a mensagem "Esquiva Perfeita!".
