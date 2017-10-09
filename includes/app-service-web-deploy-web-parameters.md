<span data-ttu-id="d1370-101">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="d1370-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="d1370-102">plantilla de Hello incluye una sección denominada parámetros que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1370-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="d1370-103">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1370-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="d1370-104">No se define parámetros para valores que siempre permanecerá Hola igual.</span><span class="sxs-lookup"><span data-stu-id="d1370-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="d1370-105">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="d1370-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="d1370-106">Al definir parámetros, usar hello **allowedValues** toospecify campo los valores de un usuario puede proporcionar durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="d1370-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="d1370-107">Hola de uso **defaultValue** tooassign campo valor toohello parámetro, si se proporciona ningún valor durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="d1370-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="d1370-108">Vamos a describir cada parámetro de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1370-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="d1370-109">siteName</span><span class="sxs-lookup"><span data-stu-id="d1370-109">siteName</span></span>
<span data-ttu-id="d1370-110">nombre de Hola de aplicación web de hello que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="d1370-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="d1370-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="d1370-111">hostingPlanName</span></span>
<span data-ttu-id="d1370-112">nombre de Hola de servicio de aplicaciones de hello planear toouse para hospedar la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="d1370-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="d1370-113">sku</span><span class="sxs-lookup"><span data-stu-id="d1370-113">sku</span></span>
<span data-ttu-id="d1370-114">Hola tarifa de hello plan de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="d1370-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="d1370-115">plantilla de Hello define los valores de hello permitidas para este parámetro y asigna un valor predeterminado (S1) si no se especifica ningún valor.</span><span class="sxs-lookup"><span data-stu-id="d1370-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="d1370-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="d1370-116">workerSize</span></span>
<span data-ttu-id="d1370-117">tamaño de la instancia de Hola de hello plan (pequeño, mediano o grande) de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="d1370-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="d1370-118">Hola plantilla define los valores de hello permitidas para este parámetro (0, 1 o 2) y asigna un valor predeterminado (0) si no se especifica ningún valor.</span><span class="sxs-lookup"><span data-stu-id="d1370-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="d1370-119">valores de Hello corresponden toosmall, mediana y grande.</span><span class="sxs-lookup"><span data-stu-id="d1370-119">hello values correspond toosmall, medium and large.</span></span>

