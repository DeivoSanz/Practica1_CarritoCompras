# Calculos, Descuentos y generacion de Ticket encargado por: David Juarez Sanchez
def calcular_subtotal(carrito, catalogo):
    subtotal = 0.0
    for item in carrito:
        id_prod = item[0]
        cantidad = item[1]
        subtotal += catalogo[id_prod]["precio"] * cantidad
    return subtotal

def aplicar_descuento(subtotal, tipo_descuento):
    reglas = {"3x2": 0.33, "porcentaje": 0.10}
    
    if tipo_descuento in reglas:
        if tipo_descuento == "porcentaje":
            return subtotal - (subtotal * reglas["porcentaje"])
        elif tipo_descuento == "3x2":
            return subtotal - (subtotal * reglas["3x2"])
    return subtotal

import datetime

def generar_ticket(carrito, catalogo, total):
    folio = "F001"
    fecha = datetime.date.today().strftime("%Y-%m-%d")
    ticket = (folio, fecha, total)
    
    print("\n" + "="*30)
    print("       RESUMEN DE COMPRA       ")
    print("="*30)
    print(f"Folio: {ticket[0]}")
    print(f"Fecha: {ticket[1]}")
    print("-" * 30)
    
    for item in carrito:
        id_prod = item[0]
        cantidad = item[1]
        nombre = catalogo[id_prod]["nombre"]
        precio = catalogo[id_prod]["precio"]
        print(f"{nombre} x{cantidad} : ${precio * cantidad:.2f}")
        
    print("-" * 30)
    print(f"TOTAL A PAGAR: ${ticket[2]:.2f}")
    print("=" * 30)
    
    return ticket