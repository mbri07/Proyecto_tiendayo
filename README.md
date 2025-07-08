#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<stdbool.h>

#define MAX_WORKERS 10
#define MAX_CLIENTS 10
#define MAX_SUPPLIERS 10
#define MAX_PRODUCT 1000

//STRUCTS
typedef struct{
    char nombre[60];
    int cedula;
    char tlf[20];
    char direc[60];
} Trabajador;

typedef struct{
    char nombre[60];
    int cedula;
    char tlf[20];
    char direc[60];
} Cliente;

typedef struct{
    char nombre[60];
    int cedula;
    char tlf[20];
    char direc[60];
} Proveedor;

typedef struct{
	int dia;
	int mes;
	int anio;
}Fecha;

typedef struct{
    char codigo[7];
	char nom[60];
	char desc[100];
	Fecha fecha_adquisicion; //DD-MM-AAAA
	int cantidad, ubi, categoria, tipo;
    float costo, precio_venta;
} Produc;

Produc producto[MAX_PRODUCT];
Trabajador trab[MAX_WORKERS];
Cliente clien[MAX_CLIENTS];
Proveedor prov[MAX_SUPPLIERS];
int num_productos = 0;
int num_clientes = 0;
int num_trabajadores = 0;
int num_facturas = 0;
int num_proveedores = 0;

float tasa_dolar = 108.98;
float tasa_euro = 129.20;
float tasa_peso = 36.87;

void mostrarMenuPrincipal();
void mostrarSubMenuReportes();
void menu_productos();
void menu_clientes();
void menu_trabajadores();
void menu_facturas();
void limpiar_buffer(); 
int leer_entero_positivo(const char *mensaje);
int leer_entero_no_negativo(const char *mensaje);
float leer_flotante_positivo(const char *mensaje);
bool validar_fecha(int dia, int mes, int anio);
void leer_producto(int cantidad_a_agregar);
void mostrar_producto();
void leer_trabajador(int cantidad_a_agregar);
void mostrar_trabajador();
void leer_cliente(int cantidad_a_agregar);
void mostrar_cliente();
void mostrar_proveedor();
void mostrar_productos_danados();
void modificar_trabajador();
int buscar_trabajador_por_cedula(int cedula_a_buscar);
void eliminar_trabajador();
void modificar_cliente();
int buscar_cliente_por_cedula(int cedula_a_buscar);
void eliminar_cliente();
void modificar_producto();
void eliminar_producto();
void mostrar_tipos_zapatos_vendidos();
int buscar_producto_por_codigo(const char *codigo_a_buscar);
void mostrar_productos_mas_vendidos();
void mostrar_clientes_con_compras();
void mostrar_ventas_diarias_por_tipo();
void mostrar_ultimas_facturas();

int main() {
	// Proveedor 1
    strcpy(prov[0].nombre, "Calzados Global S.A.");
    prov[0].cedula = 12132255;
    strcpy(prov[0].tlf, "0412-1234567");
    strcpy(prov[0].direc, "Av. Principal, Edif. Central, Caracas");

	// Proveedor 2
    strcpy(prov[1].nombre, "Suelas de Oro C.A.");
    prov[1].cedula = 13265847;
    strcpy(prov[1].tlf, "0212-9876543");
    strcpy(prov[1].direc, "Calle Miranda, Centro Comercial, Valencia");

    // Proveedor 3
    strcpy(prov[2].nombre, "Pieles y Diseños R.L.");
    prov[2].cedula = 11456236;
    strcpy(prov[2].tlf, "0414-7654321");
    strcpy(prov[2].direc, "Zona Industrial, Galpon 5, Maracay");

    num_proveedores = 3; 
    
    int opcion_principal;
    int opcion_reportes;
    int opcion;
    int cont;
    do {
        mostrarMenuPrincipal();
        printf("\nSeleccione una opcion: ");
        scanf("%d", &opcion_principal);
        limpiar_buffer();
        system("cls");
        
        switch (opcion_principal) {
            case 1:
                printf("\nHa seleccionado Inventario.\n");
                //funcion inventario 
                break;
            case 2:
                printf("\nHa seleccionado Productos.\n");
                
            do{
                menu_productos();
                printf("Seleccione una opcion: ");
                scanf("%d", &opcion);
                limpiar_buffer();
        
        	switch (opcion) {
            	case 1: 
				if (num_productos >= MAX_PRODUCT) {
        		printf("El sistema ya esta lleno, no se pueden cargar mas productos\n");
        		} else{
        		printf("Cuantos productos desea cargar al sistema?: ");
        		scanf("%d", &cont);
        		limpiar_buffer();    			
				leer_producto(cont);
				}
				break;
            	case 2: modificar_producto(); break;
            	case 3: eliminar_producto(); break;
            	case 4: mostrar_producto(); break;
            	case 0: break;
            	default: printf("Opcion invalida.\n");
            }
        	}while (opcion != 0);
                break;
            case 3:
                printf("\nHa seleccionado Clientes.\n");
            do{
                menu_clientes();
                printf("Seleccione una opcion: ");
        		scanf("%d", &opcion);
        		limpiar_buffer();
        	
        	switch (opcion) {
            	case 1: 
				if (num_productos >= MAX_CLIENTS) {
        		printf("El sistema ya esta lleno, no se pueden cargar mas clientes\n");
        		} else{
        		printf("Cuantos clientes desea cargar al sistema?: ");
        		scanf("%d", &cont);
        		limpiar_buffer();    			
				leer_cliente(cont);
				}
				break;
            	case 2: modificar_cliente(); break;
            	case 3: eliminar_cliente(); break;
            	case 4: mostrar_cliente(); break;
           	 	case 0: break;
            	default: printf("Opcion invalida.\n");
        		}
    		} while (opcion != 0);
    		
                break;
            case 4:
                printf("\nHa seleccionado Facturas.\n");
            do{
                menu_facturas();
                printf("Seleccione una opcion: ");
        	scanf("%d", &opcion);
        	limpiar_buffer();
        
        	switch (opcion) {
            	case 1: /*crear_factura();*/ break;
            	case 2: /*mostrar_facturas();*/ break;
           		case 0: break;
            	default: printf("Opcion invalida.\n");
        		}
    		} while (opcion != 0);
                //funcion facturas
                break;
            case 5:
                printf("\nHa seleccionado Trabajadores.\n");
            do{
                menu_trabajadores();
                printf("Seleccione una opcion: ");
                scanf("%d", &opcion);
                limpiar_buffer();
        
        	switch (opcion) {
            	case 1: 
				if (num_trabajadores >= MAX_WORKERS) {
        		printf("El sistema ya esta lleno, no se pueden cargar mas trabajadores\n");
        		} else{
        		printf("Cuantos trabajadores desea cargar al sistema?: ");
        		scanf("%d", &cont);
        		limpiar_buffer();    			
				leer_trabajador(cont);
				}
				break;
            	case 2: modificar_trabajador(); break;
            	case 3: eliminar_trabajador(); break;
            	case 4: mostrar_trabajador(); break;
            	case 0: break;
            	default: printf("Opcion invalida.\n");
        		}
    		} while (opcion != 0);
                //funcion trabajadores
                break;
            case 6: // Opcion para Reportes!
                do {
                    mostrarSubMenuReportes(); //submenu
                    printf("Seleccione una opcion de reporte: ");
                    scanf("%d", &opcion_reportes);
                    limpiar_buffer();

                    switch (opcion_reportes) {
                        // Opciones de INVENTARIO
                        case 1: printf("Inventario completo.\n"); break;
                        case 2: printf("Stock minimo.\n"); break;
                        case 3: printf("Productos danados.\n");  mostrar_productos_danados(); break;
                        // Opciones de VENTAS/PRODUCTOS
                        case 4: printf("Valor y costo.\n"); break;
                        case 5: printf("Tipos de zapato mas y menos vendidos.\n"); mostrar_tipos_zapatos_vendidos(); break;
            case 6: printf("Total ventas por tipo de zapato.\n"); break;
            case 7: mostrar_productos_mas_vendidos(); break;
            case 8: mostrar_ultimas_facturas (); break;
            // Opciones de CLIENTES/TRABAJADORES
            case 9: mostrar_clientes_con_compras(); break;
            case 10: printf("Cantidad de trabajadores.\n"); printf("El numero de trabajadores cargados en el sistema es de %d\n\n", num_trabajadores); break;
            case 11: printf("Proveedores.\n"); mostrar_proveedor(); break;
            // Opciones "Reportes" y "Salir" del submenu
            case 12: printf("Volviendo al menu principal...\n"); break;
            default: printf("Opcion de reporte no valida. Intente de nuevo.\n"); break;
        	}
        
        	if (opcion_reportes != 12) { 
            printf("Presione Enter para continuar...");
            while (getchar() != '\n'); 
            getchar();
        	}
   		 } while (opcion_reportes != 12);
    		break;
                
            case 7:
                printf("Saliendo del programa. Hasta pronto!\n");
                break;
                
            default:
                printf("Opcion no valida. Por favor, intente de nuevo.\n");
                break;
        }
        
        if (opcion_principal != 7 && opcion_principal != 6) { 
            printf("Presione Enter para continuar...");
            while (getchar() != '\n'); 
            
            getchar(); 
        }
    
	} while (opcion_principal != 7); 

    return 0;
	}
//FUNCIONES MENU Y SUBMENU
void mostrarMenuPrincipal() {
    printf("\n============ MENU PRINCIPAL ============\n");
    printf("1. Inventario\n");
    printf("2. Productos\n");
    printf("3. Clientes\n");
    printf("4. Facturas\n");
    printf("5. Trabajadores\n");
    printf("6. Reportes\n");
    printf("7. Salir\n");
    printf("========================================\n");
}

void mostrarSubMenuReportes() {
    printf("\n======== SUBMENU: REPORTES ========\n");
    printf("\n--- INVENTARIO ---\n");
    printf("1. Inventario completo\n");
    printf("2. Stock minimo\n");
    printf("3. Productos danados\n");
    printf("\n--- VENTAS/PRODUCTOS ---\n");
    printf("4. Valor y costo\n");
    printf("5. Tipos de zapato mas y menos vendidos\n");
    printf("6. Total ventas por tipo de zapato\n");
    printf("7. Productos mas vendidos\n");
    printf("8. Ultimas 7 facturas\n");
    printf("\n--- CLIENTES/TRABAJADORES ---\n");
    printf("9. Clientes que realizaron compras\n");
    printf("10. Cantidad de trabajadores\n");
    printf("11. Proveedores\n");
    printf("\n");
    printf("12. Volver al menu principal...\n");
    printf("========================================\n");
}

void menu_productos() {
        printf("\n--- MENU PRODUCTOS ---\n");
        printf("1. Agregar producto\n");
        printf("2. Modificar producto\n");
        printf("3. Eliminar producto\n");
        printf("4. Mostrar productos\n");
        printf("0. Volver al menu principal\n");
}

void menu_clientes() {
        printf("\n======== MENU CLIENTES ========\n");
        printf("1. Agregar cliente\n");
        printf("2. Modificar cliente\n");
        printf("3. Eliminar cliente\n");
        printf("4. Mostrar clientes\n");
        printf("0. Volver al menu principal\n");
        printf("====================================\n");
    }

void menu_trabajadores() {
        printf("\n======== MENU TRABAJADORES ========\n");
        printf("1. Agregar trabajador\n");
        printf("2. Modificar trabajador\n");
        printf("3. Eliminar trabajador\n");
        printf("4. Mostrar trabajadores\n");
        printf("0. Volver al menu principal\n");
        printf("====================================\n");
    }
 	
 	
 	void menu_facturas() {
    printf("\n======== MENU FACTURAS ========\n");
    printf("1. Crear factura\n");
    printf("2. Ver facturas\n");
    printf("0. Volver al menu principal\n");
    printf("====================================\n");
	}

// FUNCIONES CREAR, M0STRAR DATOS
void leer_producto(int cantidad_a_agregar){
	if (cantidad_a_agregar <= 0) {
        printf("Error: La cantidad de productos a agregar debe ser positiva.\n");
        return;
    }
    
    if ((num_productos + cantidad_a_agregar) > MAX_PRODUCT) {
        printf("Error: No se pueden agregar %d productos.", cantidad_a_agregar);
        return;
    }
    
	for(int i=0;i<cantidad_a_agregar;i++){
	 int j = num_productos + i;
	  printf("Ingrese el nombre del zapato\n");
	  fgets(producto[j].nom,sizeof(producto[j].nom),stdin);
	  producto[j].nom[strcspn(producto[j].nom,"\n")]='\0';
	  printf("Ingrese una descripcion para el producto: ");
	  fgets(producto[j].desc, sizeof(producto[j].desc), stdin);
      producto[j].desc[strcspn(producto[j].desc, "\n")] = '\0';
      
      do {
            printf("Ingrese el tipo de zapato:\n(1 para deportivo; 2 para casual; 3 para formal): ");
            scanf("%d", &producto[j].tipo);
            limpiar_buffer();
            if (producto[j].tipo < 1 || producto[j].tipo > 3) {
                printf("Opcion invalida. Por favor, ingrese 1, 2 o 3.\n");
            }
        } while (producto[j].tipo < 1 || producto[j].tipo > 3);
        
        do {
            printf("El producto tiene alguna condicion?\n(1 para buen estado; 2 para mal estado): ");
            scanf("%d", &producto[j].categoria);
            limpiar_buffer();
            if (producto[j].categoria < 1 || producto[j].categoria > 2) {
                printf("Opcion invalida. Por favor, ingrese 1 o 2.\n");
            }
        } while (producto[j].categoria < 1 || producto[j].categoria > 2);
		
        producto[j].cantidad = leer_entero_positivo("Ingrese la cantidad de este producto: ");
        printf("Ingrese el costo de adquisicion del producto: ");
        scanf("%f", &producto[j].costo);
        limpiar_buffer();
        printf("Ingrese el precio de venta del producto: ");
        scanf("%f", &producto[j].precio_venta);
        limpiar_buffer();
        
        printf("Ingrese la fecha adquisicion: \n");
        do {
            printf("Dia (1-31): ");
            scanf("%d", &producto[j].fecha_adquisicion.dia); 
            limpiar_buffer();
            printf("Mes (1-12): ");
            scanf("%d", &producto[j].fecha_adquisicion.mes);
            limpiar_buffer();
            printf("Anio: ");
            scanf("%d", &producto[j].fecha_adquisicion.anio); 
            limpiar_buffer();

            if (!validar_fecha(producto[j].fecha_adquisicion.dia, producto[j].fecha_adquisicion.mes, producto[j].fecha_adquisicion.anio)) {
                printf("Fecha invalida. Por favor, ingrese una fecha valida.\n");
            }
        } while (!validar_fecha(producto[j].fecha_adquisicion.dia, producto[j].fecha_adquisicion.mes, producto[j].fecha_adquisicion.anio));
        
        producto[j].codigo[0] = 'Z'; 
        switch(producto[j].tipo){
            case 1: producto[j].codigo[1] = '1'; break;
            case 2: producto[j].codigo[1] = '2'; break;
            case 3: producto[j].codigo[1] = '3'; break;
        }
        switch(producto[j].categoria){
            case 1: producto[j].codigo[2] = 'A'; break;
            case 2: producto[j].codigo[2] = 'B'; break;
        }
        
        if((j+1)<10){ // Si el numero es del 1 al 9
            producto[j].codigo[3]='0';
            producto[j].codigo[4]='0';
            producto[j].codigo[5]='0'+(j+1);
            producto[j].codigo[6]='\0';
        }else if((j+1)<100){ // Si el numero es del 10 al 99
            producto[j].codigo[3]='0';
            sprintf(&producto[j].codigo[4],"%d",j+1);
            producto[j].codigo[6]='\0';
        } else { // Si el numero es 100 o ms
            sprintf(&producto[j].codigo[3],"%d",j+1);
            producto[j].codigo[6] = '\0';
        }
        printf("Codigo generado para el producto: %s\n", producto[j].codigo);
    }
    num_productos += cantidad_a_agregar; 
    printf("\nSe agregaron %d producto(s) con exito!", cantidad_a_agregar);
}
    void mostrar_producto(){
    if (num_productos == 0) {
        printf("No hay productos registrados en el sistema.\n");
        return;
    }

    printf("\n--- LISTADO DE PRODUCTOS ---\n");
    printf("%-20s\t%-15s\t%-15s\t%-10s\t%-12s\t%-12s\t%-12s\t%-12s\t%-12s\t%-15s\t%-10s\n",
           "Nombre", "Tipo", "Condicion", "Cantidad", "Costo (BS)", "Venta (BS)",
           "Venta (USD)", "Venta (EUR)", "Venta (COP)", "Adquisicion", "Codigo");
    printf("------------------------------------------------------------------------------------------------------------------------------------------------------------------\n");

    for(int i = 0; i < num_productos; i++){
        printf("%-20s\t", producto[i].nom);

        switch(producto[i].tipo){
            case 1: printf("%-15s\t","Deportivo"); break;
            case 2: printf("%-15s\t","Casual"); break;
            case 3: printf("%-15s\t","Formal"); break;
            default: printf("%-15s\t","N/D"); break;
        }
        switch(producto[i].categoria){
            case 1: printf("%-15s\t","Buen estado"); break;
            case 2: printf("%-15s\t","Mal estado"); break;
            default: printf("%-15s\t","N/D"); break;
        }

        printf("%-10d\t", producto[i].cantidad);

        printf("%-12.2f\t%-12.2f\t",
               producto[i].costo, producto[i].precio_venta);

        printf("%-12.2f\t", producto[i].precio_venta / tasa_dolar);

        printf("%-12.2f\t", producto[i].precio_venta / tasa_euro);

        printf("%-12.2f\t", producto[i].precio_venta / tasa_peso);
 
        printf("%02d/%02d/%d\t",
               producto[i].fecha_adquisicion.dia,
               producto[i].fecha_adquisicion.mes,
               producto[i].fecha_adquisicion.anio);

        printf("%-10s\n", producto[i].codigo);
    }
    printf("------------------------------------------------------------------------------------------------------------------------------------------------------------------\n"); 
}

void leer_trabajador(int cantidad_a_agregar){
if (cantidad_a_agregar <= 0) {
        printf("Error: La cantidad de trabajadores a agregar debe ser positiva.\n");
        return;
    }
    
    if ((num_trabajadores + cantidad_a_agregar) > MAX_WORKERS) {
        printf("Error: No se pueden agregar %d trabajadores.\n", cantidad_a_agregar);
        return;
    }
    
   for(int i=0;i< cantidad_a_agregar;i++){
   	int j = num_trabajadores + i;
    printf("Ingrese el nombre del trabajador: ");
    fgets(trab[j].nombre,sizeof(trab[j].nombre),stdin);
    trab[j].nombre[strcspn(trab[j].nombre,"\n")]='\0';
    trab[j].cedula = leer_entero_positivo("Ingrese la C.I del trabajador: ");
    printf("Ingrese numero de telefono del trabajador: ");
    fgets(trab[j].tlf,sizeof(trab[j].tlf),stdin);
    trab[j].tlf[strcspn(trab[j].tlf,"\n")]='\0';
    printf("Ingrese la direccion del trabajador: ");
    fgets(trab[j].direc,sizeof(trab[j].direc),stdin);
    trab[j].direc[strcspn(trab[j].direc,"\n")]='\0';
   }
    num_trabajadores += cantidad_a_agregar;
    printf("\nSe agregaron %d trabajador(es) con exito!\n", cantidad_a_agregar);
}

void mostrar_trabajador() { 
    if (num_trabajadores == 0) {
        printf("\nNo hay trabajadores registrados en el sistema.\n");
        return;
    }
     printf("\n--- LISTADO DE TRABAJADORES ---\n");
    printf("%-5s\t%-20s\t%-10s\t%-20s\t%-30s\n", "Nro.", "Nombre", "Cedula", "Telefono", "Direccion");
    printf("--------------------------------------------------------------------------------------------------\n");

    for (int i = 0; i < num_trabajadores; i++) {
        printf("%-5d\t", i + 1); // nUmero de empleado (indice + 1)
        printf("%-20s\t%-10d\t%-20s\t%-30s\n",
               trab[i].nombre, trab[i].cedula, trab[i].tlf, trab[i].direc);
    }
    printf("--------------------------------------------------------------------------------------------------\n"); 
}

void leer_cliente(int cantidad_a_agregar){
	if (cantidad_a_agregar <= 0) {
        printf("Error: La cantidad de clientes a agregar debe ser positiva.\n");
        return;
    }
    if ((num_clientes + cantidad_a_agregar) > MAX_CLIENTS) {
        printf("Error: No se pueden agregar %d clientes.\n", cantidad_a_agregar);
        return;
    }
    for(int i=0;i<cantidad_a_agregar;i++){
    	int j = num_clientes + i;
    printf("Ingrese el nombre del cliente: ");
    fgets(clien[j].nombre,sizeof(clien[j].nombre),stdin);
     clien[j].nombre[strcspn(clien[j].nombre, "\n")] ='\0';
    clien[j].cedula = leer_entero_positivo("Ingrese la C.I del cliente: ");
    printf("Ingrese numero de telefono del cliente: ");
    fgets(clien[j].tlf,sizeof(clien[j].tlf),stdin);
    clien[j].tlf[strcspn(clien[j].tlf, "\n")]='\0';
    printf("Ingrese la direccion del cliente: ");
    fgets(clien[j].direc,sizeof(clien[j].direc),stdin);
    clien[j].direc[strcspn(clien[j].direc,"\n")]='\0';
   }
  	num_clientes += cantidad_a_agregar;
	printf("\nSe agregaron %d cliente(s) con exito! \n", cantidad_a_agregar);
}

void mostrar_cliente(){
	if(num_clientes == 0){
		printf("\nNo hay clientes registrados.\n");
		return;
	}
	printf("\n--- LISTADO DE CLIENTES ---\n");
     printf("%-20s\t%-15s\t%-20s\t%-30s\n", "Nombre", "Cedula", "Telefono", "Direccion");
     printf("----------------------------------------------------------------------------------\n");
    for (int i = 0; i < num_clientes;i++) {
         printf("%-20s\t%-15d\t%-20s\t%-30s\n", 
               clien[i].nombre,clien[i].cedula,clien[i].tlf,clien[i].direc);
}
printf("----------------------------------------------------------------------------------\n");
}

void mostrar_proveedor(){
	if (num_proveedores == 0) {
        printf("\nNo hay proveedores registrados en el sistema.\n");
        return;
    }
    printf("\n--- LISTADO DE PROVEEDORES ---\n");
    printf("%-20s\t%-10s\t%-20s\t%-30s\n", "Nombre", "Cedula", "Telefono", "Direccion");
    printf("----------------------------------------------------------------------------------\n");
    for (int i = 0; i < num_proveedores; i++) {
         printf("%-20s\t%-10d\t%-20s\t%-30s\n",
               prov[i].nombre, prov[i].cedula, prov[i].tlf, prov[i].direc);
	}
	printf("----------------------------------------------------------------------------------\n");
}

void mostrar_productos_danados(){
    if (num_productos == 0) {
        printf("\nNo hay productos registrados en el sistema para verificar su estado.\n");
        return;
    }

    printf("\n--- LISTADO DE PRODUCTOS DAÑADOS ---\n");
    printf("%-20s\t%-15s\t%-15s\t%-10s\t%-12s\t%-12s\t%-12s\t%-12s\t%-12s\t%-15s\t%-10s\n",
           "Nombre", "Tipo", "Condicion", "Cantidad", "Costo (VES)", "Venta (VES)",
           "Venta (USD)", "Venta (EUR)", "Venta (COP)", "Adquisicion", "Codigo");
    printf("------------------------------------------------------------------------------------------------------------------------------------------------------------------\n");

    int productos_encontrados = 0; 

    for(int i = 0; i < num_productos; i++){
        if (producto[i].categoria == 2) {
            productos_encontrados++;

            printf("%-20s\t", producto[i].nom);

            switch(producto[i].tipo){
                case 1: printf("%-15s\t","Deportivo"); break;
                case 2: printf("%-15s\t","Casual"); break;
                case 3: printf("%-15s\t","Formal"); break;
                default: printf("%-15s\t","N/D"); break;
            }
            switch(producto[i].categoria){
                case 1: printf("%-15s\t","Buen estado"); break;
                case 2: printf("%-15s\t","Mal estado"); break;
                default: printf("%-15s\t","N/D"); break;
            }

            printf("%-10d\t", producto[i].cantidad);
            printf("%-12.2f\t%-12.2f\t", producto[i].costo, producto[i].precio_venta);
            printf("%-12.2f\t", producto[i].precio_venta / tasa_dolar);
            printf("%-12.2f\t", producto[i].precio_venta / tasa_euro);
            printf("%-12.2f\t", producto[i].precio_venta / tasa_peso);

            printf("%02d/%02d/%d\t",
                   producto[i].fecha_adquisicion.dia,
                   producto[i].fecha_adquisicion.mes,
                   producto[i].fecha_adquisicion.anio);

            printf("%-10s\n", producto[i].codigo);
        }
    }
     if (productos_encontrados == 0) {
        printf("No se encontraron productos registrados en mal estado.\n");
    }
    printf("------------------------------------------------------------------------------------------------------------------------------------------------------------------\n");
}

// FUNCIONES MODIFICAR Y ELIMINAR DATOS
void modificar_trabajador(){
	if (num_trabajadores == 0) {
        printf("Actualmente no hay trabajadores registrados para modificar.\n");
        return;
    }
    int cedula_buscar;
    printf("\n--- Modificar Trabajador ---\n");
    cedula_buscar = leer_entero_positivo("Ingrese la cedula del trabajador a modificar: ");
    int indice = buscar_trabajador_por_cedula(cedula_buscar);
    if (indice == -1) {
        printf("Error: No se encontro un trabajador con la cedula %d.\n", cedula_buscar);
        return;
    }
            printf("Modificando trabajador: %s\n", trab[indice].nombre);
            
            printf("Nuevo nombre (actual: %s): ", trab[indice].nombre);
            fgets(trab[indice].nombre, sizeof(trab[indice].nombre), stdin);
            trab[indice].nombre[strcspn(trab[indice].nombre, "\n")] = '\0';
            
            printf("Nuevo telefono (actual: %s): ", trab[indice].tlf);
            fgets(trab[indice].tlf, sizeof(trab[indice].tlf), stdin);
            trab[indice].tlf[strcspn(trab[indice].tlf, "\n")] = '\0';
            
            printf("Nueva direccion (actual: %s): ", trab[indice].direc);
            fgets(trab[indice].direc, sizeof(trab[indice].direc), stdin);
            trab[indice].direc[strcspn(trab[indice].direc, "\n")] = '\0';
            
            printf("Trabajador modificado con exito\n");
    }

void eliminar_trabajador(){
	printf("\n--- Eliminar trabajador ---\n");
	if (num_trabajadores == 0) {
        printf("Actualmente no hay trabajadores registrados para eliminar.\n");
        return;
    }

    int cedula_a_eliminar;
    cedula_a_eliminar = leer_entero_positivo("Ingrese la cedula del trabajador que desea eliminar: ");
    int indice = buscar_trabajador_por_cedula(cedula_a_eliminar);

    if (indice == -1) {
        printf("Error: No se encontro un trabajador con la cedula %d.\n", cedula_a_eliminar);
        return;
    }

    printf("\nTrabajador encontrado. Se eliminaran los siguientes datos:\n");
    printf("  Nombre: %s\n", trab[indice].nombre);
    printf("  Cedula: %d\n", trab[indice].cedula);
    printf("  Telefono: %s\n", trab[indice].tlf);
    printf("  Direccion: %s\n", trab[indice].direc);

    char confirmacion;
    printf("Esta completamente seguro de que desea eliminar a este trabajador? (S/N): ");
    // El espacio antes de %c es importante para consumir cualquier caracter de nueva linea
    // que haya quedado en el buffer de entrada de una lectura anterior (ej. de leer_entero_positivo)
    scanf(" %c", &confirmacion); 

    if (confirmacion == 'S' || confirmacion == 's') {
        //  eliminar el elemento es pq se mueven todos los elementos desde la posicion siguiente
        // una posicion hacia atras, sobrescribiendo el elemento actual
        for (int i = indice; i < num_trabajadores - 1; i++) {
            trab[i] = trab[i+1]; 
        }
        num_trabajadores--; 
        printf("Trabajador eliminado con exito!\n");
    } else {
        printf("Eliminacion cancelada. El trabajador no ha sido removido.\n");
    }
    }
	void modificar_cliente(){
	if (num_clientes == 0) {
        printf("Actualmente no hay clientes registrados para modificar.\n");
        return;
    }
    int cedula_buscar;
    printf("\n--- Modificar Cliente ---\n");
    cedula_buscar = leer_entero_positivo("Ingrese la cedula del cliente que desea modificar: ");
    int indice = buscar_cliente_por_cedula(cedula_buscar);
    if (indice == -1) {
        printf("Error: No se encontro un cliente con la cedula %d.\n", cedula_buscar);
        return;
    }
            printf("Modificando cliente: %s\n", clien[indice].nombre);
            
            printf("Nuevo nombre (actual: %s): ", clien[indice].nombre);
            fgets(clien[indice].nombre, sizeof(clien[indice].nombre), stdin);
            clien[indice].nombre[strcspn(clien[indice].nombre, "\n")] = '\0';
            
            printf("Nuevo telefono (actual: %s): ", clien[indice].tlf);
            fgets(clien[indice].tlf, sizeof(clien[indice].tlf), stdin);
            clien[indice].tlf[strcspn(clien[indice].tlf, "\n")] = '\0';
            
            printf("Nueva direccion (actual: %s): ", clien[indice].direc);
            fgets(clien[indice].direc, sizeof(clien[indice].direc), stdin);
            clien[indice].direc[strcspn(clien[indice].direc, "\n")] = '\0';
            
            printf("Cliente modificado con exito\n");
	}

	void eliminar_cliente(){
	printf("\n--- Eliminar Cliente ---\n");
	if (num_clientes == 0) {
        printf("Actualmente no hay clientes registrados para eliminar.\n");
        return;
    }

    int cedula_a_eliminar;
    cedula_a_eliminar = leer_entero_positivo("Ingrese la cedula del clientes que desea eliminar: ");
    int indice = buscar_cliente_por_cedula(cedula_a_eliminar);

    if (indice == -1) {
        printf("Error: No se encontro un cliente con la cedula %d.\n", cedula_a_eliminar);
        return;
    }

    printf("\nCliente encontrado. Se eliminaran los siguientes datos:\n");
    printf("  Nombre: %s\n", clien[indice].nombre);
    printf("  Cedula: %d\n", clien[indice].cedula);
    printf("  Telefono: %s\n", clien[indice].tlf);
    printf("  Direccion: %s\n", clien[indice].direc);

    char confirmacion;
    printf("ï¿½Esta completamente seguro de que desea eliminar a este cliente? (S/N): ");
    
    scanf(" %c", &confirmacion); 

    if (confirmacion == 'S' || confirmacion == 's') {
        for (int i = indice; i < num_clientes - 1; i++) {
            clien[i] = clien[i+1]; 
        }
        num_clientes--; 
        printf("Cliente eliminado con exito!\n");
    } else {
        printf("Eliminacion cancelada. El cliente no ha sido removido.\n");
    }
}

	void modificar_producto(){
		if (num_productos == 0) {
        printf("Actualmente no hay productos registrados para modificar.\n");
        return;
    }
     char codigo_buscar[7];
      printf("Ingrese el codigo del producto a modificar: ");
    fgets(codigo_buscar, sizeof(codigo_buscar), stdin);
    codigo_buscar[strcspn(codigo_buscar, "\n")] = '\0';
    limpiar_buffer();
    printf("\n--- Modificar Producto ---\n");
    int indice = buscar_producto_por_codigo(codigo_buscar);
    if (indice == -1) {
         printf("Error: No se encontro un producto con el codigo '%s'.\n", codigo_buscar);
        return;
    }
            printf("Modificando Producto: %s\n", producto[indice].nom);
            
        printf("  Nuevo nombre (actual: %s): ", producto[indice].nom);
    	fgets(producto[indice].nom, sizeof(producto[indice].nom), stdin);
    	producto[indice].nom[strcspn(producto[indice].nom, "\n")] = '\0';
        printf("  Nueva descripcion (actual: %s): ", producto[indice].desc);
    	fgets(producto[indice].desc, sizeof(producto[indice].desc), stdin);
   		producto[indice].desc[strcspn(producto[indice].desc, "\n")] = '\0';
    	do {
        printf("  Nuevo tipo (actual: %d - 1: Deportivo, 2: Casual, 3: Formal): ", producto[indice].tipo);
        scanf("%d", &producto[indice].tipo);
        limpiar_buffer();
        if (producto[indice].tipo < 1 || producto[indice].tipo > 3) {
            printf("Opcion invalida. Por favor, ingrese 1, 2 o 3.\n");
        }
    	} while (producto[indice].tipo < 1 || producto[indice].tipo > 3);
		do {
        printf("  Nueva categoria (actual: %d - 1: Buen estado, 2: Mal estado): ", producto[indice].categoria);
        scanf("%d", &producto[indice].categoria);
        limpiar_buffer();
        if (producto[indice].categoria < 1 || producto[indice].categoria > 2) {
            printf("Opcion invalida. Por favor, ingrese 1 o 2.\n");
        }
    	} while (producto[indice].categoria < 1 || producto[indice].categoria > 2);
		printf("  Nueva cantidad (actual: %d): ", producto[indice].cantidad);
    	producto[indice].cantidad = leer_entero_no_negativo("Ingrese la nueva cantidad: ");
		printf("  Nuevo costo (actual: %.2f): ", producto[indice].costo);
    	producto[indice].costo = leer_flotante_positivo("Ingrese el nuevo costo: ");
 		printf("  Nuevo precio de venta (actual: %.2f): ", producto[indice].precio_venta);
    	producto[indice].precio_venta = leer_flotante_positivo("Ingrese el nuevo precio de venta: ");
	
    printf("  Nueva fecha de adquisicion (actual: %02d/%02d/%d):\n",
           producto[indice].fecha_adquisicion.dia,
           producto[indice].fecha_adquisicion.mes,
           producto[indice].fecha_adquisicion.anio);
    do {
        printf("    Dia (1-31): ");
        scanf("%d", &producto[indice].fecha_adquisicion.dia);
        limpiar_buffer();
        printf("    Mes (1-12): ");
        scanf("%d", &producto[indice].fecha_adquisicion.mes);
        limpiar_buffer();
        printf("    Anio: ");
        scanf("%d", &producto[indice].fecha_adquisicion.anio);
        limpiar_buffer();

        if (!validar_fecha(producto[indice].fecha_adquisicion.dia, producto[indice].fecha_adquisicion.mes, producto[indice].fecha_adquisicion.anio)) {
            printf("Fecha invalida. Por favor, ingrese una fecha valida.\n");
        }
    } while (!validar_fecha(producto[indice].fecha_adquisicion.dia, producto[indice].fecha_adquisicion.mes, producto[indice].fecha_adquisicion.anio));

    char temp_codigo[7]; 
    temp_codigo[0] = 'Z';
    
    switch(producto[indice].tipo){
        case 1: temp_codigo[1] = '1'; break;
        case 2: temp_codigo[1] = '2'; break;
        case 3: temp_codigo[1] = '3'; break;
    }
    switch(producto[indice].categoria){
        case 1: temp_codigo[2] = 'A'; break;
        case 2: temp_codigo[2] = 'B'; break;
    }
    if((indice+1)<10){ 
        temp_codigo[3]='0';
        temp_codigo[4]='0';
        temp_codigo[5]='0'+(indice+1);
        temp_codigo[6]='\0';
    }else if((indice+1)<100){ 
        temp_codigo[3]='0';
        sprintf(&temp_codigo[4],"%d",indice+1);
        temp_codigo[6]='\0';
    } else { 
        sprintf(&temp_codigo[3],"%d",indice+1);
        temp_codigo[6] = '\0';
    }
    strcpy(producto[indice].codigo, temp_codigo); 

    printf("Producto modificado con exito. Nuevo codigo: %s\n", producto[indice].codigo);
	}
	
	void eliminar_producto(){
	printf("\n--- Eliminar Producto ---\n");
	if (num_productos == 0) {
        printf("Actualmente no hay productos registrados para eliminar.\n");
        return;
    }

    char codigo_a_eliminar[7];
    
	printf("Ingrese el codigo del producto que desea eliminar: ");
    fgets(codigo_a_eliminar, sizeof(codigo_a_eliminar), stdin);
    codigo_a_eliminar[strcspn(codigo_a_eliminar, "\n")] = '\0';

    int indice = buscar_producto_por_codigo(codigo_a_eliminar); 

    if (indice == -1) {
        printf("Error: No se encontro un producto con el codigo '%s'.\n", codigo_a_eliminar);
        return;
    }

    printf("\nProducto encontrado. Se eliminaran los siguientes datos:\n");
    printf("  Codigo: %s\n", producto[indice].codigo);
    printf("  Nombre: %s\n", producto[indice].nom);
    printf("  Descripcion: %s\n", producto[indice].desc);
    printf("  Cantidad: %d\n", producto[indice].cantidad);
    printf("  Precio de Venta: %.2f\n", producto[indice].precio_venta);
    printf("  Fecha de Adquisicion: %02d/%02d/%d\n",
       producto[indice].fecha_adquisicion.dia,
       producto[indice].fecha_adquisicion.mes,
       producto[indice].fecha_adquisicion.anio);

    char confirmacion;
    printf("Esta completamente seguro de que desea eliminar este producto? (S/N): ");
    scanf(" %c", &confirmacion); 

    if (confirmacion == 'S' || confirmacion == 's') {
        for (int i = indice; i < num_productos - 1; i++) {
            producto[i] = producto[i+1];
        }
        num_productos--;
        printf("Producto eliminado con exito!\n");
    } else {
        printf("Eliminacion cancelada. El producto no ha sido removido.\n");
    }
}

void limpiar_buffer() {
    int c;
    while ((c = getchar()) != '\n' && c != EOF);
}

int buscar_trabajador_por_cedula(int cedula_a_buscar) {
    for (int i = 0; i < num_trabajadores; i++) {
        if (trab[i].cedula == cedula_a_buscar) {
            return i; 
        }
    }
    return -1; 
}


int buscar_cliente_por_cedula(int cedula_a_buscar) {
    for (int i = 0; i < num_clientes; i++) {
        if (clien[i].cedula == cedula_a_buscar) {
            return i; 
        }
    }
    return -1;
}

int buscar_producto_por_codigo(const char *codigo_a_buscar) {
    for (int i = 0; i < num_productos; i++) {
        if (strcmp(producto[i].codigo, codigo_a_buscar) == 0) {
            return i;
        }
    }
    return -1;
}

int leer_entero_positivo(const char *mensaje) { 
    int valor;
    int lectura;
    do {
        printf("%s", mensaje);
        lectura = scanf("%d", &valor);
        limpiar_buffer();
        
        if (lectura != 1) {
            printf("Error: Ingrese numeros enteros.\n");
            limpiar_buffer();
        } else if (valor <= 0){
			printf("Error: Ingrese un numero positivo mayor que cero.\n");
			limpiar_buffer();
        }
		} while (lectura != 1 || valor <= 0);
    return valor;
}

int leer_entero_no_negativo(const char *mensaje) {
    int valor;
    int lectura;
    do {
        printf("%s", mensaje);
        lectura = scanf("%d", &valor); 
        limpiar_buffer(); 

        if (lectura != 1) { 
            printf("Error: Por favor, ingrese un numero entero valido.\n");
        } else if (valor < 0) { 
            printf("Error: Ingrese un numero entero que sea cero o positivo.\n");
        }
    } while (lectura != 1 || valor < 0); 
    return valor;
}

float leer_flotante_positivo(const char *mensaje){
    float valor;
    int lectura;
    do {
        printf("%s", mensaje);
        lectura = scanf("%f", &valor); 
        limpiar_buffer(); 

        if (lectura != 1) {
            printf("Error: Por favor, ingrese un numero decimal valido.\n");
        } else if (valor <= 0) {
            printf("Error: Ingrese un numero positivo mayor que cero.\n"); 
        }
    } while (lectura != 1 || valor <= 0);
    return valor;
}

  bool validar_fecha(int dia, int mes, int anio) {
    if (anio < 1900 || anio > 2025) { 
        return false;
    }
    if (mes < 1 || mes > 12) {
        return false;
    }
    if (dia < 1 || dia > 31) {
        return false;
    }
    int dias_en_mes[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    if ((anio % 400 == 0) || (anio % 4 == 0 && anio % 100 != 0)) {
        dias_en_mes[2] = 29;
    }
    if (dia > dias_en_mes[mes]) {
        return false;
    }
    return true;
}

void mostrar_clientes_con_compras() {
    if (num_facturas == 0) {
        printf("No hay facturas registradas. No se pueden mostrar clientes con compras.\n");
        return;
    }

    int clientes_con_compras[MAX_CLIENTS] = {0};
    float total_compras[MAX_CLIENTS] = {0};
    int num_compras[MAX_CLIENTS] = {0};

    // Recorrer facturas para identificar clientes
    for (int i = 0; i < num_facturas; i++) {
        int indice_cliente = buscar_cliente_por_cedula(facturas[i].cedula_cliente);
        if (indice_cliente != -1) {
            clientes_con_compras[indice_cliente] = 1;
            total_compras[indice_cliente] += facturas[i].total;
            num_compras[indice_cliente]++;
        }
    }

    printf("\n=== CLIENTES QUE REALIZARON COMPRAS ===\n");
    printf("%-30s %-15s %-10s %-15s %-15s\n", "NOMBRE", "CEDULA", "COMPRAS", "TOTAL BS", "PROMEDIO BS");
    printf("---------------------------------------------------------------------------\n");

    int clientes_mostrados = 0;
    for (int i = 0; i < num_clientes; i++) {
        if (clientes_con_compras[i]) {
            float promedio = total_compras[i] / num_compras[i];
            printf("%-30s %-15d %-10d %-15.2f %-15.2f\n", 
                   clien[i].nombre, clien[i].cedula, 
                   num_compras[i], total_compras[i], promedio);
            clientes_mostrados++;
        }
    }

    if (clientes_mostrados == 0) {
        printf("No se encontraron clientes con compras registradas.\n");
    }
    printf("---------------------------------------------------------------------------\n");
}

void mostrar_productos_mas_vendidos() {
    if (num_facturas == 0) {
        printf("No hay facturas registradas para generar reportes.\n");
        return;
    }

    int cantidad_vendida[MAX_PRODUCT] = {0};
    
    for (int i = 0; i < num_facturas; i++) {
        for (int j = 0; j < facturas[i].num_items; j++) {
            ItemFactura item = facturas[i].items[j];
            int indice_producto = buscar_producto_por_codigo(item.codigo_producto);
            if (indice_producto != -1) {
                cantidad_vendida[indice_producto] += item.cantidad;
            }
        }
    }

    int indices_ordenados[MAX_PRODUCT];
    for (int i = 0; i < num_productos; i++) {
        indices_ordenados[i] = i;
    }

    for (int i = 0; i < num_productos - 1; i++) {
        for (int j = 0; j < num_productos - i - 1; j++) {
            if (cantidad_vendida[indices_ordenados[j]] < cantidad_vendida[indices_ordenados[j + 1]]) {
                int temp = indices_ordenados[j];
                indices_ordenados[j] = indices_ordenados[j + 1];
                indices_ordenados[j + 1] = temp;
            }
        }
    }

    printf("\n=== PRODUCTOS MAS VENDIDOS ===\n");
    printf("%-10s %-30s %-15s %-10s %-10s\n", "CODIGO", "NOMBRE", "TIPO", "VENDIDOS", "STOCK");
    printf("------------------------------------------------------------------\n");

    int max_a_mostrar = (num_productos > 10) ? 10 : num_productos;
    for (int i = 0; i < max_a_mostrar; i++) {
        int indice = indices_ordenados[i];
        if (cantidad_vendida[indice] == 0) break; // No mostrar productos no vendidos
        
        printf("%-10s %-30s ", producto[indice].codigo, producto[indice].nom);
        
        // Mostrar tipo de zapato
        switch(producto[indice].tipo) {
            case 1: printf("%-15s ", "Deportivo"); break;
            case 2: printf("%-15s ", "Casual"); break;
            case 3: printf("%-15s ", "Formal"); break;
            default: printf("%-15s ", "Desconocido"); break;
        }
        
        printf("%-10d %-10d\n", cantidad_vendida[indice], producto[indice].cantidad);
    }
    printf("------------------------------------------------------------------\n");
}

void mostrar_tipos_zapatos_vendidos() {
    if (num_facturas == 0) {
        printf("No hay facturas registradas para generar reportes.\n");
        return;
    }

    int cantidad_por_tipo[4] = {0}; // Índices 1-3 para los tipos de zapatos
    float monto_por_tipo[4] = {0};

    // Recorrer todas las facturas y sus items
    for (int i = 0; i < num_facturas; i++) {
        for (int j = 0; j < facturas[i].num_items; j++) {
            ItemFactura item = facturas[i].items[j];
            int indice_producto = buscar_producto_por_codigo(item.codigo_producto);
            if (indice_producto != -1) {
                int tipo = producto[indice_producto].tipo;
                if (tipo >= 1 && tipo <= 3) {
                    cantidad_por_tipo[tipo] += item.cantidad;
                    monto_por_tipo[tipo] += item.subtotal;
                }
            }
        }
    }

    // Determinar el tipo más y menos vendido
    int tipo_mas_vendido = 0;
    int tipo_menos_vendido = 0;
    int max_vendidos = -1;
    int min_vendidos = -1;

    for (int i = 1; i <= 3; i++) {
        if (cantidad_por_tipo[i] > 0) {
            if (max_vendidos == -1 || cantidad_por_tipo[i] > max_vendidos) {
                max_vendidos = cantidad_por_tipo[i];
                tipo_mas_vendido = i;
            }
            if (min_vendidos == -1 || cantidad_por_tipo[i] < min_vendidos) {
                min_vendidos = cantidad_por_tipo[i];
                tipo_menos_vendido = i;
            }
        }
    }

    // Mostrar resultados
    printf("\n=== REPORTE POR TIPO DE ZAPATO ===\n");
    printf("%-15s %-15s %-15s\n", "TIPO", "CANTIDAD", "MONTO TOTAL (Bs)");
    printf("--------------------------------------------\n");

    for (int i = 1; i <= 3; i++) {
        char* nombre_tipo = "";
        switch(i) {
            case 1: nombre_tipo = "Deportivo"; break;
            case 2: nombre_tipo = "Casual"; break;
            case 3: nombre_tipo = "Formal"; break;
        }
        
        printf("%-15s %-15d %-15.2f", nombre_tipo, cantidad_por_tipo[i], monto_por_tipo[i]);
        
        if (i == tipo_mas_vendido) {
            printf(" (MÁS VENDIDO)");
        } else if (i == tipo_menos_vendido && max_vendidos != min_vendidos) {
            printf(" (MENOS VENDIDO)");
        }
        
        printf("\n");
    }
    
    printf("--------------------------------------------\n");
}

void mostrar_ventas_diarias_por_tipo() {
    if (num_facturas == 0) {
        printf("No hay facturas registradas para generar reportes.\n");
        return;
    }

    // Pedir fecha para el reporte
    Fecha fecha_reporte;
    printf("\nIngrese la fecha para el reporte de ventas:\n");
    do {
        printf("Dia (1-31): ");
        scanf("%d", &fecha_reporte.dia);
        limpiar_buffer();
        printf("Mes (1-12): ");
        scanf("%d", &fecha_reporte.mes);
        limpiar_buffer();
        printf("Anio: ");
        scanf("%d", &fecha_reporte.anio);
        limpiar_buffer();

        if (!validar_fecha(fecha_reporte.dia, fecha_reporte.mes, fecha_reporte.anio)) {
            printf("Fecha invalida. Por favor, ingrese una fecha valida.\n");
        }
    } while (!validar_fecha(fecha_reporte.dia, fecha_reporte.mes, fecha_reporte.anio));

    int cantidad_por_tipo[4] = {0}; // Índices 1-3 para los tipos de zapatos
    float monto_por_tipo[4] = {0};

    // Recorrer facturas de la fecha especificada
    for (int i = 0; i < num_facturas; i++) {
        if (facturas[i].fecha.dia == fecha_reporte.dia && facturas[i].fecha.mes == fecha_reporte.mes && facturas[i].fecha.anio == fecha_reporte.anio){
            
            for (int j = 0; j < facturas[i].num_items; j++) {
                ItemFactura item = facturas[i].items[j];
                int indice_producto = buscar_producto_por_codigo(item.codigo_producto);
                if (indice_producto != -1) {
                    int tipo = producto[indice_producto].tipo;
                    if (tipo >= 1 && tipo <= 3) {
                        cantidad_por_tipo[tipo] += item.cantidad;
                        monto_por_tipo[tipo] += item.subtotal;
                    }
                }
            }
        }
    }

    // Mostrar resultados
    printf("\n=== VENTAS DEL %02d/%02d/%d POR TIPO DE ZAPATO ===\n", 
           fecha_reporte.dia, fecha_reporte.mes, fecha_reporte.anio);
    printf("%-15s %-15s %-15s\n", "TIPO", "CANTIDAD", "MONTO TOTAL (Bs)");
    printf("--------------------------------------------\n");

    int total_unidades = 0;
    float total_monto = 0;

    for (int i = 1; i <= 3; i++) {
        char* nombre_tipo = "";
        switch(i) {
            case 1: nombre_tipo = "Deportivo"; break;
            case 2: nombre_tipo = "Casual"; break;
            case 3: nombre_tipo = "Formal"; break;
        }
        
        printf("%-15s %-15d %-15.2f\n", nombre_tipo, cantidad_por_tipo[i], monto_por_tipo[i]);
        total_unidades += cantidad_por_tipo[i];
        total_monto += monto_por_tipo[i];
    }
    
    printf("--------------------------------------------\n");
    printf("%-15s %-15d %-15.2f\n", "TOTAL", total_unidades, total_monto);
    printf("--------------------------------------------\n");
}

void mostrar_ultimas_facturas() {
    if (num_facturas == 0) {
        printf("No hay facturas registradas.\n");
        return;
    }

    int inicio = (num_facturas > 7) ? num_facturas - 7 : 0;
    
    printf("\n=== ULTIMAS %d FACTURAS ===\n", (num_facturas > 7) ? 7 : num_facturas);
    printf("Tasas de cambio actuales: USD: %.2f | EUR: %.2f | COP: %.2f\n", tasa_dolar, tasa_euro, tasa_peso);
    
    for (int i = inicio; i < num_facturas; i++) {
        printf("\nFactura #%d - Fecha: %02d/%02d/%d\n", 
               facturas[i].numero_factura, 
               facturas[i].fecha.dia, 
               facturas[i].fecha.mes, 
               facturas[i].fecha.anio);
        
        printf("Total: %.2f Bs. | %.2f USD | %.2f EUR | %.2f COP\n",
               facturas[i].total, facturas[i].total_dolares,
               facturas[i].total_euros, facturas[i].total_pesos);
        
        int indice_cliente = buscar_cliente_por_cedula(facturas[i].cedula_cliente);
        if (indice_cliente != -1) {
            printf("Cliente: %s (C.I. %d)\n", clien[indice_cliente].nombre, clien[indice_cliente].cedula);
        }
        
        printf("--------------------------------------------------\n");
    }
}
