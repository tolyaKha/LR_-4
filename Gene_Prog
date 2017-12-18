import random

top_quantity = 4 # количество вершин графа
gene_quantity = 2 # количество генов, хромосома;максимальное количество преодолеваемых вершин без учета начальной (start_top) и конечной (end_top)
individual_quantity = 4 # количество особей; должно быть кратно 2-м для скрещивания
start_top = 1 # начальная вершина графа
end_top = 2 # конечная вершина графа
generation_quantity = 4 # количество поколений
min_edge_weight = 10 # минимальный вес ребра графа
max_edge_weight = 30 # максимальный вес ребра графа
inf_edge_weight = 1000000 # вес ребра до недостижимой вершины


# --------------генерация ориентированного графа----------------------------
edge_weight = [] # все возможные веса ребер графа

for i in range(max_edge_weight - min_edge_weight + 1):
  edge_weight.append(min_edge_weight + i)
  edge_weight.append(inf_edge_weight)

# print('edge_weight = ', edge_weight, '\n')
# print(len(edge_weight))

graph = []

for i in range(top_quantity): 
  for j in range(top_quantity): 
    edge = []
    if i == j:
      edge.append(i)
      edge.append(j)
      edge.append(0) # ребро графа - петля обратно в вершину
    else:
      edge.append(i)
      edge.append(j)
      edge.append(edge_weight[random.randint(0, len(edge_weight) - 1)])
    graph.append(edge)

print('graph = ', graph, '\n')
# --------------генерация первого поколения--------------------------------
population_1 = [] # популяция - набор особей поколения

for i in range(individual_quantity):
  individual = [] # особь характеризуется набором генов
  individual.append(start_top)
  for j in range(gene_quantity):  # генерация особи с произвольными генами из генофонда
    individual.append(random.randint(0, top_quantity - 1))
  individual.append(end_top)
  population_1.append(individual)

print('population_1 = ', population_1, '\n')
# --------------поиск длин путей в первом поколении-----------------
mass_lenght = [] # массив для хранения длин путей особей в данном поколении

for i in population_1: # перебор особей популяции первого поколения
  length = 0 # переменная для хранения длины пути каждой особи
  for j in range(gene_quantity + 1): # перебор генов особи, без учета последнего
    for k in graph: # поиск нужного веса ребра графа
      if (k[0] == i[j]) and (k[1] == i[j + 1]):
        length = length + k[2]
        break # так как нужное ребро графа найдено
  if  length < inf_edge_weight: # конечная вершина достижима
    individ = []
    individ.append(1) # номер поколения
    individ.append(i)
    individ.append(length)
    mass_lenght.append(individ)

# --------------поиск кратчайшего пути в первом поколении-----------------
min_lenght_array = [] # для поиска самого короткого пути из всех поколений

print('mass_lenght = ', mass_lenght)
if (mass_lenght != []): # хотя бы одна особь добралась до конечной вершины
  min_lenght = mass_lenght[0]
  for i in mass_lenght:
    if i[2] < min_lenght[2]:
      min_lenght = i
  min_lenght_array.append(min_lenght)
  print('min_lenght = ', min_lenght, '\n')
# ---------------------следующие поколения---------------------------------
for generation in range(generation_quantity - 1): # перебор поколений, первое поколение отдельно
  # --------------генерация поколения--------------------------------
  population = [] # популяция - набор особей поколения
  
  #for t in range(individual_quantity):
  father = []
  mother = []
  for k in population_1:
    if father == []:
      father = k
      continue
    if mother == []:
      mother = k
      #continue
    individual_1 = [] # ребенок № 1
    individual_2 = [] # ребенок № 2
    individual_1.append(start_top)
    individual_2.append(start_top)
    for j in range(gene_quantity):  # генерация особи с заданным количеством генов
      if j % 2 == 0:
        individual_1.append(father[j + 1]) # скрещивание особей, добавляем один ген предка - отца
        individual_2.append(father[j + 2])
      else:
        individual_1.append(mother[j]) # скрещивание особей, добавляем один ген предка - матери
        individual_2.append(mother[j + 1])
    individual_1.append(end_top)
    individual_2.append(end_top)
    # -------------------мутация гена-----------------------------
    individual_1[random.randint(1, gene_quantity)] = random.randint(0, top_quantity - 1) # присвоить произвольное значение гена из генофонда в произвольное место, за исключением начальной (start_top) и конечной (end_top) вершин-генов
    individual_2[random.randint(1, gene_quantity)] = random.randint(0, top_quantity - 1)
    
    population.append(individual_1)
    population.append(individual_2)
    father = []
    mother = []
  print('population №', generation + 2, ' =', population, '\n')
  
  # --------------поиск длин путей в поколении-----------------
  mass_lenght_new = [] # массив для хранения длин путей особей в данном поколении

  for i in population: # перебор особей поколения
    length = 0 # переменная для хранения длины пути каждой особи
    for j in range(gene_quantity + 1): # перебор генов особи, без учета последнего
      for k in graph: # поиск нужного веса ребра графа
        if (k[0] == i[j]) and (k[1] == i[j + 1]):
          length = length + k[2]
          break # так как нужное ребро графа найдено
    if  length < inf_edge_weight: # конечная вершина достижима
      individ = []
      individ.append(generation + 2) # номер поколения
      individ.append(i)
      individ.append(length)
      mass_lenght_new.append(individ)

  # --------------поиск кратчайшего пути в поколении-----------------
  print('mass_lenght_new = ', mass_lenght_new)
  if (mass_lenght_new != []): # хотя бы одна особь добралась до конечной вершины
    min_lenght = mass_lenght_new[0]
    for i in mass_lenght_new:
      if i[2] < min_lenght[2]:
        min_lenght = i
    min_lenght_array.append(min_lenght)
    print('min_lenght = ', min_lenght, '\n')
  
  population_1 = population # следующее поколение становится предком

# --------------поиск наилучшего пути из всех поколений-----------------
print('min_lenght_array = ', min_lenght_array, '\n')
if (min_lenght_array != []): # хотя бы один кратчайший путь найден
  the_best_way = min_lenght_array[0]
  for i in min_lenght_array:
    if i[2] < the_best_way[2]:
      the_best_way = i
  print('the_best_way = ', the_best_way, '\n')
