# Sistema de Control de Estacionamiento (Java Swing)

> **Nota:** Este proyecto representa una de mis primeras versiones desarrolladas hace varios años utilizando Java Swing y Programación Orientada a Objetos (POO). Se conserva como registro histórico de mis inicios en el desarrollo de software.

---

## 📌 Descripción del Sistema

Sistema de escritorio diseñado para la gestión y control de entradas, salidas, cálculo de tarifas y reportes en un parqueadero / estacionamiento.

---

## 📐 Arquitectura y Diseño de Clases

La arquitectura del sistema fue estructurada utilizando **Tarjetas CRC (Clase, Responsabilidad y Colaboradores)** y un **Diagrama de Clases UML**.

### 1. Tarjetas CRC

| Clase | Responsabilidades | Colaboradores |
| :--- | :--- | :--- |
| **`Estacionamiento`** | • `ingreso(placa, producto, espacio)`<br>• `salida(placa)`<br>• `listar_vehiculos()`<br>• `reportar_ingresos()`<br>• `validar()` | `Vehiculo`, `Espacio`, `Producto` |
| **`Producto`** | • `registrar_producto(nombre, tarifa, horas, sobreestadia, tolerancia)`<br>• `modificar_producto(...)`<br>• `eliminar_producto(nombre)` | `Estacionamiento`, `Espacio`, `Vehiculo` |
| **`Detalle_estacionamiento`** | • `modificar_datos(razon, ruc, direccion, celular, comentario, igv, capacidad, asignarespacios)` | `Estacionamiento` |
| **`Vehiculo`** | • Representación y estado de la unidad estacionada. | `Estacionamiento`, `Espacio`, `Producto` |
| **`Espacio`** | • Control de disponibilidad y asignación de lugares. | `Estacionamiento`, `Vehiculo`, `Producto` |
| **`Usuario`** | • Gestión de credenciales de acceso al sistema. | `Estacionamiento` |

---

### 2. Diagrama de Clases (UML)

```mermaid
classDiagram
    class detalle_estacionamiento {
        -String razon
        -String ruc
        -String dir
        -String cel
        -double igv
        -int capacidad
        -Boolean asignar_espacios
        +modificar_datos() void
    }

    class estacionamiento {
        -espacio espacios
        -vehiculo vehiculo
        -producto producto
        +ingresar() void
        +retirar() void
        +listar_vehiculos() void
        +reportar_ingresos() void
        +validar() void
    }

    class vehiculo {
        -String placa
        -String estado
    }

    class espacio {
        -int id
        -String horadeuso
        -String horadesuso
        -double cargo
        -vehiculo vehiculo
        -producto producto
    }

    class producto {
        -int id
        -String nombre
        -double tarifa
        -double horas
        -double sobreestadia
        -double tolerancia
        +agregar() void
        +modificar() void
        +eliminar() void
    }

    class usuario {
        -String usu
        -String pass
    }

    detalle_estacionamiento "1" -- "1" estacionamiento
    vehiculo "*" -- "1" estacionamiento
    estacionamiento "1" -- "*" espacio
    estacionamiento "1" *-- "*" producto
    estacionamiento "1" -- "*" usuario
