# Proyecto_estructura_de_datos
#include <iostream>
using namespace std;

struct Proceso {
    int id;
    string estado; // "listo", "ejecutando", "bloqueado"
    int prioridad;
    int memoria[100]; // pila de memoria simple (arreglo)
    int topeMemoria;
    Proceso* siguiente;
};

Proceso* cabeza = NULL;
int siguienteID = 1;

// Agregar proceso al final de la lista
void crearProceso(string estado, int prioridad) {
    Proceso* nuevo = new Proceso;
    nuevo->id = siguienteID++;
    nuevo->estado = estado;
    nuevo->prioridad = prioridad;
    nuevo->topeMemoria = -1;
    nuevo->siguiente = NULL;

    if (cabeza == NULL) {
        cabeza = nuevo;
    } else {
        Proceso* aux = cabeza;
        while (aux->siguiente != NULL) aux = aux->siguiente;
        aux->siguiente = nuevo;
    }
    cout << "Proceso creado con ID: " << nuevo->id << ", Estado: " << estado << endl;
}

