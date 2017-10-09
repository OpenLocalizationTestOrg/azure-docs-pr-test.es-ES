


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="d2e9d-101">Etiquetado de una máquina virtual mediante plantillas</span><span class="sxs-lookup"><span data-stu-id="d2e9d-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="d2e9d-102">En primer lugar, veamos el etiquetado a través de plantillas.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="d2e9d-103">[Esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) coloca las etiquetas en hello recursos siguientes: proceso (Máquina Virtual), almacenamiento (cuenta de almacenamiento) y red (dirección IP pública, red Virtual e interfaz de red).</span><span class="sxs-lookup"><span data-stu-id="d2e9d-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="d2e9d-104">Esta plantilla es para una máquina virtual Windows, pero se puede adaptar a máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="d2e9d-105">Haga clic en hello **implementar tooAzure** botón de hello [vínculo plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="d2e9d-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="d2e9d-106">Esto le remitirá toohello [portal de Azure](https://portal.azure.com/) donde puede implementar esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Implementación sencilla con etiquetas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="d2e9d-108">Esta plantilla incluye Hola siguientes etiquetas: *departamento*, *aplicación*, y *creado por*.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="d2e9d-109">Puede agregar o modificar estas etiquetas directamente en la plantilla de hello si desea que los nombres de etiqueta distinto.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Etiquetas de Azure en una plantilla](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="d2e9d-111">Como puede ver, etiquetas de Hola se definen como pares de clave/valor, separados por dos puntos (:).</span><span class="sxs-lookup"><span data-stu-id="d2e9d-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="d2e9d-112">Hola etiquetas deben definirse en este formato:</span><span class="sxs-lookup"><span data-stu-id="d2e9d-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="d2e9d-113">Guarde el archivo de plantilla de hello cuando termine de editar con etiquetas de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="d2e9d-114">Después, en hello **editar parámetros** sección, puede rellenar los valores de hello para las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Editar etiquetas en el Portal de Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="d2e9d-116">Haga clic en **crear** toodeploy esta plantilla con los valores de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="d2e9d-117">Etiquetado a través del Portal de Hola</span><span class="sxs-lookup"><span data-stu-id="d2e9d-117">Tagging through hello Portal</span></span>
<span data-ttu-id="d2e9d-118">Después de crear los recursos con etiquetas, puede ver, agregar y eliminar etiquetas en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="d2e9d-119">Hola seleccione etiquetas icono tooview etiquetas:</span><span class="sxs-lookup"><span data-stu-id="d2e9d-119">Select hello tags icon tooview your tags:</span></span>

![Icono de etiquetas en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="d2e9d-121">Agrega una nueva etiqueta a través del portal de hello mediante la definición de su propio par clave/valor y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Agregar etiqueta nueva en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="d2e9d-123">La nueva etiqueta debería aparecer ahora en la lista de Hola de etiquetas para el recurso.</span><span class="sxs-lookup"><span data-stu-id="d2e9d-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Etiqueta nueva guardada en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

