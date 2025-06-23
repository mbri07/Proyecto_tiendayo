#include<stdio.h>

void mostrarMenuPrincipal();
void mostrarSubMenuReportes();

int main() {
    int opcion_principal;
    int opcion_reportes;

    do {
        mostrarMenuPrincipal();
        printf("Seleccione una opcion: ");
        scanf("%d", &opcion_principal);

        switch (opcion_principal) {
            case 1:
                printf("\nHa seleccionado Inventario.\n");
                //función inventario 
                break;
            case 2:
                printf("\nHa seleccionado Productos.\n");
                //función productos
                break;
            case 3:
                printf("\nHa seleccionado Clientes.\n");
                //función clientes
                break;
            case 4:
                printf("\nHa seleccionado Facturas.\n");
                //función facturas
                break;
            case 5:
                printf("nHa seleccionado Trabajadores.\n");
                //función trabajadores
                break;
            case 6: // Opción para Reportes!
                do {
                    mostrarSubMenuReportes(); //submenú
                    printf("Seleccione una opcion de reporte: ");
                    scanf("%d", &opcion_reportes);

                    switch (opcion_reportes) {
                        // Opciones de INVENTARIO
                        case 1: printf("Inventario completo.\n"); break;
                        case 2: printf("Stock minimo.\n"); break;
                        case 3: printf("Productos danados.\n"); break;
                        // Opciones de VENTAS/PRODUCTOS
                        case 4: printf("Valor y costo.\n"); break;
                        case 5: printf("Tipos de zapato mas y menos vendidos.\n"); break;
                        case 6: printf("Total ventas por tipo de zapato.\n"); break;
                        case 7: printf("Ultimas 7 facturas.\n"); break;
                        // Opciones de CLIENTES/TRABAJADORES
                        case 8: printf("Clientes que realizaron compras.\n"); break;
                        case 9: printf("Cantidad de trabajadores.\n"); break;
                        case 10: printf("Proveedores.\n"); break;
                        // Opciones "Reportes" y "Salir" del submenú
                        case 11: printf("Volviendo al menú principal...\n"); break;
                        default: printf("Opcion de reporte no valida. Intente de nuevo.\n"); break;
                    }
                    
                    if (opcion_reportes != 12) { 
                        printf("Presione Enter para continuar...");
                        
                        while (getchar() != '\n'); 
                        getchar();
                    }
                } while (opcion_reportes != 11);
                break;
                
            case 7:
                printf("Saliendo del programa. ¡Hasta pronto!\n");
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
    printf("7. Ultimas 7 facturas\n");
    printf("\n--- CLIENTES/TRABAJADORES ---\n");
    printf("8. Clientes que realizaron compras\n");
    printf("9. Cantidad de trabajadores\n");
    printf("10. Proveedores\n");
    printf("\n");
    printf("11. Volver al menú principal...\n");
    printf("========================================\n");
}
