# Shop
Mini_tienda
mini_tienda = {
    1: ["Mazanas", 5000.0, 25],
    2: ["Limones", 2300.0, 15],
    3: ["Peras", 2700.0, 33],
    4: ["Arandanos", 9300.0, 5],
    5: ["Totamates", 2100.0, 42],
    6: ["Fresas", 4100.0, 3],
    7: ["Helado", 4500.0, 41],
    8: ["Galletas", 500.0, 8],
    9: ["Chocolates", 3500.0, 80],
    10:["Jamon", 15000.0, 10]
}

global art_pre_may
global prod_menor

def calcular():
    precio_me = precio_menor(mini_tienda)
    precio_may = precio_mayor(mini_tienda)
    prom = promedio_precios(mini_tienda)
    valin = valor_inventario(mini_tienda)
    print(precio_may, precio_me, prom, valin)


def leer_datos():
    operacion = input()
    producto = input().split()
    producto[0] = int(producto[0])
    producto[2] = float(producto[2])
    producto[3] = int(producto[3])
    return operacion, producto


def precio_menor(mini_tienda):

    # precios = []
    # for i in tienda:
    #     precios.append(tienda[i][1])
    # minimo = min(precios)
    # posmin = 1 + precios.index(minimo)
    #
    # if tienda.get(posmin)[0] is not None:
    #     prod_menor: object = tienda.get(posmin)[0]
    # return prod_menor
    return min(mini_tienda.values(),key=lambda fila:fila[1])[0]



def precio_mayor(mini_tienda):

    # precios = []
    # for i in tienda:
    #     precios.append(tienda[i][1])
    # maximo = max(precios)
    # posmax = 1 + precios.index(maximo)
    #
    # if tienda.get(posmax)[0] is not None:
    #     art_pre_may: object = tienda.get(posmax)[0]
    # return art_pre_may
    return max(mini_tienda.values(), key=lambda fila: fila[1])[0]

def valor_inventario(mini_tienda):
    valor = 0
    for i in mini_tienda:
        valor += mini_tienda[i][1] * mini_tienda[i][2]
    return round(valor, 1)


def promedio_precios(mini_tienda):
    promedio = 0
    for i in mini_tienda:
        promedio += mini_tienda[i][1]
    promedio /= len(mini_tienda)
    return round(promedio, 1)


def agregar_producto(mini_tienda, producto: list):
    if producto[0] in mini_tienda:
        print("ERROR")
    else:
        codigo = producto[0]
        producto.pop(0)
        mini_tienda[codigo] = producto
        calcular()


def borrar_producto(mini_tienda: dict, producto: list):
    if producto[0] in mini_tienda:
        del mini_tienda[producto[0]]
        calcular()
    else:
        print("ERROR")


def actualizar_producto(mini_tienda: dict, producto: list):
    if producto[0] in mini_tienda:
        codigo = producto[0]
        mini_tienda[codigo] = producto
        producto.pop(0)
        calcular()
    else:
        print("ERROR")


def productos():
    operacion, producto = leer_datos()
    if operacion == 'AGREGAR':
        agregar_producto(mini_tienda, producto)
    elif operacion == 'BORRAR':
        borrar_producto(mini_tienda, producto)
    elif operacion == 'ACTUALIZAR':
        actualizar_producto(mini_tienda, producto)


productos()
