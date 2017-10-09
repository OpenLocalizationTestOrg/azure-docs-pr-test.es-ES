Aplicar etiquetas tooyour recursos de Azure toologically organizarlos por categorías. Cada etiqueta consta de un nombre y un valor. Por ejemplo, puede aplicar Hola recursos de nombre "Entorno" y Hola valor "Producción" tooall hello en producción. Sin esta etiqueta, puede que tenga dificultades para identificar si un recurso está diseñado para el desarrollo, la prueba o la producción. Sin embargo, "Entorno" y "Producción" son solo ejemplos. Se definen los nombres de Hola y valores que componen hello más conveniente para organizar su suscripción.

Después de aplicar las etiquetas, puede recuperar todos los recursos de hello en su suscripción con ese nombre de etiqueta y valor. Habilitación de las etiquetas se tooretrieve relacionados con los recursos que se encuentran en distintos grupos de recursos. Este enfoque es útil cuando necesita tooorganize recursos para administración o de facturación.

Hola siguientes limitaciones aplica tootags:

* Cada recurso o grupo de recursos puede tener un máximo de 15 pares de nombre/valor de etiqueta. Esta limitación aplica solo grupo de recursos de toohello tootags aplicada directamente o recurso. Un grupo de recursos puede contener muchos recursos con 15 pares de clave/valor de etiqueta cada uno. 
* nombre de etiqueta de Hello es limitado too512 caracteres y valor de etiqueta de hello es limitado too256 caracteres. Las cuentas de almacenamiento, nombre de etiqueta de hello es limitado too128 caracteres y valor de etiqueta de hello es limitado too256 caracteres.
* Grupo de recursos de etiquetas aplicadas toohello no son heredadas por recursos hello en ese grupo de recursos. 

Si tiene más de 15 valores que necesita tooassociate con un recurso, use una cadena JSON para el valor de etiqueta de Hola. Hola cadena JSON puede contener muchos valores que son el nombre de etiqueta única tooa aplicada. Este artículo muestra un ejemplo de asignación de una etiqueta de toohello de cadena JSON.
