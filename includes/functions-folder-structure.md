
código de Hello para todas las funciones de hello en una aplicación de la función especificada se encuentra en una carpeta raíz que contiene un archivo de configuración de host y las subcarpetas de uno o más, cada uno de los cuales contiene código de hello para una función diferente, como en el siguiente ejemplo de Hola:

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

Hola *host.json* archivo contiene alguna configuración específica del tiempo de ejecución y se ubica en la carpeta raíz de Hola de aplicación de la función de hello. Para obtener información sobre la configuración que están disponibles, vea [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) en hello WebJobs.Script repositorio wiki.

Cada función tiene una carpeta que contiene uno o varios archivos de código, configuración de function.json de Hola y otras dependencias.

