# 🧃 Previsão de Demanda para uma Empresa de Sucos Naturais

Este projeto usa inteligência artificial para **prever quantos litros de cada sabor de suco serão vendidos no mês seguinte** na **Claujuices**, uma pequena empresa de sucos naturais que produz sob demanda ("produção puxada"): só se produz o que os clientes vão comprar.

O objetivo é ajudar a empresa a decidir **quanto produzir e quanto comprar de insumos**, evitando dois problemas comuns:

- **Sobra de produto e de fruta**, que estraga e vira prejuízo;
- **Falta de produto**, que significa venda perdida.

O trabalho foi desenvolvido na Universidade Federal do Pampa (UNIPAMPA), Campus Bagé, e resultou no artigo *"Inteligência Artificial Aplicada à Previsão de Demanda em Sistemas de Produção Puxada: Um Estudo em uma Empresa de Sucos"*, incluído neste repositório.


## 📊 Os dados

A própria empresa forneceu o histórico de vendas de **15 sabores** entre **abril de 2025 e junho de 2026**. Cada linha da base mostra quantos litros de um sabor foram vendidos em um mês, junto com informações que podem influenciar a venda:

- mês do ano e temperatura média;
- número de dias úteis e de fins de semana;
- se houve feriado;
- se o sabor é um lançamento recente;
- quanto foi vendido no mês anterior e a média dos últimos três meses.

Cerca de **53% dos registros têm volume zero**, porque alguns sabores são novos ou vendem muito pouco. Por isso, os modelos foram treinados só com os **9 sabores que tiveram vendas em pelo menos 6 meses** (abacaxi, abacaxi com hortelã, bergamota, laranja, laranja com couve, limonada, maracujá, morango e uva). Os demais, como butiá, goiaba, manga, melancia e pink lemonade, ainda não têm histórico suficiente.

## 🔬 O que foi feito

Foram comparados dois modelos para prever as vendas de cada sabor:

1. **Regressão linear:** um modelo simples, que relaciona as informações acima com o volume vendido;
2. **Rede neural LSTM:** um modelo mais sofisticado, que olha os últimos 3 meses de cada sabor para prever o próximo.

A pergunta era: **o modelo mais complexo prevê melhor?**

## 🏆 Principais resultados

**A regressão linear foi melhor que a rede neural na maioria dos sabores** (8 de 9). A LSTM só ganhou na limonada. O motivo é que cada sabor tem apenas de 9 a 12 meses de histórico, o que é pouco para uma rede neural aprender bem. Nesse cenário, o modelo simples se mostrou mais estável.

**Um número geral pode enganar.** Os dois modelos tiveram uma nota global muito alta (R² de 0,90 e 0,98), o que parece ótimo. Mas olhando sabor por sabor, a maioria foi mal. Isso acontece porque a laranja vende muito mais que os outros sabores e "puxa" a nota geral para cima. Por isso, a avaliação principal do trabalho foi feita **sabor a sabor**.

**Teste real com junho de 2026.** Os modelos foram treinados até maio e usados para prever junho:

- **Laranja** (o sabor mais vendido): previsão de 152,7 L (regressão) e 154,3 L (LSTM), contra **152 L** vendidos de fato, um erro menor que 2%;
- **Sabores de baixo volume:** as previsões erraram mais. O caso mais extremo foi o abacaxi, que caiu para 3 L em junho. A regressão previu 32,8 L e a LSTM 13,4 L. Nada parecido tinha acontecido antes no histórico, então nenhum modelo poderia antecipar.


## 📂 Estrutura do Repositório

```
.
├── model_claujuices.ipynb           # Notebook com preparação dos dados, regressão linear e LSTM
├── sucos_claujuices_jun2026.csv     # Base de vendas mensais por sabor
├── Artigo_DemandaPuxada.pdf         # Artigo completo
└── Artigo_DemandaPuxada/            # Código-fonte LaTeX do artigo
```
