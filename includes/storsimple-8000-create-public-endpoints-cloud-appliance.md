#### <a name="to-create-public-endpoints-on-the-cloud-appliance"></a><span data-ttu-id="3c084-101">Creación de puntos de conexión públicos en la aplicación en la nube</span><span class="sxs-lookup"><span data-stu-id="3c084-101">To create public endpoints on the cloud appliance</span></span>

1. <span data-ttu-id="3c084-102">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c084-102">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="3c084-103">Vaya a **Máquinas virtuales**y, a continuación, haga clic en la máquina virtual que se utiliza como aplicación en la nube.</span><span class="sxs-lookup"><span data-stu-id="3c084-103">Go to **Virtual Machines**, and then select and click the virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="3c084-104">Debe crear una regla de grupo de seguridad de red (NSG) para controlar el flujo de tráfico de entrada y salida de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3c084-104">You need to create a network security group (NSG) rule to control the flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="3c084-105">Realice los siguientes pasos para crear una regla de NSG.</span><span class="sxs-lookup"><span data-stu-id="3c084-105">Perform the following steps to create an NSG rule.</span></span>
    1. <span data-ttu-id="3c084-106">Seleccione **Grupo de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="3c084-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="3c084-107">Haga clic en el grupo de seguridad de red predeterminado que se presenta.</span><span class="sxs-lookup"><span data-stu-id="3c084-107">Click the default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="3c084-108">Seleccione **Reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="3c084-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="3c084-109">Haga clic en **+ Agregar** para crear una regla de seguridad de entrada.</span><span class="sxs-lookup"><span data-stu-id="3c084-109">Click **+ Add** to create an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="3c084-110">En la hoja Agregar regla de seguridad de entrada:</span><span class="sxs-lookup"><span data-stu-id="3c084-110">In the Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="3c084-111">En **Nombre**, escriba el siguiente nombre para el punto de conexión: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="3c084-111">For the **Name**, type the following name for the endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="3c084-112">En **Prioridad**, seleccione un número menor que 1000 (que es la prioridad para la regla predeterminada).</span><span class="sxs-lookup"><span data-stu-id="3c084-112">For the **Priority**, select a number lesser than 1000 (which is the priority for the default rule).</span></span> <span data-ttu-id="3c084-113">Cuanto mayor sea el valor, menor es la prioridad.</span><span class="sxs-lookup"><span data-stu-id="3c084-113">Higher the value, lower the priority.</span></span>

        3. <span data-ttu-id="3c084-114">Establezca **Origen** en **Cualquiera**.</span><span class="sxs-lookup"><span data-stu-id="3c084-114">Set the **Source** to **Any**.</span></span>

        4. <span data-ttu-id="3c084-115">En **Servicio**, seleccione **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="3c084-115">For the **Service**, select **WinRM**.</span></span> <span data-ttu-id="3c084-116">El **protocolo** se establece automáticamente en **TCP** y el **intervalo de puertos** se establece en **5986**.</span><span class="sxs-lookup"><span data-stu-id="3c084-116">The **Protocol** is automatically set to **TCP** and the **Port range** is set to **5986**.</span></span>

        5. <span data-ttu-id="3c084-117">Haga clic en **Aceptar** para crear la regla.</span><span class="sxs-lookup"><span data-stu-id="3c084-117">Click **OK** to create the rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="3c084-118">El paso final es asociar el grupo de seguridad de red a una subred o una interfaz de red específica.</span><span class="sxs-lookup"><span data-stu-id="3c084-118">Your final step is to associate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="3c084-119">Realice los pasos siguientes para asociar el grupo de seguridad de red a una subred.</span><span class="sxs-lookup"><span data-stu-id="3c084-119">Perform the following steps to associate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="3c084-120">Vaya a **Subredes**.</span><span class="sxs-lookup"><span data-stu-id="3c084-120">Go to **Subnets**.</span></span>
    2. <span data-ttu-id="3c084-121">Haga clic en **+ Asociar**.</span><span class="sxs-lookup"><span data-stu-id="3c084-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="3c084-122">Seleccione la red virtual y luego seleccione la subred adecuada.</span><span class="sxs-lookup"><span data-stu-id="3c084-122">Select your virtual network, and then select the appropriate subnet.</span></span>
    4. <span data-ttu-id="3c084-123">Haga clic en **Aceptar** para crear la regla.</span><span class="sxs-lookup"><span data-stu-id="3c084-123">Click **OK** to create the rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="3c084-124">Una vez creada la regla, puede ver sus detalles para determinar la dirección IP virtual (VIP) pública.</span><span class="sxs-lookup"><span data-stu-id="3c084-124">After the rule is created, you can view its details to determine the Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="3c084-125">Anote esta dirección.</span><span class="sxs-lookup"><span data-stu-id="3c084-125">Record this address.</span></span>


