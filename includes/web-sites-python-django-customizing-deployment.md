<span data-ttu-id="1653a-101">Azure determinará que la aplicación use Python **si se cumplen estas condiciones**:</span><span class="sxs-lookup"><span data-stu-id="1653a-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="1653a-102">la carpeta raíz contiene el archivo requirements.txt</span><span class="sxs-lookup"><span data-stu-id="1653a-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="1653a-103">la carpeta raíz contiene cualquier archivo .py o hay un runtime.txt que especifique Python.</span><span class="sxs-lookup"><span data-stu-id="1653a-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="1653a-104">Cuando ese es el caso, usará un script de implementación específico de Python, que lleva a cabo la sincronización de archivos, así como otras operaciones de Python como:</span><span class="sxs-lookup"><span data-stu-id="1653a-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="1653a-105">la administración automática del entorno virtual,</span><span class="sxs-lookup"><span data-stu-id="1653a-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="1653a-106">la instalación de paquetes que aparecen en requirements.txt con pip,</span><span class="sxs-lookup"><span data-stu-id="1653a-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="1653a-107">la creación del archivo web.config adecuado en función de la versión de Python seleccionada,</span><span class="sxs-lookup"><span data-stu-id="1653a-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="1653a-108">la recopilación de archivos estáticos para aplicaciones Django.</span><span class="sxs-lookup"><span data-stu-id="1653a-108">Collect static files for Django applications</span></span>

<span data-ttu-id="1653a-109">Puede controlar ciertos aspectos de los pasos de implementación predeterminados sin tener que personalizar el script.</span><span class="sxs-lookup"><span data-stu-id="1653a-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="1653a-110">Si desea omitir todos los pasos de implementación específicos de Python, puede crear este archivo vacío:</span><span class="sxs-lookup"><span data-stu-id="1653a-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="1653a-111">Si desea omitir la recopilación de archivos estáticos de la aplicación Django:</span><span class="sxs-lookup"><span data-stu-id="1653a-111">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="1653a-112">Para obtener más control sobre la implementación, puede invalidar el script de implementación predeterminado mediante la creación de los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1653a-112">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="1653a-113">Puede usar el [interfaz de línea de comandos de Azure] [ Azure command-line interface] para crear los archivos.</span><span class="sxs-lookup"><span data-stu-id="1653a-113">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="1653a-114">Use este comando desde la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="1653a-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="1653a-115">Cuando estos archivos no existen, Azure crea un script de implementación temporal y lo ejecuta.</span><span class="sxs-lookup"><span data-stu-id="1653a-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="1653a-116">Es idéntico al que se crea con el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="1653a-116">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
