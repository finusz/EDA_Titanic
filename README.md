# Análise Exploratória dos Dados do Titanic

Titanic é um _dataset_ popular, principalmente para projetos de aprendizado de máquina (AM). Tendo isso em mente, realizei uma pequena análise exploratória para entender como o _dataset_ está organizado.

Nesta analise, quis responder a pergunta "quanto mais cara a passagem do passageiro, maior a chance de sobrevivência ao afundamento do Titanic?"

---

## Informações do dataset

O conjunto é formado por **891 registros** distintos, com **15 características** e um total de **869 valores vazios**.

```
RangeIndex: 891 entries, 0 to 890
Data columns (total 15 columns):
 #   Column       Non-Null Count  Dtype   
---  ------       --------------  -----   
 0   survived     891 non-null    int64   
 1   pclass       891 non-null    int64   
 2   sex          891 non-null    object  
 3   age          714 non-null    float64 
 4   sibsp        891 non-null    int64   
 5   parch        891 non-null    int64   
 6   fare         891 non-null    float64 
 7   embarked     889 non-null    object  
 8   class        891 non-null    category
 9   who          891 non-null    object  
 10  adult_male   891 non-null    bool    
 11  deck         203 non-null    category
 12  embark_town  889 non-null    object  
 13  alive        891 non-null    object  
 14  alone        891 non-null    bool    
dtypes: bool(2), category(2), float64(2), int64(4), object(5)
memory usage: 80.7+ KB
```

**Valores nulos por coluna:**

| Coluna      | Nulos |
|-------------|-------|
| age         | 177   |
| embarked    | 2     |
| deck        | 688   |
| embark_town | 2     |

---

## Tratamento de dados

Para melhorar a compreensão e preencher os valores nulos:

- **`age`** → preenchida com a **média aparada** de todos os registros, por ser mais robusta a outliers.
- **`embark_town`** e **`embarked`** → preenchidos como `"Não informado"`, por falta de informação.
- **`deck`** → rotulado como `"Não Informado"`; apesar de ser o foco desta analise, essa característica pode ser predita por um modelo de AM em aprendizado semi-supervisionado.

Além do preenchimento dos valores nulos, também foi feito a tradução dos nomes das colunas e valores do dataset.

```
RangeIndex: 891 entries, 0 to 890
Data columns (total 15 columns):
 #   Column           Non-Null Count  Dtype  
---  ------           --------------  -----  
 0   sobreviveu       891 non-null    int64  
 1   pclasse          891 non-null    int64  
 2   sexo             891 non-null    object 
 3   idade            891 non-null    float64
 4   n_irmaosEsposa   891 non-null    int64  
 5   n_paisFilhos     891 non-null    int64  
 6   preco_passagem   891 non-null    float64
 7   local_embarque   891 non-null    object 
 8   classe           891 non-null    object 
 9   quem             891 non-null    object 
 10  homem_adulto     891 non-null    bool   
 11  cabine           891 non-null    object 
 12  cidade_embarque  891 non-null    object 
 13  vivo             891 non-null    object 
 14  sozinho          891 non-null    bool   
dtypes: bool(2), float64(2), int64(4), object(7)
memory usage: 92.4+ KB
```

---

## Estatísticas descritivas

|       | sobreviveu | pclasse | idade   | n_irmaosEsposa | n_paisFilhos | preco_passagem   |
|-------|----------|--------|-------|-------|-------|--------|
| count | 891      | 891    | 891   | 891   | 891   | 891    |
| mean  | 0.38     | 2.31   | 29.61 | 0.52  | 0.38  | 32.20  |
| std   | 0.49     | 0.84   | 13.00 | 1.10  | 0.81  | 49.69  |
| min   | 0.00     | 1.00   | 0.42  | 0.00  | 0.00  | 0.00   |
| 25%   | 0.00     | 2.00   | 22.00 | 0.00  | 0.00  | 7.91   |
| 50%   | 0.00     | 3.00   | 29.27 | 0.00  | 0.00  | 14.45  |
| 75%   | 1.00     | 3.00   | 35.00 | 1.00  | 0.00  | 31.00  |
| max   | 1.00     | 3.00   | 80.00 | 8.00  | 6.00  | 512.33 |

> Como foi aplicada a média aparada, a média da idade fica próxima da mediana.

---

## Correlações

Não há correlações fortes o suficiente para responder diretamente à pergunta, mas há uma **correlação negativa entre classe (`pclasse`) e tarifa (`preco_passagem`)**.

<img width="590" alt="matriz de correlação" src="https://github.com/user-attachments/assets/766b1786-c247-4a37-b18d-49c84e8d234a" />

---

## Idade e tarifa por classe

Na primeira classe se concentram os passageiros mais velhos e com tarifas mais altas.

<img width="475" alt="boxplot idade por classe" src="https://github.com/user-attachments/assets/4c785945-5223-4e18-8bc1-b05ff5548d6f" />
<img width="483" alt="boxplot tarifa por classe" src="https://github.com/user-attachments/assets/79bc5588-5689-4e19-ad92-fd8e46df668f" />

---

## Sobrevivência por classe

Em número absoluto de sobreviventes, a ordem foi: **1ª classe > 3ª classe > 2ª classe**.

<img width="490" alt="sobreviventes por classe" src="https://github.com/user-attachments/assets/7c618082-9271-4ce5-b785-a532eaa84a5a" />

Já em **taxa média de sobrevivência** por classe, o cenário muda:

| Classe | Taxa de sobrevivência |
|--------|------------------------|
| Primeira  | 62.96%                 |
| Segunda | 47.28%                 |
| Terceira  | 24.24%                 |

---

## Idade, tarifa e sobrevivência por sexo

A idade média dos homens é maior, mas as mulheres pagam tarifas mais altas, independentemente da classe.

<img width="473" alt="idade por sexo" src="https://github.com/user-attachments/assets/bba9e2ca-21ff-4776-95a5-9704e023a162" />
<img width="476" alt="tarifa por sexo" src="https://github.com/user-attachments/assets/c2ccc6ce-742d-4138-aaeb-f759f40e7abe" />

Há mais mulheres sobreviventes que homens em **todas as classes**:

<img width="510" alt="sobreviventes por sexo" src="https://github.com/user-attachments/assets/ba2279d2-dec8-454c-8634-2528c6034eed" />

| Sexo   | Taxa de sobrevivência |
|--------|------------------------|
| Fêmea | 74.20%                 |
| Macho   | 18.89%                 |

---

## Conclusão

- Passageiros da **primeira classe** tiveram maior probabilidade de sobrevivência do que os da **terceira classe**.
- **Mulheres** tiveram muito mais chance de sobreviver do que **homens**, em todas as classes.
