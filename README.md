"""Sistema de gestión de vehículos de un concesionario (FPY1101 - Evaluación Parcial 4)."""


# Funciones de menú

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


# Funciones de validación (una responsabilidad cada una, sin mensajes)

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
