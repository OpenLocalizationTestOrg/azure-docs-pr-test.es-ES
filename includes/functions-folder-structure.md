
<span data-ttu-id="64389-101">código de Hello para todas las funciones de hello en una aplicación de la función especificada se encuentra en una carpeta raíz que contiene un archivo de configuración de host y las subcarpetas de uno o más, cada uno de los cuales contiene código de hello para una función diferente, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="64389-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

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

<span data-ttu-id="64389-102">Hola *host.json* archivo contiene alguna configuración específica del tiempo de ejecución y se ubica en la carpeta raíz de Hola de aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="64389-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="64389-103">Para obtener información sobre la configuración que están disponibles, vea [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) en hello WebJobs.Script repositorio wiki.</span><span class="sxs-lookup"><span data-stu-id="64389-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="64389-104">Cada función tiene una carpeta que contiene uno o varios archivos de código, configuración de function.json de Hola y otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="64389-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

