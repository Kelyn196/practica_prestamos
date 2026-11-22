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