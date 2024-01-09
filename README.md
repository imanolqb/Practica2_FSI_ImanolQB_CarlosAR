<a href="https://www.eii.ulpgc.es" target="_blank"><img src="https://www.eii.ulpgc.es/sites/default/files/eii-acron-mod.png" alt="EII-ULPGC" align="right" width="516" height="150" /></a>
# PRÁCTICA 2 DE FSI
> - Redes neuronales aplicadas a clasificación de conjuntos de imágenes
> - Realizado por Carlos Alonso Rodríguez e Imanol Quintero Bermúdez

Esta práctica tiene como objetivo el desarrollo de una red neuronal efectiva para la clasificación de conjuntos de imágenes. Para lograrlo, se busca comprender y aplicar los conceptos esenciales de aprendizaje profundo, desde la selección adecuada de la arquitectura de red hasta la implementación de técnicas de preprocesamiento de datos. Se pretende entrenar la red utilizando un conjunto diverso de imágenes, permitiendo que el modelo aprenda a reconocer patrones y características distintivas en las diferentes clases de interés. Además, se busca optimizar los hiperparámetros del modelo y evaluar su rendimiento utilizando métricas pertinentes. Al finalizar la práctica, se espera no solo haber creado una red neuronal capaz de clasificar imágenes con precisión.

## Conjunto de imágenes elegido
El [dataset](https://www.kaggle.com/datasets/misrakahmed/vegetable-image-dataset) de imágenes escogido representa quince categorías distintas de verduras. El conjunto resulta ideal para nuestro cometido, pues cuenta con un gran número de fotografías, con una distribución que resulta ideal para el entrenamiento y aprendizaje de nuestra red, y que sigue, aproximadamente, la relación 70-20-10 (1000 imágenes en cada categoría del directorio “Training”, 200 en el directorio “Validation” y 200 en el directorio “Test”). Asimismo, se han evaluado los datos para comprobar que no siguen el mismo formato, como fondos blancos, que pueden resultar perjudiciales para el amaestramiento de la red.

## Ejecuciones de la red neuronal
Para poner en funcionamiento la red neuronal, se ha hecho uso de la web de procesamiento en línea [Kaggle](https://www.kaggle.com/), que ofrece distintas herramientas, tales como GPU, que resultan muy beneficiosas para los objetivos que planteamos (mayormente concurrencia), y librerías asociadas que ayudarán a aprovechar al máximo la gráfica.
Respecto al código propuesto por el profesor, se han cambiado finalmente varios hiperparámetros, como la convolución de las capas, los valores de ***Max Pooling***, y la capa ***Dense***. No obstante, a fin de mejorar el resultado, se ha tenido en cuenta el posible gasto de recursos adicional, así como el sobreajuste cada vez que se ha llevado a cabo alguna modificación, aunque esto último no ha significado un problema relevante, ya que el conjunto cuenta con una gran variedad de imágenes de entrenamiento.
No obstante, para validar los hiperparámetros elegidos, se han realizado diversas ejecuciones con distintos valores de hiperparámetros.
A continuación, se muestran los valores de precisión y la gráfica de pérdida y precisión obtenida para las diferentes combinaciones de hiperparámetros probados:

- 1ª ejecución, con capas convolutivas a 32, 64 y 128, *Max Pooling* a 2, *Dense* a 128:
  
- 2ª ejecución, con capas convolutivas a 32, 64 y 128, *Max Pooling* a 2, *Dense* a 128:
  
- 3ª ejecución, con capas convolutivas a 32, 64 y 128, *Max Pooling* a 2, *Dense* a 128:

- 4ª ejecución, con capas convolutivas a 32, 64 y 128, *Max Pooling* a 2, *Dense* a 128:

- 5ª ejecución, con capas convolutivas a 32, 64 y 128, *Max Pooling* a 2, *Dense* a 128:

- 6ª ejecución, con capas convolutivas a 32, 64 y 128, *Max Pooling* a 2, *Dense* a 128:

El proyecto consta de tres módulos principales:
- [utils.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/utils.py) : en este módulo se crean los métodos para las pilas LIFO y colas FIFO que usaremos para los algoritmos de búsqueda en anchura (BFS), en profundidad (DFS) y acotación y ramificación (Branch & Bound). En definitiva, cómo logramos extraer y extender en las listas a medida que generamos nodos.
- [search.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/search.py) : aquí se encuentra el algoritmo, que hará uso de todos los métodos contenidos en [utils.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/utils.py). También aquí, se hallan definidos los valores de las diferentes ciudades y las clases ***Problem*** y ***Node***.
- [run.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/run.py) : programa principal. Se ponen en marcha los programas de búsqueda, que se muestran como salida. Para realizar búsquedas con cada uno de los distintos algoritmos de búsqueda, ya sea BFS, DFS o Branch & Bound con y sin heurística, debemos definir en este módulo el problema, desde dónde queremos empezar hasta dónde queremos llegar, y que viene dado, en el módulo [search.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/search.py), por GPSProblem, sus atributos ***initial*** (nodo inicial) y ***goal*** (nodo objetivo), y los métodos ***sucessor*** (nodos hijo del padre), ***path_cost*** (coste desde el nodo inicial hasta el nodo actual) y ***h***, que define la heurística.

## Modificaciones realizadas en ***utils.py*** y ***search.py***
Para velar por el correcto funcionamiento de los algoritmos implementados, se han desarrollado en el módulo [utils.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/utils.py) las distintas listas y funciones derivadas según el tipo de procedimiento:
- Para la búsqueda en amplitud o Breadth-first search (BFS), se ha desarrollado la clase ***FIFOQueue***, de la que emanan las funciones ***extend*** y ***pop***. La particularidad del ***pop*** es que se extrae un elemento o nodo del principio de la lista, a semejanza de una cola FIFO.
- Para la búsqueda en profundidad o Depth-first search (DFS), se ha desarrollado la función ***Stack***, que devuelve una lista vacía. Las funciones que aplicamos sobre esa lista actúan de manera similar a una pila LIFO, pues el último elemento o nodo que se añade es el primero que se extrae.
- Para la ramificación y acotación o Branch and bound (B&B), se ha desarrollado la clase ***branchAndBoundQueue***, de la que emanan las funciones ***extend*** y ***pop***. La particularidad del ***extend*** es que se ordenan los elementos o nodos de menor a mayor coste de su ruta (desde el nodo inicial hasta él), y la función ***pop***, que actúa de manera análoga a la cola FIFO.
- Para la ramificación y acotación con subestimación o Branch and bound with heuristic (B&B with heuristic), se ha desarrollado la clase ***branchAndBoundQueueHeuristic***, de la que emanan las funciones ***extend***, ***pop*** y ***takeHeuristic***. La función ***takeHeuristic*** nos permite ordenar en ***extend*** los elementos y nodos por coste de ruta, sumado a su heurística, que es la distancia entre ese nodo y el nodo objetivo.

Por otra parte, también se ha dotado al módulo [search.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/utils.py) de funciones para la legibilidad de la búsqueda según los algoritmos en [run.py](https://github.com/imanolqb/Practica1_FSI_ImanolQB_CarlosAR/blob/master/code/run.py):
- ***breadth_first_graph_search***, para la búsqueda mediante BFS.
- ***depth_first_graph_search***, para la búsqueda mediante DFS.
- ***branch_and_bound***, para la búsqueda mediante Branch and Bound.
- ***branch_and_bound_with_heuristic***, para la búsqueda mediante Branch and Bound con subestimación.

Esto nos ayudará, en el programa principal, pasar como parámetro, únicamente, el problema al que nos enfrentamos, es decir, nodo inicial y nodo objetivo.

## Resultados esperados y obtenidos

Como prueba de la correcta ejecución del programa, hemos realizado la siguiente tabla en la que se comprueba los distintos resultados esperados y, finalmente, obtenidos.

<a href="https://www.dc.fi.udc.es/~cabalar/ai/ex1/index.html" target="_blank"><img src="https://www.dc.fi.udc.es/~cabalar/ai/ex1/romania-distances.jpg" alt="Romania" align="center" width="498" height="300" /></a>

*Figura con el mapa de la red de carreteras que cubre a Rumanía*

|  ID  |  Origen  |  Destino  |   Amplitud   |   Profundidad   |   Ramificación y acotación | Ramificación y acotación con subestimación |  Prueba de ejecución  |
|:----:|:--------:|:---------:|:------------:|:---------------:|:--------------------------:|:------------------------------------------:|:---------------------:|
| 1 |Arad|Bucharest|**Generados**: 21 <br> **Visitados**: 16 <br> **Costo total**: 450 <br> **Ruta**:[\<Node B>,\<Node F>,\<Node S>,\<Node A>]|**Generados**: 18 <br> **Visitados**: 10 <br> **Costo total**: 733 <br> **Ruta**:[\<Node B>,\<Node P>,\<Node C>,\<Node D>,\<Node M>,\<Node L>,\<Node T>,\<Node A>]|**Generados**: 31 <br> **Visitados**: 24 <br> **Costo total**: 418 <br> **Ruta**:\[<Node B>, \<Node P>, \<Node R>, \<Node S>, \<Node A>]|**Generados**: 16 <br> **Visitados**: 6 <br> **Costo total**: 418 <br> **Ruta**:[\<Node B>, \<Node P>, \<Node R>, \<Node S>, \<Node A>]|**Correcto**|
| 2 |Oradea|Eforie|**Generados**: 45 <br> **Visitados**: 43 <br> **Costo total**: 730 <br> **Ruta**:[\<Node E>, \<Node H>, \<Node U>, \<Node B>, \<Node F>, \<Node S>, \<Node O>]|**Generados**: 41 <br> **Visitados**: 31 <br> **Costo total**: 698 <br> **Ruta**:[\<Node E>, \<Node H>, \<Node U>, \<Node B>, \<Node P>, \<Node R>, \<Node S>, \<Node O>]|**Generados**: 43 <br> **Visitados**: 40 <br> **Costo total**: 698 <br> **Ruta**:[\<Node E>, \<Node H>, \<Node U>, \<Node B>, \<Node P>, \<Node R>, \<Node S>, \<Node O>]|**Generados**: 32 <br> **Visitados**: 15 <br> **Costo total**: 698 <br> **Ruta**:[\<Node E>, \<Node H>, \<Node U>, \<Node B>, \<Node P>, \<Node R>, \<Node S>, \<Node O>]|**Correcto**|
| 3 |Giurgiu|Zerind|**Generados**: 41 <br> **Visitados**: 34 <br> **Costo total**: 615 <br> **Ruta**:[\<Node Z>, \<Node A>, \<Node S>, \<Node F>, \<Node B>, \<Node G>]|**Generados**: 32 <br> **Visitados**: 21 <br> **Costo total**: 1284 <br> **Ruta**:[\<Node Z>, \<Node A>, \<Node T>, \<Node L>, \<Node M>, \<Node D>, \<Node C>, \<Node P>, \<Node R>, \<Node S>, \<Node F>, \<Node B>, \<Node G>]|**Generados**: 41 <br> **Visitados**: 35 <br> **Costo total**: 583 <br> **Ruta**:[\<Node Z>, \<Node A>, \<Node S>, \<Node R>, \<Node P>, \<Node B>, \<Node G>]|**Generados**: 26 <br> **Visitados**: 12 <br> **Costo total**: 583 <br> **Ruta**:[\<Node Z>, \<Node A>, \<Node S>, \<Node R>, \<Node P>, \<Node B>, \<Node G>]|**Correcto**|
| 4 |Neamt|Drobeta|**Generados**: 32 <br> **Visitados**: 26 <br> **Costo total**: 765 <br> **Ruta**:[\<Node D>, \<Node C>, \<Node P>, \<Node B>, \<Node U>, \<Node V>, \<Node I>, \<Node N>]|**Generados**: 31 <br> **Visitados**: 19 <br> **Costo total**: 1151 <br> **Ruta**:[\<Node D>, \<Node C>, \<Node P>, \<Node R>, \<Node S>, \<Node F>, \<Node B>, \<Node U>, \<Node V>, \<Node I>, \<Node N>]|**Generados**: 32 <br> **Visitados**: 26 <br> **Costo total**: 765 <br> **Ruta**:[\<Node D>, \<Node C>, \<Node P>, \<Node B>, \<Node U>, \<Node V>, \<Node I>, \<Node N>]|**Generados**: 23 <br> **Visitados**: 12 <br> **Costo total**: 765 <br> **Ruta**:[\<Node D>, \<Node C>, \<Node P>, \<Node B>, \<Node U>, \<Node V>, \<Node I>, \<Node N>]|**Correcto**|
| 5 |Mehadia|Fagaras|**Generados**: 31 <br> **Visitados**: 23 <br> **Costo total**: 520 <br> **Ruta**:[\<Node F>, \<Node S>, \<Node R>, \<Node C>, \<Node D>, \<Node M>]|**Generados**: 29 <br> **Visitados**: 18 <br> **Costo total**: 928 <br> **Ruta**:[\<Node F>, \<Node B>, \<Node P>, \<Node R>, \<Node S>, \<Node A>, \<Node T>, \<Node L>, \<Node M>]|**Generados**: 36 <br> **Visitados**: 27 <br> **Costo total**: 520 <br> **Ruta**:[\<Node F>, \<Node S>, \<Node R>, \<Node C>, \<Node D>, \<Node M>]|**Generados**: 25 <br> **Visitados**: 16 <br> **Costo total**: 520 <br> **Ruta**:[\<Node F>, \<Node S>, \<Node R>, \<Node C>, \<Node D>, \<Node M>]|**Correcto**|
