<span data-ttu-id="21551-101">Algunos paquetes no pueden instalarse con pip cuando se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="21551-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="21551-102">Puede ser simplemente que ese paquete hello no está disponible en hello índice del paquete Python.</span><span class="sxs-lookup"><span data-stu-id="21551-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="21551-103">Es posible que un compilador es necesario (un compilador no está disponible en hello máquina hello web aplicación en ejecución en el servicio de aplicación de Azure).</span><span class="sxs-lookup"><span data-stu-id="21551-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="21551-104">En esta sección, se examinará toodeal maneras con este problema.</span><span class="sxs-lookup"><span data-stu-id="21551-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="21551-105">Solicitar ruedas</span><span class="sxs-lookup"><span data-stu-id="21551-105">Request wheels</span></span>
<span data-ttu-id="21551-106">Si la instalación del paquete Hola requiere que un compilador, debe intentar ponerse en contacto con toorequest Hola de propietario del paquete que estar disponibles para su paquete de hello ruedas.</span><span class="sxs-lookup"><span data-stu-id="21551-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="21551-107">Con la disponibilidad reciente Hola de [compilador de Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], ahora resulta más fácil toobuild que los paquetes con código nativo para Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="21551-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="21551-108">Compilar ruedas (necesita Windows)</span><span class="sxs-lookup"><span data-stu-id="21551-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="21551-109">Nota: Cuando se usa esta opción, asegúrese de seguro de paquete de hello toocompile utilizando un entorno de Python que coincida con hello plataforma / / versión de arquitectura que se usa en la aplicación web de hello en el servicio de aplicación de Azure (Windows/32-bit/2.7 o 3.4).</span><span class="sxs-lookup"><span data-stu-id="21551-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="21551-110">Si no se instala el paquete de hello porque requiere un compilador, puede instalar el compilador de hello en el equipo local y generar una rueda para paquete de hello, que, a continuación, se incluirá en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="21551-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="21551-111">Los usuarios de Mac y Linux: Si no dispone de máquina de Windows tooa de acceso, consulte [crear una máquina Virtual de Windows ejecutando] [ Create a Virtual Machine Running Windows] para saber cómo toocreate una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="21551-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="21551-112">Puede utilizar ruedas de hello toobuild, agregarlos toohello repositorio y descartar Hola VM si lo desea.</span><span class="sxs-lookup"><span data-stu-id="21551-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="21551-113">Python 2.7, puede instalar [compilador de Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="21551-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="21551-114">3.4 de Python, puede instalar [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="21551-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="21551-115">ruedas toobuild, necesitará paquete rueda de hello:</span><span class="sxs-lookup"><span data-stu-id="21551-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="21551-116">Deberá usar `pip wheel` toocompile una dependencia:</span><span class="sxs-lookup"><span data-stu-id="21551-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="21551-117">Esto crea un archivo .whl en la carpeta de \wheelhouse Hola.</span><span class="sxs-lookup"><span data-stu-id="21551-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="21551-118">Agregar carpeta de \wheelhouse de Hola y del repositorio de tooyour de archivos de rueda.</span><span class="sxs-lookup"><span data-stu-id="21551-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="21551-119">Editar el saludo de tooadd requirements.txt `--find-links` opción a la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="21551-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="21551-120">Esto indica a pip toolook una coincidencia exacta en la carpeta local de hello antes del índice del paquete de python de curso toohello.</span><span class="sxs-lookup"><span data-stu-id="21551-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="21551-121">Si desea tooinclude todas las dependencias hello \wheelhouse carpeta y no use Hola paquete de python de índice en absoluto, puede forzar el índice del paquete de pip tooignore Hola agregando `--no-index` toohello superior de su requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="21551-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="21551-122">Personalizar la instalación</span><span class="sxs-lookup"><span data-stu-id="21551-122">Customize installation</span></span>
<span data-ttu-id="21551-123">Puede personalizar tooinstall de script de implementación de hello un paquete en el entorno virtual de hello mediante un instalador alternativo, como la forma más fácil\_instalar.</span><span class="sxs-lookup"><span data-stu-id="21551-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="21551-124">Consulte deploy.cmd para obtener un ejemplo comentado.  Asegúrese de que estos paquetes no aparezcan en requirements.txt, tooprevent pip de instalarlos.</span><span class="sxs-lookup"><span data-stu-id="21551-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="21551-125">Agregue esta secuencia de comandos de implementación de toohello:</span><span class="sxs-lookup"><span data-stu-id="21551-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="21551-126">También es posible que pueda toouse fácil\_instalar tooinstall desde un instalador exe (algunos son zip compatible, es muy fácil\_instalación es compatible con ellos).</span><span class="sxs-lookup"><span data-stu-id="21551-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="21551-127">Agregar repositorio de tooyour de instalador de hello e invocar la forma más fácil\_instalar pasando ejecutable hello toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="21551-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="21551-128">Agregue esta secuencia de comandos de implementación de toohello:</span><span class="sxs-lookup"><span data-stu-id="21551-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="21551-129">Incluir el entorno virtual de hello en el repositorio de hello (requiere Windows)</span><span class="sxs-lookup"><span data-stu-id="21551-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="21551-130">Nota: Cuando se usa esta opción, asegúrese de toouse seguro de un entorno virtual que coincida con hello plataforma / / versión de arquitectura que se usa en la aplicación web de hello en el servicio de aplicación de Azure (Windows/32-bit/2.7 o 3.4).</span><span class="sxs-lookup"><span data-stu-id="21551-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="21551-131">Si incluye el entorno virtual de hello en el repositorio de hello, puede impedir que el script de implementación de hello dedican a la administración del entorno virtual en Azure mediante la creación de un archivo vacío:</span><span class="sxs-lookup"><span data-stu-id="21551-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="21551-132">Se recomienda eliminar entorno virtual existente de hello en la aplicación hello, archivos que hayan quedado tooprevent desde al entorno virtual de Hola se administra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="21551-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
