
<span data-ttu-id="76fc4-101">El código para todas las funciones de una aplicación de función dada se encuentra en una carpeta raíz que contiene un archivo de configuración de host y una o varias subcarpetas, cada una con el código de una función diferente, como se indica en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="76fc4-101">The code for all of the functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain the code for a separate function, as in the following example:</span></span>

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

<span data-ttu-id="76fc4-102">El archivo *host.json* contiene alguna configuración específica del tiempo de ejecución y se coloca en la carpeta principal de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="76fc4-102">The *host.json* file contains some runtime-specific configuration and sits in the root folder of the function app.</span></span> <span data-ttu-id="76fc4-103">Para obtener información sobre las opciones que están disponibles, consulte [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) en la wiki de repositorio de WebJobs.Script.</span><span class="sxs-lookup"><span data-stu-id="76fc4-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in the WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="76fc4-104">Cada función tiene una carpeta que contiene uno o varios archivos de código, la configuración de function.json y otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="76fc4-104">Each function has a folder that contains one or more code files, the function.json configuration and other dependencies.</span></span>

