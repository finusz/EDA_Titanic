# Analise exploratória dos dados de Titanic

Titanic é um _dataset_ popular, principalmente para projetos de aprendizado de máquina (AM). Tendo isso em mente, realizei uma pequena analise exploratória para entender como _dataset_ está organziado. A analise veio com a finalidade de saber se quanto mais cara for a passagem, mais houve chances de sobreviver ao afundamento do Titanic.

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
None
--------------------------------
survived         0
pclass           0
sex              0
age            177
sibsp            0
parch            0
fare             0
embarked         2
class            0
who              0
adult_male       0
deck           688
embark_town      2
alive            0
alone            0

O conjunto é formado por 891 registros distintos, e possui 15 características. E possui ao todo 869 dados vazios.
Para melhorar a compreensão e preencher os valores nulos; a idade (coluna _age_) dos passageiros que apareciam como vazias, foram preenchidas com a média aparada de todos, a média aparada foi escolhida por ser mais robusta a outliers; A demais, a cidade de embarque (coluna _embark_town_) e o embarque (coluna _embarked_) foram preenchido como "Não informado" por não tem informações desses dados; Igualmente, o deck (cabine) foi rotulado como "Não Informado" por não ter indicação de qual seja, mas futuramente pode ser identificado com um modelo de AM em um aprendizado semi-supervisionado.

         survived      pclass         age       sibsp       parch        fare
count  891.000000  891.000000  891.000000  891.000000  891.000000  891.000000
mean     0.383838    2.308642   29.613719    0.523008    0.381594   32.204208
std      0.486592    0.836071   13.003148    1.102743    0.806057   49.693429
min      0.000000    1.000000    0.420000    0.000000    0.000000    0.000000
25%      0.000000    2.000000   22.000000    0.000000    0.000000    7.910400
50%      0.000000    3.000000   29.269231    0.000000    0.000000   14.454200
75%      1.000000    3.000000   35.000000    1.000000    0.000000   31.000000
max      1.000000    3.000000   80.000000    8.000000    6.000000  512.329200
Nota: Como foi aplicado a média aparada, a média da idade se aproxima da mediana.

<img width="590" height="481" alt="image" src="https://github.com/user-attachments/assets/0dd7a576-aa9a-4c9c-aece-69aefe4dc04f" />
Em primeiro momento, não vemos nenhuma correção forte o suficiente para ser relevante para nossa pergunta, porém podemos observar que há uma correlação negativa entre o a classe da passagem (_pclas_) e a tarifa (_fare_).

Quando observamos, atráves do boxplot, a distribuição da idade e tarifa dos passageiros pela classe, percebemos que na primeira classe se concentra os passageiros mais velhos e que tiveram a tarifa maior.
<img width="475" height="421" alt="image" src="https://github.com/user-attachments/assets/3c97d39b-8225-45df-a409-570c9f916ca1" />
<img width="483" height="421" alt="image" src="https://github.com/user-attachments/assets/d6625597-cf1a-4ee8-b25f-8575af4387fe" />

Observando a quantidade de passageiros sobreviventes de cada classe, identificamos que houve mais sobreviventes da primeira classe, seguido da terceiro e a segunda foi a que menos teve sobreviventes:
<img width="490" height="390" alt="image" src="https://github.com/user-attachments/assets/f2146f3e-50d2-4097-a2c0-8c13991e1250" />

E apenas dos passageiros da teiceira classe apresentarem serem os segundos com mais sobreviventes, quando observa-se a média de sobrevivência de cada uma das classes, vemos que, em média, os pasageiros da segunda classe fora mais prospícios a sobreviventes, com uma média de quase 50%. Enquanto os da terceira classe obtiveram cerca de 25% de sobrevivência.
First     0.629630
Second    0.472826
Third     0.242363

Além disso, quando observamos essa informações, comparando o sexo dos passageiros, vemos que a média da idade dos homens é maior, mas as mulheres tem maiores tarifas, independente da classe.
<img width="473" height="421" alt="image" src="https://github.com/user-attachments/assets/763dd62c-8c25-4cbc-a488-66bd21d09cc6" />
<img width="476" height="421" alt="image" src="https://github.com/user-attachments/assets/a3aefdfa-6bb6-4f0c-a189-b392e97e49bb" />

E por fim, quando vemos a quantidade de sobreviventes, vemos que há mais mulheres sobreviventes em todas as classes do que os homens. Além da média de sobrevivência das mulheres está por cerca de 75%, enquanto dos homens é de um pouco menos de 20%
<img width="510" height="390" alt="image" src="https://github.com/user-attachments/assets/d60894c2-108a-48be-9872-4dfc8e1bd1fb" />

female    0.742038
male      0.188908
