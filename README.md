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
