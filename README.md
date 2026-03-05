# Sistema de Gestión de Venta de Entradas de Cine

## Descripción General

Aplicación de consola desarrollada en Java que implementa un sistema completo de gestión de venta de entradas de cine. El proyecto utiliza una arquitectura MVC (Modelo-Vista-Controlador) con integración a base de datos MySQL para la persistencia de datos.

El sistema simula un entorno real de venta de entradas donde los clientes pueden registrarse, consultar la cartelera, seleccionar asientos y adquirir entradas con descuentos automáticos según el volumen de compra.

## Funcionalidades Principales

### Gestión de Usuarios

- Registro de nuevos clientes con validación de datos (DNI, email, contraseña)
- Sistema de autenticación con encriptación AES de contraseñas
- Validación de formato de correo electrónico
- Verificación de unicidad de datos en base de datos

### Consulta de Películas y Sesiones

- Visualización de catálogo de películas con información detallada (duración, género)
- Filtrado dinámico de películas por fechas disponibles
- Consulta de sesiones por película y fecha
- Información en tiempo real de disponibilidad de asientos por sala
- Visualización de precios por sesión

### Sistema de Carrito y Compra

- Gestión de carrito con múltiples entradas de diferentes sesiones
- Cálculo automático de descuentos progresivos (20% para 2 sesiones, 30% para 3 o más)
- Generación de resumen detallado previo a la confirmación
- Aplicación automática de IVA (21%)
- Sistema de cancelación de reservas no confirmadas

### Gestión de Entradas

- Generación automática de tickets por compra
- Actualización en tiempo real del aforo de salas
- Persistencia de tickets en sistema de archivos
- Registro completo de información por entrada (película, fecha, hora, sala, precio)

## Estructura del Proyecto

El proyecto implementa la arquitectura MVC dividida en tres capas principales:

### Modelo (`src/modelo/`)

Contiene las clases de dominio que representan los objetos del negocio:

- `ClienteAcesso.java` - Gestión de información del cliente registrado
- `Pelicula.java` - Entidad de datos de películas
- `Sala.java` - Entidad de salas con gestión de capacidad
- `Sesion.java` - Entidad de sesiones con fecha, hora y precio
- `Carrito.java` - Lógica de carrito de compra con cálculo de descuentos
- `Ticket.java` - Entidad de entradas compradas
- `GestorCine.java` - Controlador de lógica de negocio principal
- `GestorTicket.java` - Gestor de persistencia de tickets
- `EspectadoresSesion.java` - Registro de espectadores por sesión
- `dniMailCliente.java` - Validador de datos de cliente

### Vista (`src/vista/`)

Capa de presentación basada en interfaz de consola:

- `Launcher.java` - Punto de entrada de la aplicación con sistema de menús interactivos

### Controlador (`src/controlador/`)

Capa de control que gestiona la lógica de entrada/salida y acceso a datos:

- `ControladorEntradaYSalida.java` - Validación y procesamiento de entradas del usuario
- `ControladorDB.java` - Gestión de conexiones y operaciones con base de datos MySQL
- `Imprimir.java` - Formateador y presentador de información en consola

## Flujo de Funcionamiento

1. **Conexión a Base de Datos**
   - Establecimiento de conexión con MySQL al iniciar la aplicación

2. **Autenticación**
   - Verificación de cuenta existente
   - Proceso de registro con validación de datos para nuevos usuarios
   - Sistema de login para usuarios registrados

3. **Selección de Película**
   - Presentación de catálogo de películas disponibles con sesiones futuras
   - Selección de película deseada

4. **Selección de Fecha**
   - Visualización de fechas disponibles para la película seleccionada
   - Elección de fecha de función

5. **Selección de Sesión**
   - Presentación de sesiones disponibles con horarios y salas
   - Selección de sesión y cantidad de entradas
   - Verificación automática de disponibilidad de asientos

6. **Carrito de Compra**
   - Opción de añadir entradas de múltiples sesiones
   - Cálculo automático de descuentos aplicables

7. **Confirmación y Pago**
   - Generación de resumen detallado con descuentos e IVA
   - Actualización transaccional de la base de datos
   - Generación y almacenamiento de tickets

## Requisitos Técnicos

### Software Necesario
- Java Development Kit (JDK) versión 8 o superior
- MySQL Server
- Driver JDBC para MySQL (mysql-connector-java)

### Configuración de Base de Datos

- **Base de datos**: `cine_daw`
- **Usuario**: `root`
- **Contraseña**: (vacía por defecto)
- **Host**: localhost
- **Puerto**: 3306

### Esquema de Base de Datos

- `Cliente` - Información de usuarios registrados
- `Pelicula` - Catálogo de películas
- `Sala` - Información de salas de proyección
- `Sesion` - Sesiones de películas (fecha, hora, sala, precio, aforo)
- `Compra` - Registro de transacciones realizadas
- `Entrada` - Detallede compras realizadas
`Entrada` Detalles de entradas vendidas
Instalación y Ejecución

1. Verificar que MySQL Server esté en ejecución
2. Ejecutar el script SQL ubicado en `ScriptBD/CineDaw.sql` para crear la base de datos
3. Compilar el proyecto Java
4. Ejecutar la clase principal `Launcher.java`
5. Navegar por la aplicación mediante los menús interactivos de consolal
5. Seguir los menús de consola para navegar por la aplicación
y Seguridad

- **DNI**: Validación de formato (9 caracteres)
- **Email**: Validación de formato de correo electrónico
- **Contraseña**: Encriptación mediante algoritmo AES
- **Capacidad**: Verificación de disponibilidad de asientos antes de confirmar compra
- **Sesiones**: Filtrado automático para mostrar únicamente sesiones futuras
- **Unicidad**: Validación de DNI y email únicos en el sistema
- **SQL Injection**: Uso de PreparedStatement para prevenir inyecciones SQL
DupPolítica de Descuentos

El sistema implementa descuentos progresivos automáticos según el volumen de compra:

- **1 sesión**: Sin descuento
- **2 sesiones**: 20% de descuento
- **3 o más sesiones**: 30% de descuento

Los descuentos se aplican sobre el subtotal previo al cálculo d

El Características Técnicas Destacadas

- **Seguridad**: Implementación de encriptación AES para almacenamiento seguro de contraseñas
- **Integridad de datos**: Uso de PreparedStatement para prevenir inyecciones SQL
- **Validación temporal**: Filtrado automático de sesiones basado en fecha y hora actual
- **Gestión de transacciones**: Limpieza automática del carrito tras completar o cancelar compras
- **Persistencia**: Almacenamiento de tickets en sistema de archivos para registro permanente

## Tecnologías Utilizadas

- **Lenguaje**: Java SE
- **Base de Datos**: MySQL
- **Arquitectura**: MVC (Modelo-Vista-Controlador)
- **Conectividad**: JDBC
- **Seguridad**: Encriptación AES

Proyecto de equipo de desarrollo para la asignatura de DAW (Desarrollo de Aplicaciones Web)
