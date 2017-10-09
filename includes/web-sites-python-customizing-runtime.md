Azure determinará la versión de Hola de Python toouse para su entorno virtual con hello después de prioridad:

1. versión especificada en runtime.txt en la carpeta raíz de Hola
2. versión especificada por el valor de Python en configuración de la aplicación hello web (Hola **configuración** > **configuración de la aplicación** hoja para la aplicación web en hello Portal de Azure)
3. Python 2.7 es valor predeterminado de hello si no se especifica ninguna Hola anterior

Valores válidos para el contenido de Hola de 

    \runtime.txt

son:

* python-2.7
* python-3.4

Si versión micro hello (tercer dígito) se especifica, se omite.

