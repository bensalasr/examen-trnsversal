import random
import csv

trabajadores = ["Juan Pérez", 
                "María García", 
                "Carlos López", 
                "Ana Martínez", 
                "Pedro Rodríguez", 
                "Laura Hernández", 
                "Miguel Sánchez", 
                "Isabel Gómez", 
                "Francisco Díaz", 
                "Elena Fernández"]
sueldos = {}

def dar_sueldos_randoms(trabajadores):
    sueldos={trabajador:random.randint(300000,2500000) for trabajador in trabajadores}
    print("sueldos asignados")
    for trabajador,sueldo in sueldos.items():
        print(f"{trabajador}:{sueldo}")
    return sueldos

def clasificar_sueldos(sueldos):
    clasificacion={"menores a 800000":[],"entre 800000 y 2000000":[],"arriba de 2000000":[]}
    for trabajador,sueldo in sueldos.items():
        if sueldo < 800000:
            clasificacion["menores a 800000"].append((trabajador,sueldo))
        elif sueldo < 2000000:
            clasificacion["entre 800000 y 2000000"]
        else:
            clasificacion["arriba de 2000000"].append((trabajador,sueldo))
    print("clasificacion de sueldos:")
    for tipo,empleados in clasificacion.items():
        print(f"{tipo}{empleados}")
    print(f"total sueldos:{sum(sueldos.values())}")

def ver_estadisticas(sueldos):
    sueldo_mas_alto=max(sueldos.values())
    print(f"el sueldo mas alto es de : {sueldo_mas_alto}")
    sueldo_mas_bajo=min(sueldos.values())
    print(f"el sueldo mas bajo es de : {sueldo_mas_bajo}")
    sueldo_promedio=round(sum(sueldos.values())/len(sueldos),2)
    print(f"el sueldo promedio es de : {sueldo_promedio}")

    producto_sueldo=1
    for sueldo in sueldos.values():
        producto_sueldo *= sueldo
    media_geomtrica=round(producto_sueldo **(1.0/len(sueldos)),2)
    print(f"la media geometrica es de : {media_geomtrica}")

def reporte_de_sueldos(sueldos):
    with open('sueldos.csv','w',newline='') as archivo_csv:
        escritor_csv=csv.writer(archivo_csv,delimiter=",")
        escritor_csv.writerow(['nombre del empleado','sueldo base','descuento por salud','descuento por AFP','sueldo liquido'])
        for trabajador, sueldo in sueldos.items():
            descuento_afp=round(sueldo*0.12)
            descuento_salud=round(sueldo*0.07)
            sueldo_liquido=round(sueldo-descuento_afp-descuento_salud)
            escritor_csv.writerow([trabajador,round(sueldo,2),descuento_afp,descuento_salud,sueldo_liquido])
def menu():
    while True:
        print("menu examen \n1.asignar sueldos aleatorios\n2.clasificar sueldos \n3.ver estadisticas \n4.reporte de sueldo(exportar a csv) \n5.salir")
        opcion = input("seleccione una opcion ")
        if opcion=="1":
            sueldos=dar_sueldos_randoms(trabajadores)
        elif opcion=="2":
            if sueldos:
                clasificar_sueldos(sueldos)
            else:
                print("no hay sueldos asignados(escoja la primera opcion)")
        elif opcion=="3":
            if sueldos:
                 ver_estadisticas(sueldos)
            else:
                print("no hay sueldos asignados(escoja la primera opcion)")
        elif opcion=="4":
            if sueldos:
                reporte_de_sueldos(sueldos)
            else:
                print("no hay sueldos asignados(escoja la primera opcion)")
        elif opcion=="5":
            print("Finalizando programa... \nDesarrolado por Benjamin Salas \nRUT: 21.679.600-4")
        else:
            print("opcion invalida(escoja una opcion del 1 al 5)")
menu()
