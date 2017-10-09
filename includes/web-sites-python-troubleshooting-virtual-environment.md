script de implementación de Hello omitirá la creación del entorno virtual de hello en Azure si detecta que ya existe un entorno virtual compatible.  Esto puede agilizar la implementación considerablemente.  Pip omitirá los paquetes que ya están instalados.

En ciertas situaciones, puede que desee eliminar tooforce dicho entorno virtual.  Debe tener toodo esto si decide tooinclude un entorno virtual como parte de su repositorio.  Puede que también desee toodo esto si necesita tooget rid de ciertos paquetes o probar cambios toorequirements.txt.

Hay unos Hola de toomanage opciones existentes de un entorno virtual en Azure:

### <a name="option-1-use-ftp"></a>Opción 1: utilizar FTP
Con un cliente FTP, conecte toohello servidor y se env carpeta de toodelete capaz de Hola.  Tenga en cuenta que algunos clientes FTP (por ejemplo, los exploradores web) pueden ser de sólo lectura y no permiten que las carpetas de toodelete, por lo que es conveniente toomake seguro toouse un cliente FTP con esa capacidad.  nombre de host FTP de Hola y el usuario se muestran en la hoja de la aplicación web en hello [Portal de Azure](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Opción2: alternar el tiempo de ejecución
Aquí es una alternativa que aprovecha las ventajas de hechos de hello script de implementación de hello eliminará carpeta env de hello cuando lo no coincide con la versión deseada de Hola de Python.  Esto eliminará eficazmente entorno existente de hello y crear uno nuevo.

1. Versión diferente de conmutador tooa de Python (a través de runtime.txt o hello **configuración de la aplicación** hoja Hola Portal de Azure)
2. Realizar cambios mediante inserciones de Git (ignorar cualquier error de instalación de PIP, si hay)
3. Cambiar tooinitial back-versión de Python
4. Volver a realizar cambios mediante inserciones de Git

### <a name="option-3-customize-deployment-script"></a>Opción 3: personalizar el script de implementación
Si ha personalizado el script de implementación de hello, puede cambiar Hola codificarlo en deploy.cmd tooforce carpeta env de toodelete Hola.

