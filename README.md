# Práctica de Préstamo de Equipo en Odoo
Estudiante: Kelyn Leonela Rodriguez Arias
Número de cuenta:0506200401292

Paso 1. Catálogo de equipos
1. ¿Qué pasa con un equipo cuando se desmarca el campo Activo? ¿Por qué es mejor que borrarlo?

R: Cuando se desmarca el campo Activo, el equipo deja de aparecer en las listas habituales, pero permanece guardado en el sistema. Es mejor que borrarlo porque permite conservar su información y su historial para futuras consultas.

2. ¿Para qué sirve copy=False en el campo codigo?

R: Sirve para evitar que el código de inventario se copie cuando se duplica un equipo, permitiendo que cada equipo tenga un código único.

Paso 2. Registro de préstamos

1. Este modelo usa _name y _inherit al mismo tiempo. ¿Qué hace cada uno aquí?

R: _name define el nombre del nuevo modelo que se está creando, mientras que _inherit permite heredar las funciones de mail.thread, como el historial de mensajes y los cambios realizados en el préstamo.

2. ¿Qué hace tracking=True en el campo state? Lo verá funcionar en el paso 4.

R: Permite registrar los cambios realizados en el estado del préstamo en el chatter, mostrando cuándo cambia de Borrador a Prestado o a Devuelto.

Paso 3. Equipos del préstamo

1. En fields.One2many("prestamo.linea", "prestamo_id"), ¿qué indica cada parámetro?

R: El primer parámetro, "prestamo.linea", indica el modelo relacionado. El segundo, "prestamo_id", indica el campo que conecta cada línea con su préstamo. Esto permite que un préstamo tenga varios equipos asociados.

2. ¿Qué pasa con las líneas cuando se borra un préstamo? ¿Qué parte del código lo define?

R: Cuando se elimina un préstamo, también se eliminan automáticamente las líneas relacionadas con él. Esto lo define ondelete="cascade" en el campo prestamo_id.

Paso 4. Flujo de estados

1. Los botones ya se ocultan según el estado. ¿Por qué los métodos vuelven a validar el estado?

R: Porque ocultar los botones solamente controla lo que aparece en la interfaz. Los métodos vuelven a validar el estado para evitar acciones incorrectas y asegurar que el préstamo cumpla las condiciones antes de cambiar.

2. ¿Qué hace prestamo.linea_ids.equipo_id.write(...)? ¿Por qué no hace falta un for para cada equipo?

R: Permite cambiar el estado de todos los equipos relacionados con el préstamo al mismo tiempo. No hace falta un for porque Odoo permite ejecutar write() sobre varios registros a la vez.

Paso 5. Reglas del préstamo

1. El campo equipo_id ya filtra los equipos disponibles. ¿Por qué hace falta el TODO 5?

R: Porque el filtro solamente muestra los equipos disponibles al momento de seleccionarlos. Su estado podría cambiar antes de confirmar el préstamo, por eso es necesario verificar nuevamente que sigan disponibles.

2. ¿En qué momento se ejecuta un método con @api.constrains? ¿Y la validación de action_prestar?

R: El método @api.constrains se ejecuta cuando se crean o modifican los campos indicados, para comprobar que los datos cumplan las reglas establecidas. La validación de action_prestar se ejecuta cuando el usuario presiona el botón Prestar.

Paso 6. Contacto, kanban y búsqueda
1. ¿Qué pasa si arrastra una tarjeta del kanban a otra columna? ¿Por qué?

R: Al arrastrar una tarjeta a otra columna, el equipo cambia de estado automáticamente. Esto sucede porque el kanban está agrupado por el campo estado, y Odoo permite modificar ese campo al mover las tarjetas entre columnas.

2. El campo prestamo_ids se agregó a res.partner. ¿Se crea una columna nueva en la tabla de contactos? Explique.

R: No, porque prestamo_ids es un campo One2many que permite consultar los préstamos relacionados con un contacto. La relación se guarda mediante el campo partner_id del modelo prestamo.prestamo, que es el que almacena la referencia al contacto.