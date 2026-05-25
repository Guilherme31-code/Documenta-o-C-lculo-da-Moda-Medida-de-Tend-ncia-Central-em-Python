# Documenta-o-C-lculo-da-Moda-Medida-de-Tend-ncia-Central-em-Python
Na estatística, a moda representa o valor que aparece com maior frequência em um conjunto de dados. Diferente da média e da mediana, a moda pode ser aplicada tanto a dados numéricos quanto a dados categóricos (textos, booleanos, etc.).

Um conjunto de dados pode ser: Amodal: Nenhum valor se repete.Unimodal: Possui apenas uma moda.Bimodal / Multimodal: Possui dois ou mais valores com a mesma frequência máxima.2. Implementações DisponíveisAbaixo estão documentadas as três bibliotecas mais utilizadas em Python para extração da moda, adequadas para diferentes escalas e tipos de projeto.BibliotecaMódulo/FunçãoMelhor Caso de UsoTratamento de MultimodaisPadrão (Built-in)statistics.mode() / multimode()Listas simples e scripts rápidos.Requer o uso explícito de multimode().Pandaspandas.Series.mode()Análise de dados estruturados (CSVs, Tabelas).Retorna nativamente todos os valores modais.SciPyscipy.stats.mode()Matrizes multidimensionais (NumPy) e alta performance.Retorna a menor moda em caso de empate (comportamento padrão).3. Exemplos de Uso e Assinaturas de Métodos3.1. 

Usando a biblioteca nativa statisticsIdeal para operações onde não se deseja importar bibliotecas de terceiros.Nota de Versão: O método statistics.multimode() foi introduzido no Python 3.8 para resolver o problema de conjuntos de dados com mais de uma moda. O método mode() tradicional levanta um erro (StatisticsError) no Python 3.7 ou anterior se houver empate.Exemplo de Código:Pythonimport statistics

dados_unimodais = ['maçã', 'banana', 'maçã', 'laranja']
dados_bimodais = [1, 1, 2, 3, 3, 4]

# Extraindo uma única moda
moda_simples = statistics.mode(dados_unimodais)
print(f"Moda Simples: {moda_simples}") 
# Saída: Moda Simples: maçã

# Extraindo múltiplas modas (Bimodal)
modas = statistics.multimode(dados_bimodais)
print(f"Múltiplas Modas: {modas}") 
# Saída: Múltiplas Modas: [1, 3]
3.2. Usando a biblioteca pandasA escolha padrão para Ciência de Dados e análise tabular. O método .mode() é chamado diretamente na Série (coluna) ou DataFrame.Assinatura: Series.mode(dropna=True)dropna: Se True (padrão), ignora valores nulos (NaN).Exemplo de Código:Pythonimport pandas as pd

# Criando uma série (coluna de um DataFrame)
vendas = pd.Series([150.50, 200.00, 150.50, 300.00, 200.00, 450.00])

# O pandas sempre retorna uma Series com as modas encontradas
resultado_moda = vendas.mode()

print("Modas encontradas na coluna de vendas:")
print(resultado_moda)
# Saída:
# 0    150.5
# 1    200.0
# dtype: float64
3.3. Usando a biblioteca scipy.statsRecomendado para cálculos científicos em grandes arrays do numpy.Assinatura: scipy.stats.mode(a, axis=0, keepdims=False)a: Array de entrada.axis: Eixo ao longo do qual a moda será calculada.keepdims: Se True, mantém as dimensões reduzidas no resultado com tamanho um.Exemplo de Código:Pythonimport numpy as np
from scipy import stats

# Array NumPy
dados_sensor = np.array([12, 15, 12, 15, 12, 18, 19])

# Calcula a moda
resultado = stats.mode(dados_sensor, keepdims=True)

# O Scipy retorna um objeto contendo a moda e a contagem (frequência)
print(f"Valor da Moda: {resultado.mode[0]}")
print(f"Frequência absoluta: {resultado.count[0]}")
# Saída:
# Valor da Moda: 12
# Frequência absoluta: 3
4. Tratamento de Erros ComunsStatisticsError: no unique mode: Ocorre ao usar statistics.mode() em Python < 3.8 com dados bimodais/multimodais. Solução: Utilize statistics.multimode().Acesso a índice inexistente no Pandas: Como pd.Series.mode() retorna uma Series, tentar extrair o valor com .mode()[0] quando o conjunto de dados for completamente vazio (ou só contiver NaN com dropna=True) gerará um KeyError. Solução: Verifique se a série resultante não está vazia (if not resultado.empty:) antes de acessar o índice.
