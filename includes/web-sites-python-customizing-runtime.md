<span data-ttu-id="e3e5a-101">Azure determinará la versión de Python que se usará para su entorno virtual con la siguiente prioridad:</span><span class="sxs-lookup"><span data-stu-id="e3e5a-101">Azure will determine the version of Python to use for its virtual environment with the following priority:</span></span>

1. <span data-ttu-id="e3e5a-102">versión especificada en runtime.txt en la carpeta raíz</span><span class="sxs-lookup"><span data-stu-id="e3e5a-102">version specified in runtime.txt in the root folder</span></span>
2. <span data-ttu-id="e3e5a-103">versión especificada en la configuración de Python en la configuración de la aplicación web (la hoja **Configuración** > **Configuración de la aplicación** de su aplicación web en Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="e3e5a-103">version specified by Python setting in the web app configuration (the **Settings** > **Application Settings** blade for your web app in the Azure Portal)</span></span>
3. <span data-ttu-id="e3e5a-104">python-2.7 es el valor predeterminado si no se especifica ninguno de los anteriores</span><span class="sxs-lookup"><span data-stu-id="e3e5a-104">python-2.7 is the default if none of the above are specified</span></span>

<span data-ttu-id="e3e5a-105">Los valores válidos para el contenido</span><span class="sxs-lookup"><span data-stu-id="e3e5a-105">Valid values for the contents of</span></span> 

    \runtime.txt

<span data-ttu-id="e3e5a-106">son:</span><span class="sxs-lookup"><span data-stu-id="e3e5a-106">are:</span></span>

* <span data-ttu-id="e3e5a-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="e3e5a-107">python-2.7</span></span>
* <span data-ttu-id="e3e5a-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="e3e5a-108">python-3.4</span></span>

<span data-ttu-id="e3e5a-109">Si se especifica la versión micro (tercer dígito), se ignora.</span><span class="sxs-lookup"><span data-stu-id="e3e5a-109">If the micro version (third digit) is specified, it is ignored.</span></span>

