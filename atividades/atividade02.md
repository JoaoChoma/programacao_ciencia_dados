# Atividade Prática 2

## Processando dados de equipamentos com Python

### Objetivo

Nesta atividade você utilizará os conceitos:

```python
dict
set

if
elif
else

for
while

def

try
except

np.array
```

O objetivo é construir um pequeno programa capaz de **representar, validar, processar e analisar dados de equipamentos**.

---

# Cenário

Uma empresa registrou informações sobre a operação de seus equipamentos.

Cada equipamento possui:

```text
código
tipo
horas trabalhadas
combustível consumido
produção
```

Os registros serão utilizados para calcular indicadores e identificar diferentes níveis de utilização.

---

# Parte 1 — Representando um equipamento

Crie um dicionário para representar:

```text
Código: ESC-01
Tipo: Escavadeira
Horas trabalhadas: 8
Combustível: 95 litros
Produção: 120 m³
```

Utilize a estrutura:

```python
equipamento = {
    ...
}
```

---

# Parte 1 — Acessando o dicionário

Utilizando o dicionário criado, apresente:

```text
Código: ESC-01
Tipo: Escavadeira
Horas: 8
Combustível: 95
Produção: 120
```

Os valores devem ser obtidos utilizando suas respectivas chaves.

Exemplo:

```python
equipamento["codigo"]
```

---

# Parte 1 — Alterando o dicionário

Adicione ao equipamento:

```text
ativo = True
```

Depois adicione:

```text
operador = Carlos
```

Apresente o dicionário atualizado.

---

# Parte 2 — Vários equipamentos

Agora temos quatro equipamentos:

```text
ESC-01 | Escavadeira      | 8 h  | 95 L  | 120 m³
ESC-02 | Escavadeira      | 7 h  | 87 L  | 100 m³
ESC-03 | Caminhão         | 10 h | 150 L | 180 m³
ESC-04 | Pá carregadeira  | 4 h  | 68 L  | 85 m³
```

Represente cada equipamento utilizando um `dict`.

Depois coloque os quatro dicionários dentro de uma `list`.

Estrutura esperada:

```python
equipamentos = [
    {...},
    {...},
    {...},
    {...}
]
```

---

# Parte 3 — Percorrendo os equipamentos

Utilize:

```python
for
```

para percorrer a lista.

Para cada equipamento apresente:

```text
ESC-01 - Escavadeira
ESC-02 - Escavadeira
ESC-03 - Caminhão
ESC-04 - Pá carregadeira
```

Não escreva quatro comandos `print()`.

Utilize apenas um `print()` dentro do `for`.

---

# Parte 4 — Classificando a utilização

Vamos considerar:

```text
horas > 8
    → ALTA UTILIZAÇÃO

horas >= 5 e horas <= 8
    → UTILIZAÇÃO NORMAL

horas < 5
    → BAIXA UTILIZAÇÃO
```

Utilize:

```python
if
elif
else
```

dentro do `for`.

---

# Resultado esperado

Seu programa deverá produzir algo semelhante a:

```text
ESC-01 → UTILIZAÇÃO NORMAL
ESC-02 → UTILIZAÇÃO NORMAL
ESC-03 → ALTA UTILIZAÇÃO
ESC-04 → BAIXA UTILIZAÇÃO
```

---

# Parte 5 — Calculando o total

Utilize um `for` para calcular o total de horas trabalhadas.

Comece com:

```python
total_horas = 0
```

Depois percorra os equipamentos acumulando suas horas.

Ao final:

```python
print(total_horas)
```

---

# Parte 5 — Média

Utilizando:

```text
total de horas
quantidade de equipamentos
```

calcule:

```text
         total de horas
média = ─────────────────
         quantidade
```

Apresente a média.

---

# Parte 6 — Valores únicos com set

Observe os tipos dos equipamentos:

```text
Escavadeira
Escavadeira
Caminhão
Pá carregadeira
```

Queremos descobrir:

> Quais tipos de equipamentos aparecem nos dados?

Crie inicialmente:

```python
tipos = []
```

Percorra os equipamentos e adicione seus tipos à lista.

---

# Parte 6 — Eliminando duplicidades

Depois transforme a lista em:

```python
set
```

Exemplo:

```python
tipos_unicos = set(tipos)
```

Apresente o resultado.

---

# Pergunta

Explique:

> Por que `set` é adequado para descobrir as categorias existentes nos dados?

---

# Parte 7 — Criando uma função

Até agora calculamos o consumo por hora diretamente.

Vamos transformar esse cálculo em uma função.

Crie:

```python
def calcular_consumo_hora(combustivel, horas):
    ...
```

A função deverá retornar:

```text
combustível
───────────
   horas
```

---

# Testando a função

Execute:

```python
resultado = calcular_consumo_hora(
    95,
    8
)

print(resultado)
```

O resultado deve ser aproximadamente:

```text
11.875
```

---

# Parte 8 — Função de classificação

Crie:

```python
def classificar_utilizacao(horas):
    ...
```

A função deverá retornar:

```text
ALTA UTILIZAÇÃO
UTILIZAÇÃO NORMAL
BAIXA UTILIZAÇÃO
```

de acordo com as regras anteriores.

---

# Testando

```python
print(
    classificar_utilizacao(10)
)

print(
    classificar_utilizacao(7)
)

print(
    classificar_utilizacao(3)
)
```

Resultado esperado:

```text
ALTA UTILIZAÇÃO
UTILIZAÇÃO NORMAL
BAIXA UTILIZAÇÃO
```

---

# Parte 9 — Aplicando as funções aos dados

Agora combine:

```text
for
+
dict
+
def
+
if
```

Percorra todos os equipamentos.

Para cada um, calcule:

```text
consumo por hora
```

e:

```text
classificação de utilização
```

---

# Resultado esperado

Algo semelhante a:

```text
EQUIPAMENTO: ESC-01
Consumo/hora: 11.875
Utilização: UTILIZAÇÃO NORMAL

EQUIPAMENTO: ESC-02
Consumo/hora: 12.43
Utilização: UTILIZAÇÃO NORMAL

...
```

Os resultados devem ser calculados pelo programa.

---

# Parte 10 — Um problema nos dados

Um novo valor foi recebido de um sistema externo:

```python
horas = "oito"
```

Tente executar:

```python
horas = float(horas)
```

O que aconteceu?

---

# Tratando o problema

Utilize:

```python
try
```

e:

```python
except
```

para impedir que o programa seja interrompido.

```python
try:
    horas = float(horas)

except ValueError:
    print("Valor inválido")
```

---

# Parte 10 — Teste

Seu programa deverá funcionar para:

```python
horas = "8.5"
```

e tratar adequadamente:

```python
horas = "oito"
```

Explique:

> Qual problema o `try/except` resolve nesse exemplo?

---

# Parte 11 — while

Imagine que queremos simular a leitura de cinco registros.

Utilize:

```python
while
```

para apresentar:

```text
Processando registro 1
Processando registro 2
Processando registro 3
Processando registro 4
Processando registro 5
```

Não escreva cinco `print()`.

---

# Parte 11 — Atenção

Explique o que aconteceria se retirássemos:

```python
contador = contador + 1
```

do código.

> Por que devemos tomar cuidado com a condição de um `while`?

---

# Parte 12 — Do Python para NumPy

Considere:

```python
horas = [
    8,
    7,
    10,
    4
]
```

Transforme essa lista em um array NumPy.

```python
import numpy as np

horas_np = ...
```

---

# Inspecionando o array

Apresente:

```python
type(horas_np)
```

```python
horas_np.ndim
```

```python
horas_np.shape
```

```python
horas_np.size
```

Responda:

1. Quantas dimensões possui?
2. Qual seu formato?
3. Quantos elementos possui?
4. Podemos considerá-lo um vetor?

---

# Parte 13 — for × NumPy

Primeiro calcule o dobro das horas utilizando `for`.

Exemplo de resultado:

```text
[16, 14, 20, 8]
```

---

# Agora com NumPy

Execute:

```python
horas_np * 2
```

Compare as duas soluções.

Responda:

> Qual diferença você percebe entre percorrer explicitamente os elementos com `for` e realizar uma operação sobre todo o array?

---

# Parte 14 — Array bidimensional

Considere:

```text
HORAS | COMBUSTÍVEL | PRODUÇÃO
  8   |      95     |   120
  7   |      87     |   100
 10   |     150     |   180
  4   |      68     |    85
```

Crie:

```python
operacoes = np.array([
    ...
])
```

---

# Inspecione

Execute:

```python
operacoes.ndim
```

```python
operacoes.shape
```

```python
operacoes.size
```

Responda:

> Por que esse array possui duas dimensões?

---

# Desafio Final

## Mini processamento de dados

Considere:

```python
equipamentos = [
    {
        "codigo": "ESC-01",
        "tipo": "Escavadeira",
        "horas": 8,
        "combustivel": 95,
        "producao": 120
    },
    {
        "codigo": "ESC-02",
        "tipo": "Escavadeira",
        "horas": 7,
        "combustivel": 87,
        "producao": 100
    },
    {
        "codigo": "CAM-01",
        "tipo": "Caminhão",
        "horas": 10,
        "combustivel": 150,
        "producao": 180
    },
    {
        "codigo": "PAC-01",
        "tipo": "Pá carregadeira",
        "horas": 4,
        "combustivel": 68,
        "producao": 85
    }
]
```

---

# Sua missão

Construa um programa que:

1. percorra todos os equipamentos;
2. apresente código e tipo;
3. calcule o consumo por hora utilizando uma função;
4. classifique a utilização utilizando outra função;
5. calcule o total de horas;
6. calcule a média de horas;
7. descubra os tipos únicos utilizando `set`;
8. crie um array NumPy contendo todas as horas;
9. apresente `ndim`, `shape` e `size` do array;
10. identifique o equipamento com maior quantidade de horas.

---

# Saída

O programa deverá produzir um pequeno relatório:

```text
=== RELATÓRIO DE OPERAÇÕES ===

ESC-01
Tipo: Escavadeira
Horas: 8
Consumo/hora: 11.88
Utilização: UTILIZAÇÃO NORMAL

...

----------------------------

Total de horas: ...
Média de horas: ...

Tipos encontrados:
{...}

Array de horas:
[...]

Dimensões: ...
Formato: ...
Quantidade: ...

Maior utilização:
...
```

---

# Questões finais

Responda utilizando células Markdown:

1. Qual a diferença entre `list` e `set`?
2. Qual a vantagem de representar um equipamento com `dict`?
3. Qual a diferença entre `if` e `for`?
4. Quando utilizaríamos `while`?
5. Qual o benefício de criar uma função com `def`?
6. Para que serve `try/except`?
7. Qual a diferença entre uma lista Python e um array NumPy?
8. O que significa dizer que um array possui uma ou duas dimensões?

---

# Critérios de avaliação

| Critério | Valor |
|---|---:|
| Uso de `dict` e acesso por chaves | 1,0 |
| Uso de `set` e valores únicos | 0,5 |
| Decisões com `if/elif/else` | 1,0 |
| Repetições com `for` e `while` | 1,5 |
| Criação e utilização de funções | 1,5 |
| Tratamento com `try/except` | 1,0 |
| Criação e manipulação de arrays NumPy | 1,5 |
| Desafio final e integração dos conceitos | 1,5 |
| Respostas conceituais | 0,5 |
| **Total** | **10,0** |

---

# O fluxo que estamos construindo

Nesta atividade começamos a sair de comandos isolados:

```text
DADOS
  ↓
dict / list
  ↓
VALIDAÇÃO
try / except
  ↓
DECISÃO
if
  ↓
PROCESSAMENTO
for / while
  ↓
REUTILIZAÇÃO
def
  ↓
ORGANIZAÇÃO NUMÉRICA
NumPy / array
```

Esse fluxo prepara o próximo passo:

```text
ARRAY
  ↓
Series
  ↓
DataFrame
  ↓
pandas
  ↓
ANÁLISE DE DADOS
```