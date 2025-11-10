# GFPI
El GFPI (Gestor de Finanzas Personales Inteligente) es una aplicación desarrollada en Python que permite administrar de forma organizada los ingresos, gastos y ahorros de una persona o familia.
El sistema está diseñado para ser escalable y modular, aplicando Programación Orientada a Objetos (POO) y el patrón de arquitectura MVC (Modelo–Vista–Controlador).
Su objetivo principal es ayudar a los usuarios a controlar sus finanzas personales, ofreciendo herramientas para:
•	Registrar y consultar operaciones financieras.
•	Editar o eliminar movimientos.
•	Generar reportes con resúmenes de gastos e ingresos.
•	Exportar información a formatos como CSV o PDF (opcional).
•	Visualizar estadísticas de manera clara.
Objetivo del programa
•	Facilitar el control de gastos e ingresos en la vida cotidiana.
•	Proveer un sistema seguro, intuitivo y adaptable a distintos perfiles de usuario.
•	Implementar un CRUD completo (Crear, Leer, Actualizar, Borrar) sobre una base de datos MySQL, con consultas seguras y parametrizadas.
•	Servir como base para un sistema financiero más complejo en el futuro (ej: presupuestos, metas de ahorro, alertas).

Módulo transaccion.py
Define la estructura base de las transacciones financieras.
•	Clase Transaccion
Clase abstracta que representa una operación financiera.

I.	Atributos:
	_monto: valor de la operación (positivo).
	_descripcion: detalle de la transacción.
	_tipo: define si es ingreso (+) o gasto (–).

II.	Métodos:
	get_tipo(): devuelve el tipo de transacción.
	get_monto(): devuelve el monto.
	get_descripcion(): devuelve la descripción.
	set_descripcion(): permite modificar la descripción.
	calcular_impacto(): método abstracto, debe implementarse en subclases.
	__str__(): devuelve representación en texto.

III.	Clase Ingreso(Transaccion)
Representa ingresos de dinero.
	Sobrescribe calcular_impacto() → retorna +monto.

IV.	Clase Gasto(Transaccion)
Representa egresos de dinero.
	Sobrescribe calcular_impacto() → retorna -monto.
Módulo gestor_finanzas.py
Gestiona todas las transacciones y el balance.
•	Clase GestorFinanzas

V.	Atributos:
	_transacciones: lista privada con todas las operaciones.
	_balance: saldo actual.

VI.	Métodos:
	agregar_transaccion(): añade un ingreso o gasto y actualiza balance.
	listar_transacciones(): muestra las transacciones guardadas.
	ver_balance(): muestra el balance actual.
	crear_y_agregar_transaccion(): crea transacción desde inputs del usuario.

Módulo menu.py
Interfaz de usuario en consola.
•	Función menu(gestor)
Presenta un menú con 4 opciones:
1)	Agregar transacción.
2)	Ver balance.
3)	Listar transacciones.
4)	Salir.

Update del prototipo - Gestor de Finanzas Multiusuario
En esta nueva versión del proyecto se implementaron las siguientes mejoras:
•	Sistema de usuarios con contraseña: ahora cada persona puede crear su propio perfil, iniciar sesión y proteger su información financiera con una clave.
•	Gestión independiente de finanzas: cada usuario cuenta con un balance y lista de transacciones aislados de los demás.
Clases especializadas:
•	Transaccion como clase base abstracta.
•	Subclases Ingreso y Gasto que definen el impacto positivo o negativo en el balance.
•	Gestor de Finanzas: maneja de forma encapsulada el balance y las transacciones de cada usuario.
•	Menú interactivo: permite agregar transacciones, consultar balance, listar movimientos y cambiar de usuario.
•	Validaciones básicas: control de errores en montos, tipo de transacción y contraseñas.
Con estas mejoras, el prototipo ahora soporta multiusuario seguro y una experiencia más ordenada para llevar el control de ingresos y gastos.

Update Script SQL
1. Eliminación de columna balance en Usuario
Motivo: El balance se calcula dinámicamente desde las transacciones
Ventaja: Evita inconsistencia de datos
Implementación: Se calcula con SQL: SUM(CASE WHEN tipo='+' THEN monto ELSE -monto END)
2. Eliminación de columna categoria en Transaccion
Motivo: Simplificación del prototipo
Ventaja: Menos complejidad en la interfaz
Implementación: La descripción incluye el contexto
3. Eliminación de tabla Transferencia
Motivo: Las transferencias se implementan como transacciones simples
Ventaja: Modelo más simple y consistente
Implementación: Una transferencia = 2 transacciones (egreso + ingreso)
IMPACTO EN LA APLICACIÓN
Cambios en el Código:
Balance: Se calcula en tiempo real en lugar de almacenarse
Transacciones: Sin categorización, solo descripción
Transferencias: Implementadas como transacciones pareadas

ACTUALIZACIÓN DE LA CLASE USUARIO
MÉTODOS MODIFICADOS:
agregar_transaccion():
Se eliminó el parámetro categoria
Consulta SQL simplificada sin referencia a columna de categoría
Mantiene misma funcionalidad pero con menos complejidad
transferir():
Eliminada inserción en tabla Transferencia
Implementación mediante dos transacciones separadas
Mantiene el registro de movimiento pero con modelo más simple
obtener_transacciones():
Eliminada la columna categoria del SELECT
Eliminada lógica de fallback para categoría
Consulta más eficiente y simple
obtener_datos_graficos():
Eliminado el análisis por categorías
Mantenido solo el análisis mensual de ingresos vs gastos
Reducción de complejidad en el procesamiento de datos

NUEVAS IMPLEMENTACIONES
SISTEMA DE DEPURACIÓN COMPLETO:
Verificación de archivos esenciales al inicio
Logs detallados de cada etapa de carga
Manejo robusto de errores en todas las operaciones
Vistas de respaldo automáticas ante fallos
MANEJO DE IMÁGENES CON FALLBACKS:
Carga segura de imágenes de fondo y logo
Continuación de funcionamiento sin imágenes
Mensajes informativos de estado
CARGA DINÁMICA DE VISTAS:
Importación automática de todas las vistas
Creación de vistas de respaldo en caso de error
Sistema de navegación con validación

IMPACTO EN LA ARQUITECTURA
VENTAJAS OBTENIDAS:
Base de datos normalizada sin datos redundantes
Código más mantenible y menos propenso a errore
Mejor manejo de situaciones excepcionales
Mayor velocidad de desarrollo
COMPROMISOS ACEPTADOS:
Pérdida de categorización de transacciones
Cálculo de balance en tiempo real (mayor carga computacional)
Historial de transferencias menos detallado

MIGRACIÓN DE FUNCIONALIDADES
FUNCIONALIDADES MANTENIDAS:
Registro y autenticación de usuarios
Gestión completa de transacciones
Sistema de transferencias entre usuarios
Gráficos de análisis financiero
Interfaz gráfica completa

FUNCIONALIDADES ELIMINADAS:
Categorización automática de transacciones
Balance almacenado (se calcula dinámicamente)
Tabla específica para transferencias

MEJORAS EN LA ESTABILIDAD
MANEJO DE ERRORES:
Try-catch en todas las operaciones de base de datos
Validación de datos antes de cada operación
Mensajes de error informativos para el usuario
Recuperación automática ante fallos menores

VERIFICACIONES IMPLEMENTADAS:
Existencia de archivos requeridos
Conexión a base de datos
Carga de componentes de interfaz
Validación de datos de entrada

RESUMEN DE CAMBIOS TÉCNICOS
BASE DE DATOS:
De 3 tablas a 2 tablas
Eliminación de 2 columnas
Simplificación de relaciones

CÓDIGO BACKEND:
Reducción de complejidad en consultas SQL
Eliminación de código redundante
Mejor manejo de excepciones

INTERFAZ:
Mantenimiento de todas las funcionalidades visibles
Mejora en la experiencia de usuario ante errores
Sistema de logs para desarrollo
Esta actualización representa una evolución del prototipo hacia una arquitectura más robusta y mantenible, priorizando la estabilidad sobre características avanzadas en esta etapa de desarrollo.
