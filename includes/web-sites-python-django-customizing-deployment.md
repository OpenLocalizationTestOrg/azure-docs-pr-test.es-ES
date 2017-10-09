<span data-ttu-id="fdb67-101">Azure determinará que la aplicación use Python **si se cumplen estas condiciones**:</span><span class="sxs-lookup"><span data-stu-id="fdb67-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="fdb67-102">archivo Requirements.txt en la carpeta raíz de Hola</span><span class="sxs-lookup"><span data-stu-id="fdb67-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="fdb67-103">cualquier archivo .py en la carpeta raíz de Hola o runtime.txt que especifica python</span><span class="sxs-lookup"><span data-stu-id="fdb67-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="fdb67-104">Una vez que el caso de hello, usará un script de implementación específica de Python, que lleva a cabo Hola estándar sincronización de archivos, así como operaciones adicionales de Python, como:</span><span class="sxs-lookup"><span data-stu-id="fdb67-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="fdb67-105">la administración automática del entorno virtual,</span><span class="sxs-lookup"><span data-stu-id="fdb67-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="fdb67-106">la instalación de paquetes que aparecen en requirements.txt con pip,</span><span class="sxs-lookup"><span data-stu-id="fdb67-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="fdb67-107">Creación de hello web.config adecuado en función de hello seleccionado versión de Python.</span><span class="sxs-lookup"><span data-stu-id="fdb67-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="fdb67-108">la recopilación de archivos estáticos para aplicaciones Django.</span><span class="sxs-lookup"><span data-stu-id="fdb67-108">Collect static files for Django applications</span></span>

<span data-ttu-id="fdb67-109">Puede controlar algunos aspectos de pasos de implementación predeterminado de hello sin necesidad de script de Hola toocustomize.</span><span class="sxs-lookup"><span data-stu-id="fdb67-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="fdb67-110">Si desea tooskip todos los pasos de implementación específica de Python, puede crear este archivo vacío:</span><span class="sxs-lookup"><span data-stu-id="fdb67-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="fdb67-111">Si desea tooskip colección de archivos estáticos de la aplicación Django:</span><span class="sxs-lookup"><span data-stu-id="fdb67-111">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="fdb67-112">Para tener más control sobre la implementación, puede invalidar el script de implementación predeterminado de hello mediante la creación de hello siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="fdb67-112">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="fdb67-113">Puede usar hello [interfaz de línea de comandos de Azure] [ Azure command-line interface] toocreate archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb67-113">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="fdb67-114">Use este comando desde la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="fdb67-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="fdb67-115">Cuando estos archivos no existen, Azure crea un script de implementación temporal y lo ejecuta.</span><span class="sxs-lookup"><span data-stu-id="fdb67-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="fdb67-116">Es idéntico toohello que cree con hello comando anterior.</span><span class="sxs-lookup"><span data-stu-id="fdb67-116">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
