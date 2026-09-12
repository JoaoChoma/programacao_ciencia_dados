# Atividade Prática

## Fundamentos de Python

Nesta atividade, você desenvolverá um pequeno programa para registrar informações sobre equipamentos e suas operações.

### Conceitos avaliados

```python
int
float
str
bool

list
tuple

type()

int()
float()
str()
bool()
```

---

# Cenário

Uma empresa precisa registrar informações básicas sobre seus equipamentos.

Para um determinado equipamento foram coletados os seguintes dados:

```text
Código: ESC-01
Tipo: Escavadeira
Ano: 2022
Horas trabalhadas: 8.5
Combustível consumido: 95.7 litros
Equipamento ativo: Sim
Localização da operação: -23.42, -51.93
```

Você deverá representar e manipular essas informações utilizando Python.

---

# Parte 1 — Representando os dados

Crie as seguintes variáveis:

```text
codigo
tipo
ano
horas_trabalhadas
combustivel
ativo
```

Escolha o tipo Python mais adequado para cada informação.

Utilize:

```python
int
float
str
bool
```

---

# Parte 1 — Verificação

Depois de criar as variáveis, apresente seus valores e tipos.

Exemplo:

```python
print(codigo)
print(type(codigo))
```

Faça isso para **todas as variáveis**.

---

# Resultado esperado

Seu programa deverá permitir identificar algo semelhante a:

```text
ESC-01
<class 'str'>

Escavadeira
<class 'str'>

2022
<class 'int'>

8.5
<class 'float'>

95.7
<class 'float'>

True
<class 'bool'>
```

---

# Parte 2 — Produzindo uma informação

Utilizando:

```python
horas_trabalhadas
combustivel
```

calcule o consumo de combustível por hora:

```text
                 combustível consumido
consumo/hora = ─────────────────────────
                   horas trabalhadas
```

Armazene o resultado em:

```python
consumo_hora
```

---

# Parte 2 — Resultado

Apresente:

```text
Equipamento: ESC-01
Horas trabalhadas: 8.5
Combustível: 95.7 litros
Consumo por hora: ???
```

Não escreva o resultado manualmente.

O valor deverá ser calculado pelo programa.

---

# Parte 3 — Trabalhando com strings

Utilizando a variável:

```python
codigo = "ESC-01"
```

apresente:

1. o código original;
2. o código em letras minúsculas;
3. o código em letras maiúsculas;
4. a quantidade de caracteres do código.

Pesquise/utilize:

```python
.lower()
.upper()
len()
```

---

# Parte 4 — Conversão de tipos

Imagine que os dados foram importados de um arquivo e chegaram ao programa desta forma:

```python
ano_texto = "2022"
horas_texto = "8.5"
combustivel_texto = "95.7"
```

Verifique inicialmente os tipos:

```python
print(type(ano_texto))
print(type(horas_texto))
print(type(combustivel_texto))
```

---

# Parte 4 — Conversão

Converta:

```text
ano_texto
```

para:

```python
int
```

E:

```text
horas_texto
combustivel_texto
```

para:

```python
float
```

Armazene os resultados em novas variáveis.

---

# Parte 4 — Testando

Depois da conversão, execute:

```python
print(valor)
print(type(valor))
```

para cada variável convertida.

Explique:

> Por que `"8.5"` e `8.5` representam coisas diferentes para Python?

---

# Parte 5 — Lista de equipamentos

A empresa possui inicialmente:

```text
ESC-01
ESC-02
ESC-03
```

Crie uma lista:

```python
equipamentos = ...
```

---

# Parte 5 — Manipulando a lista

Utilizando a lista criada:

1. apresente a lista completa;
2. apresente apenas o primeiro equipamento;
3. apresente apenas o último equipamento;
4. adicione `ESC-04`;
5. altere `ESC-02` para `ESC-02-A`;
6. apresente a quantidade de equipamentos.

Utilize, quando necessário:

```python
append()
len()
```

---

# Parte 6 — Horas trabalhadas

Considere as horas trabalhadas pelos equipamentos:

```text
ESC-01 → 8.5 horas
ESC-02 → 7.0 horas
ESC-03 → 9.5 horas
ESC-04 → 6.0 horas
```

Crie uma lista contendo apenas as horas:

```python
horas = [...]
```

---

# Parte 6 — Operações com a lista

Utilizando a lista `horas`, descubra:

1. quantidade de registros;
2. total de horas trabalhadas;
3. média de horas trabalhadas;
4. maior quantidade de horas;
5. menor quantidade de horas.

Você pode utilizar:

```python
len()
sum()
max()
min()
```

Para a média:

```text
         soma das horas
média = ────────────────
        quantidade
```

---

# Parte 7 — Tupla

A operação do equipamento `ESC-01` aconteceu aproximadamente na coordenada:

```text
Latitude:  -23.42
Longitude: -51.93
```

Represente a coordenada utilizando uma `tuple`.

```python
coordenada = ...
```

---

# Parte 7 — Acessando a tupla

Apresente separadamente:

```text
Latitude: ...
Longitude: ...
```

A partir dos valores armazenados na tupla.

---

# Parte 7 — Experimento

Depois de criar:

```python
coordenada = (-23.42, -51.93)
```

tente executar:

```python
coordenada[0] = -24.00
```

Observe o resultado.

Responda:

> Por que Python não permite essa operação?

---

# Parte 8 — List × Tuple

Considere:

```python
equipamentos = [
    "ESC-01",
    "ESC-02",
    "ESC-03"
]

coordenada = (
    -23.42,
    -51.93
)
```

Responda:

1. Qual estrutura é mutável?
2. Qual estrutura é imutável?
3. Em qual delas podemos utilizar `append()`?
4. Por que uma coordenada pode ser adequadamente representada por uma tupla?
5. Em que situação você escolheria uma lista em vez de uma tupla?

---

# Desafio final

Um novo registro chegou do sistema:

```python
codigo = "ESC-05"
ano = "2021"
horas = "9.5"
combustivel = "112.8"
ativo = True
coordenada = (-23.45, -51.92)
```

Observe que alguns valores numéricos foram armazenados como texto.

---

# Sua missão

Construa um pequeno programa que:

1. verifique os tipos originais;
2. converta `ano` para `int`;
3. converta `horas` para `float`;
4. converta `combustivel` para `float`;
5. calcule o consumo por hora;
6. apresente as informações do equipamento;
7. adicione o código do equipamento a uma lista de equipamentos;
8. apresente latitude e longitude separadamente.

---

# Saída esperada

O resultado deverá apresentar informações semelhantes a:

```text
EQUIPAMENTO: ESC-05
ANO: 2021
HORAS TRABALHADAS: 9.5
COMBUSTÍVEL: 112.8
CONSUMO POR HORA: 11.87
ATIVO: True

LOCALIZAÇÃO
Latitude: -23.45
Longitude: -51.92
```

Os valores devem ser obtidos a partir das variáveis e dos cálculos realizados pelo programa.

---

# Entrega

Entregue o notebook `.ipynb` contendo:

- código executado;
- resultados das células;
- respostas das questões conceituais;
- desafio final funcionando.

Organize o notebook utilizando células Markdown para identificar cada parte.

---

# Critérios de avaliação

| Critério | Valor |
|---|---:|
| Uso adequado de `int`, `float`, `str` e `bool` | 1,5 |
| Identificação e conversão de tipos | 1,5 |
| Operações e cálculos com os valores | 1,5 |
| Criação e manipulação de `list` | 2,0 |
| Criação e utilização de `tuple` | 1,0 |
| Desafio final | 2,0 |
| Organização e legibilidade do notebook | 0,5 |
| **Total** | **10,0** |

---

# O que está sendo avaliado?

Mais importante do que decorar a sintaxe é demonstrar que você consegue decidir:

```text
Qual tipo representa este dado?
          ↓
Preciso converter?
          ↓
É um valor ou uma coleção?
          ↓
A coleção precisa mudar?
          ↓
LIST ou TUPLE?
          ↓
Que informação posso calcular?
```