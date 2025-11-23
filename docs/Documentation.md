# Documentación del Sistema de Decisión de Estructuras de Datos

## 1. Objetivo del Sistema

El sistema implementado en C funciona como un **asistente interactivo** que guía al usuario a través de una serie de preguntas de Sí/No para recomendar la estructura de datos más adecuada entre:

- Array
- Linked List
- Circular Linked List
- Stack
- Queue
- Binary Search Tree 
- AVL Tree
- Max Heap
- Graph

El diseño del **cuestionario** y de la **lógica de decisión** está orientado a que, con pocas preguntas, se pueda descartar rápidamente grandes grupos de estructuras hasta llegar a la que mejor se ajusta al problema descrito por el usuario.

---

## 2. Justificación del Cuestionario

Las preguntas no están elegidas al azar: cada una separa el espacio de posibles soluciones en ramas lógicas, basadas en las propiedades y el comportamiento de las estructuras de datos.

###  Pregunta 1  
**¿Los datos representan relaciones complejas tipo red (conexiones múltiples entre elementos, como mapas o redes sociales)?**

- **Propósito:**  
  Distinguir entre problemas que pueden resolverse con estructuras **lineales o jerárquicas** (arrays, listas, árboles, etc.) y problemas que requieren modelar **relaciones N:M** (muchos a muchos).

- **Motivo de diseño:**  
  Si el usuario trabaja con mapas, redes sociales, grafos de rutas, etc., ninguna estructura lineal o de árbol describe bien la naturaleza del problema. El **Grafo** es la única estructura del curso que soporta nodos con múltiples conexiones en distintas direcciones.

- **Efecto en la decisión:**  
  - Si responde **“sí”**, el sistema termina inmediatamente y recomienda **Graph**.  
  - Si responde **“no”**, se descarta la rama de grafos y se pasa a analizar jerarquía/orden.

---

###  Pregunta 2  
**¿Los datos tienen una estructura jerárquica (padres/hijos) o requieren mantenerse ordenados para búsquedas rápidas?**

- **Propósito:**  
  Separar los casos que necesitan una **vista jerárquica u ordenada** de los que sólo necesitan una secuencia lineal.

- **Motivo de diseño:**  
  Si al usuario le interesa mantener los datos ordenados para búsquedas rápidas o tiene una relación clara de padre–hijo, las estructuras más adecuadas son los **árboles** o las estructuras derivadas de estos (BST, AVL, Heap).  
  Si no hay jerarquía ni necesidad de orden, se puede resolver con estructuras lineales.

- **Efecto en la decisión:**  
  - Si responde **“sí”**, se entra a la rama de **árboles y prioridad** (Preguntas 3 y 4).  
  - Si responde **“no”**, se pasa directamente a la rama de **estructuras lineales** (Preguntas 5–8).

---

###  Pregunta 3  
**(Si es jerárquico) ¿Necesitas acceder siempre al elemento de MAYOR prioridad o valor rápidamente (ej. colas de prioridad)?**

- **Propósito:**  
  Identificar problemas donde el elemento más importante (con mayor prioridad o valor) debe extraerse de forma rápida y repetida.

- **Motivo de diseño:**  
  En colas de prioridad y sistemas donde siempre se atiende primero al elemento “más grande” o “más urgente”, la estructura estándar es el **Max Heap**, que garantiza:

  - Acceso O(1) al máximo (en la raíz).  
  - Inserciones y eliminaciones en O(log n).

- **Efecto en la decisión:**  
  - Si responde **“sí”**, se recomienda **Max Heap**.  
  - Si responde **“no”**, se asume que se requiere orden, pero no solamente el máximo; entonces se pasa a distinguir entre **BST** y **AVL** en la Pregunta 4.

---

###  Pregunta 4  
**¿Te preocupa que el árbol se desbalancee y degrade el rendimiento (quieres O(log n) garantizado)?**

- **Propósito:**  
  Decidir entre un **árbol de búsqueda binaria simple (BST)** y un **árbol balanceado (AVL)**.

- **Motivo de diseño:**  
  - Un **BST** es más sencillo, pero si los datos se insertan en cierto orden (por ejemplo, crecientes), el árbol puede degenerar en una lista y las operaciones pasan de O(log n) a O(n).  
  - Un **AVL** mantiene el árbol balanceado mediante rotaciones, asegurando O(log n) incluso en el peor caso.

- **Efecto en la decisión:**  
  - Si responde **“sí”** → se recomienda **AVL**, priorizando rendimiento garantizado.  
  - Si responde **“no”** → se recomienda **BST**, priorizando simplicidad de implementación.

---

###  Pregunta 5  
**¿El orden de inserción y eliminación es estricto y limitado (solo por los extremos)?**

- **Propósito:**  
  Detectar si el patrón de acceso es restringido a los extremos de la estructura.

- **Motivo de diseño:**  
  Muchos problemas reales no requieren acceso arbitrario al elemento i-ésimo, sino que siguen reglas como:

  - **LIFO** → último en llegar, primero en salir.  
  - **FIFO** → primero en llegar, primero en salir.

  Estos patrones se modelan naturalmente con **Stack** y **Queue**.

- **Efecto en la decisión:**  
  - Si responde **“sí”**, se entra a la Pregunta 6 para decidir entre **Pila** o **Cola**.  
  - Si responde **“no”**, se pasa a analizar el tipo de almacenamiento lineal general en (Preguntas 7 y 8).

---

###  Pregunta 6  
**¿Necesitas que el ÚLTIMO elemento en entrar sea el PRIMERO en salir (Pila/LIFO)?**

- **Propósito:**  
  Diferenciar claramente entre **Stack** (LIFO) y **Queue** (FIFO).

- **Motivo de diseño:**  
  - En problemas de deshacer/rehacer, recursión, pila de llamadas, evaluadores de expresiones, el elemento más reciente es el primero en procesarse → **Stack**.  
  - En colas de procesos, atención a clientes, buffers, se respeta el orden de llegada → **Queue**.

- **Efecto en la decisión:**  
  - Si responde **“sí”** → se recomienda **Stack**.  
  - Si responde **“no”** → se recomienda **Queue**.

---

###  Pregunta 7  
**¿Conoces el tamaño exacto de datos y necesitas acceso rápido por índice (ej. dato[5])?**

- **Propósito:**  
  Decidir si conviene un **Array** (memoria contigua, tamaño fijo) o una estructura enlazada dinámica.

- **Motivo de diseño:**  
  Si el tamaño se conoce y no cambia mucho, y además se hace uso frecuente de acceso por índice, el **Array** ofrece:

  - Acceso O(1) por índice.  
  - Buena localidad de memoria.  
  - Menor sobrecarga por no usar punteros.

- **Efecto en la decisión:**  
  - Si responde **“sí”** → se recomienda **Array**.  
  - Si responde **“no”** → se considera que el tamaño debe ser dinámico y se pasa a la Pregunta 8 (listas enlazadas).

---

###  Pregunta 8  
**¿Los datos deben recorrerse en un ciclo continuo (el último conecta con el primero)?**

- **Propósito:**  
  Separar el uso de una **Linked List** normal de una **Circular Linked List**.

- **Motivo de diseño:**  
  En problemas como playlists, rondas por turnos, algoritmos de tipo “ronda circular”, se requiere que al terminar el último elemento se vuelva al primero de forma natural, lo que encaja con una **lista enlazada circular**.

- **Efecto en la decisión:**  
  - Si responde **“sí”** → se recomienda **Circular Linked List**.  
  - Si responde **“no”** → se recomienda **Linked List** simple.
