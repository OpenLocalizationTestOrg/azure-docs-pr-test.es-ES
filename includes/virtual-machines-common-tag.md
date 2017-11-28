


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="8613c-101">Etiquetado de una máquina virtual mediante plantillas</span><span class="sxs-lookup"><span data-stu-id="8613c-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="8613c-102">En primer lugar, veamos el etiquetado a través de plantillas.</span><span class="sxs-lookup"><span data-stu-id="8613c-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="8613c-103">[Esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) coloca etiquetas en los siguientes recursos: proceso (máquina virtual), almacenamiento (cuenta de almacenamiento) y red (dirección IP pública, red virtual e interfaz de red).</span><span class="sxs-lookup"><span data-stu-id="8613c-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="8613c-104">Esta plantilla es para una máquina virtual Windows, pero se puede adaptar a máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="8613c-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="8613c-105">Haga clic en el botón **Implementar en Azure** del [vínculo de la plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="8613c-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="8613c-106">Esto le remitirá al [Portal de Azure](https://portal.azure.com/) , donde puede implementar esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="8613c-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Implementación sencilla con etiquetas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="8613c-108">Esta plantilla incluye las siguientes etiquetas: *Department*, *Application* y *Created By*.</span><span class="sxs-lookup"><span data-stu-id="8613c-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="8613c-109">Estas etiquetas se pueden agregar o modificar directamente en la plantilla si se desea cambiar sus nombres.</span><span class="sxs-lookup"><span data-stu-id="8613c-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Etiquetas de Azure en una plantilla](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="8613c-111">Como puede ver, las etiquetas se definen como pares de clave-valor, separados por dos puntos (:).</span><span class="sxs-lookup"><span data-stu-id="8613c-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="8613c-112">Las etiquetas deben definirse con este formato:</span><span class="sxs-lookup"><span data-stu-id="8613c-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="8613c-113">Guarde el archivo de plantilla cuando termine de modificarlo con las etiquetas que prefiera.</span><span class="sxs-lookup"><span data-stu-id="8613c-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="8613c-114">A continuación, en la sección **Editar parámetros** , puede rellenar los valores de las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="8613c-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Editar etiquetas en el Portal de Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="8613c-116">Haga clic en **Crear** para implementar esta plantilla con sus valores de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="8613c-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="8613c-117">Etiquetado a través del portal</span><span class="sxs-lookup"><span data-stu-id="8613c-117">Tagging through the Portal</span></span>
<span data-ttu-id="8613c-118">Después de crear los recursos con etiquetas, puede ver, agregar y eliminar etiquetas en el portal.</span><span class="sxs-lookup"><span data-stu-id="8613c-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="8613c-119">Seleccione el icono de etiquetas para ver las etiquetas:</span><span class="sxs-lookup"><span data-stu-id="8613c-119">Select the tags icon to view your tags:</span></span>

![Icono de etiquetas en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="8613c-121">Para agregar una nueva etiqueta desde el portal, defina su propio par de clave-valor y guárdela.</span><span class="sxs-lookup"><span data-stu-id="8613c-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Agregar etiqueta nueva en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="8613c-123">La nueva etiqueta debería aparecer en la lista de etiquetas del recurso.</span><span class="sxs-lookup"><span data-stu-id="8613c-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Etiqueta nueva guardada en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

