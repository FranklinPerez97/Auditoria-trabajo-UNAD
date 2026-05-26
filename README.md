# Auditoria-de-inventario-Unad
Herramineta para la auditoria de inventario, calculando que artículos necesitan ser reabastecidos y cuantas unidades quedan.
# ============================================================
#   SISTEMA DE AUDITORÍA DE INVENTARIO
# ============================================================
#   Columnas de la matriz:
#   [Código, Nombre, Stock Actual, Stock Mínimo Requerido]
# ============================================================

inventario = [
    ["A001", "Teclado Mecánico",      12,  20],
    ["A002", "Mouse Inalámbrico",     35,  15],
    ["A003", "Monitor 24 pulgadas",    3,  10],
    ["A004", "Cable HDMI 2m",          8,   8],
    ["A005", "Silla Ergonómica",       1,   25],
    ["A006", "Audífonos Bluetooth",   22,  30],
    ["A007", "Webcam Full HD",        14,  10], 
    ["A008", "Disco Duro Externo",     5,  12],
    ["A009", "Memoria RAM 16GB",       9,  20],
    ["A010", "Fuente de Poder 500W",   4,   10],
    ["A011", "Placa Base ATX",         2,   17],
    ["A012", "Procesador Intel i7",    6,  4]
]


# ──────────────────────────────────────────────────────────
# MÓDULO: calcular cantidad a pedir
# ──────────────────────────────────────────────────────────
def calcular_pedido(stock_actual, stock_minimo):
    """
    Determina cuántas unidades hay que pedir de un artículo.

    Parámetros:
        stock_actual  (int): Unidades disponibles actualmente.
        stock_minimo  (int): Mínimo de unidades requeridas.

    Retorna:
        int: Cantidad a pedir (0 si el stock es suficiente).
    """
    if stock_actual < stock_minimo:
        return stock_minimo - stock_actual
    return 0


# ──────────────────────────────────────────────────────────
# LÓGICA PRINCIPAL: generar lista de pedidos
# ──────────────────────────────────────────────────────────
def generar_lista_pedidos(inventario):
    """
    Recorre la matriz de inventario y devuelve
    los artículos que necesitan reabastecimiento.
    """
    pedidos = []
    for articulo in inventario:
        codigo, nombre, stock_actual, stock_minimo = articulo
        cantidad = calcular_pedido(stock_actual, stock_minimo)
        if cantidad > 0:
            pedidos.append((codigo, nombre, cantidad))
    return pedidos


# ──────────────────────────────────────────────────────────
# SALIDA: imprimir resultados
# ──────────────────────────────────────────────────────────
def imprimir_pedidos(pedidos):
    print("=" * 55)
    print("       LISTA DE PEDIDOS DE REABASTECIMIENTO")
    print("=" * 55)

    if not pedidos:
        print("Todo el inventario está en niveles óptimos.")
    else:
        print(f"  {'CÓDIGO':<8} {'ARTÍCULO':<25} {'CANT. A PEDIR':>12}")
        print("-" * 55)
        for codigo, nombre, cantidad in pedidos:
            print(f"  {codigo:<8} {nombre:<25} {cantidad:>10} ud.")

    print("=" * 55)
    print(f"  Total de artículos a reabastecer: {len(pedidos)}")
    print("=" * 55)


# ──────────────────────────────────────────────────────────
# PUNTO DE ENTRADA
# ──────────────────────────────────────────────────────────
if __name__ == "__main__":
    pedidos = generar_lista_pedidos(inventario)
    imprimir_pedidos(pedidos)