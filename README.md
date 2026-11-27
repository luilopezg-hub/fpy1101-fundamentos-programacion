"""Sistema de gestión de vehículos de un concesionario (FPY1101 - Evaluación Parcial 4)."""


# Definimos funciones de menú

def mostrar_menu():
    print("\n========== MENÚ PRINCIPAL ==========")
    print("1. Agregar vehículo")
    print("2. Buscar vehículo")
    print("3. Eliminar vehículo")
    print("4. Actualizar disponibilidad")
    print("5. Mostrar vehículos")
    print("6. Salir")
    print("=====================================")


def leer_opcion():
    while True:
        texto = input("Seleccione una opción (1-6): ").strip()
        if texto.isdigit() and 1 <= int(texto) <= 6:
            return int(texto)
        print("Opción inválida. Debe ingresar un número entre 1 y 6.")


# Definimos funciones de validación (una responsabilidad cada una, sin mensajes)

def validar_modelo(modelo):
    return modelo.strip() != ""


def validar_anio(texto_anio):
    try:
        anio = int(texto_anio)
    except ValueError:
        return False
    return anio > 1900


def validar_precio(texto_precio):
    try:
        precio = float(texto_precio)
    except ValueError:
        return False
    return precio > 0

# Definimos funciones de operaciones sobre la lista

def agregar_vehiculo(lista_vehiculos):
    modelo = input("Modelo: ")
    if not validar_modelo(modelo):
        print("Error: el modelo no puede estar vacío ni contener solo espacios.")
        return

    anio_texto = input("Año: ")
    if not validar_anio(anio_texto):
        print("Error: el año debe ser un número entero mayor que 1900.")
        return

    precio_texto = input("Precio: ")
    if not validar_precio(precio_texto):
        print("Error: el precio debe ser un número decimal mayor que cero.")
        return

    vehiculo = {
        "modelo": modelo.strip(),
        "anio": int(anio_texto),
        "precio": float(precio_texto),
        "disponible": False,
    }
    lista_vehiculos.append(vehiculo)
    print("Vehículo agregado correctamente.")


def buscar_vehiculo(lista_vehiculos, modelo_buscado):
    for posicion in range(len(lista_vehiculos)):
        if lista_vehiculos[posicion]["modelo"] == modelo_buscado:
            return posicion
    return -1


def eliminar_vehiculo(lista_vehiculos):
    modelo = input("Modelo del vehículo a eliminar: ").strip()
    posicion = buscar_vehiculo(lista_vehiculos, modelo)
    if posicion != -1:
        lista_vehiculos.pop(posicion)
        print(f"Vehículo '{modelo}' eliminado correctamente.")
    else:
        print(f"El vehículo '{modelo}' no se encuentra registrado.")


def actualizar_disponibilidad(lista_vehiculos):
    for vehiculo in lista_vehiculos:
        if vehiculo["anio"] >= 2020:
            vehiculo["disponible"] = True
        else:
            vehiculo["disponible"] = False


def mostrar_vehiculos(lista_vehiculos):
    actualizar_disponibilidad(lista_vehiculos)
    print("\n=== LISTA DE VEHICULOS ===")
    for vehiculo in lista_vehiculos:
        print(f"Modelo: {vehiculo['modelo']}")
        print(f"Año: {vehiculo['anio']}")
        print(f"Precio: {vehiculo['precio']}")
        if vehiculo["disponible"]:
            print("Estado: DISPONIBLE")
        else:
            print("Estado: NO DISPONIBLE")
        print("*" * 45)

# Programa principal

def main():

# La lista de registros comienza vacía y vive solo dentro de main;
# se entrega como argumento a las funciones que la necesitan
    vehiculos = []
    opcion = 0

# repetimos el ciclo (permitiendo varias operaciones seguidas) hasta que el usuario elige la opción 6
    while opcion != 6:
        mostrar_menu()
        opcion = leer_opcion()

        if opcion == 1:
            agregar_vehiculo(vehiculos)
        elif opcion == 2:
         # main recibe la posición y decide qué mostrar según su valor
            modelo = input("Modelo a buscar: ").strip()
            posicion = buscar_vehiculo(vehiculos, modelo)
            if posicion != -1:
                vehiculo = vehiculos[posicion]
                print(f"Vehículo encontrado en la posición {posicion}:")
                print(f"Modelo: {vehiculo['modelo']}")
                print(f"Año: {vehiculo['anio']}")
                print(f"Precio: {vehiculo['precio']}")
                print(f"Disponible: {vehiculo['disponible']}")
            else:
                print(f"El vehículo '{modelo}' no se encuentra registrado.")
        elif opcion == 3:
            eliminar_vehiculo(vehiculos)
        elif opcion == 4:
            actualizar_disponibilidad(vehiculos)
            print("Disponibilidad actualizada.")
        elif opcion == 5:
            mostrar_vehiculos(vehiculos)
        elif opcion == 6:
            print("Gracias por usar el sistema. Vuelva Pronto")


if __name__ == "__main__":
    main()
    
