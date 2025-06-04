# Poyecto_estructura_de_datos
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

void menu() {
    int opcion;
    do {
        cout << "\n===== MENÚ DE GESTIÓN DE PROCESOS =====\n";
        cout << "1. Crear proceso\n";
        cout << "2. Cambiar estado de proceso\n";
        cout << "3. Agregar memoria a proceso (Push)\n";
        cout << "4. Mostrar todos los procesos\n";
        cout << "5. Salir\n";
        cout << "6. Eliminar proceso completamente\n";
        cout << "7. Liberar espacio de memoria\n";
        cout << "8. Quitar memoria a proceso (Pop)\n";
        cout << "Seleccione una opción: ";
        cin >> opcion;

        int id, cantidad, estadoNum, prioridadNum;
        string estado, prioridad;

        switch (opcion) {
            case 1:
                while (true) {
                    cout << "Estado:\n 1. listo\n 2. ejecutando\n 3. bloqueado\nSeleccione: ";
                    cin >> estadoNum;
                    estado = obtenerEstado(estadoNum);
                    if (estado == "invalido") {
                        cout << "ERROR, la opción que marcó no existe.\n";
                    } else {
                        break;
                    }
                }

                while (true) {
                    cout << "Prioridad:\n 1. Alta\n 2. Media\n 3. Baja\nSeleccione: ";
                    cin >> prioridadNum;
                    prioridad = obtenerPrioridad(prioridadNum);
                    if (prioridad == "invalida") {
                        cout << "ERROR, la opción que marcó no existe.\n";
                    } else {
                        break;
                    }
                }

                crearProceso(estado, prioridad);
                break;

            case 2:
                cout << "ID del proceso: ";
                cin >> id;
                if (!idExiste(id)) {
                    cout << "Proceso no encontrado.\n";
                    break;
                }

                while (true) {
                    cout << "Nuevo estado:\n 1. listo\n 2. ejecutando\n 3. bloqueado\nSeleccione: ";
                    cin >> estadoNum;
                    estado = obtenerEstado(estadoNum);
                    if (estado == "invalido") {
                        cout << "ERROR, la opción que marcó no existe.\n";
                    } else {
                        break;
                    }
                }
 cambiarEstado(id, estado);
                break;

            case 3:
                cout << "ID del proceso: ";
                cin >> id;
                if (!idExiste(id)) {
                    cout << "Proceso no encontrado.\n";
                    break;
                }
                cout << "Cantidad de memoria a apilar: ";
                cin >> cantidad;
                usarMemoria(id, cantidad);
                break;

            case 4:
                mostrarProcesos();
                break;

            case 5:
                cout << "Saliendo del sistema...\n";
                break;

            case 6:
                cout << "ID del proceso a eliminar: ";
                cin >> id;
                eliminarProceso(id);
                break;

            case 7:
                liberarEspacioMemoria();
                break;

            case 8:
                cout << "ID del proceso: ";
                cin >> id;
                if (!idExiste(id)) {
                    cout << "Proceso no encontrado.\n";
                    break;
                }
                cout << "Cantidad de memoria a desapilar: ";
                cin >> cantidad;
                quitarMemoria(id, cantidad);
                break;

            default:
                cout << "Opción inválida.\n";
        }
    } while (opcion != 5);
}

int main() {
    menu();
    return 0;
}
