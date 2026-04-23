# tabela-de-distribui-o-de-frequencias
from collections import Counter
import pandas as pd
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)
pd.set_option('display.width', None)

#Criando a base de dados:
dados = [14]*6 + [15]*12 + [16]*9 + [17]*3

#Frequência Absoluta (fi):
fi = pd.Series(Counter(dados)).sort_index()

#Frequência Absoluta Acumulada (fia):
fia = fi.cumsum()

#Frequência Relativa (fr):
fr = 100 * fi / fi.sum()

#Frequência Relativa Acumulada (fra):
fra = fr.cumsum()

#Montando a tabela:
tabela = pd.DataFrame({
 'Frequencia_Absoluta': fi,
 'Frequencia_Absoluta_Acumulada': fia,
 'Frequencia_Relativa': fr,
 'Frequencia_Relativa_Acumulada': fra
})

#Nome "Total" na última linha:
total_row = pd.Series({
 'Frequencia_Absoluta': fi.sum(),
 'Frequencia_Absoluta_Acumulada': '',
 'Frequencia_Relativa': fr.sum(),
 'Frequencia_Relativa_Acumulada': ''
}, name='Total')

#Tabela de Distribuição de Frequências:
tabela = pd.concat([tabela, total_row.to_frame().T])
print(tabela)
