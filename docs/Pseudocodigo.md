#Pseudocodigo General del Sistema 

function askQuestion(texto):
    mostrar(texto + " (s/n): ")
    leer r
    return (minúscula(r) == 's')
end function

procedure main():
    mostrar("Sistema de Decisión de Estructuras de Datos")

    // 1. Grafos
    if askQuestion("¿Los datos representan relaciones complejas tipo red?") then
        showResult_Graph()
        return
    end if

    // 2. Árboles o Heap
    if askQuestion("¿Existe jerarquía o necesidad de ordenamiento rápido?") then
        
        if askQuestion("¿Necesitas acceso rápido al elemento de mayor prioridad?") then
            showResult_Heap()
        else
            if askQuestion("¿Te preocupa el desbalance del árbol?") then
                showResult_AVL()
            else
                showResult_BST()
            end if
        end if

        return
    end if

    // 3. Estructuras lineales estrictas (LIFO/FIFO)
    if askQuestion("¿El orden de inserción y eliminación es estricto?") then
        
        if askQuestion("¿El último en entrar debe salir primero (LIFO)?") then
            showResult_Stack()
        else
            showResult_Queue()
        end if

        return
    end if

    // 4. Almacenamiento lineal general
    if askQuestion("¿Conoces el tamaño y necesitas acceso por índice?") then
        showResult_Array()
    else
        if askQuestion("¿El recorrido debe ser cíclico?") then
            showResult_CircularLinkedList()
        else
            showResult_LinkedList()
        end if
    end if
end procedure
