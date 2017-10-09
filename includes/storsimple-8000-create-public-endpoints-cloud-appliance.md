#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="b6093-101">toocreate extremos públicos en el dispositivo de hello en la nube</span><span class="sxs-lookup"><span data-stu-id="b6093-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="b6093-102">Inicie sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6093-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="b6093-103">Vaya demasiado**máquinas virtuales**y, a continuación, seleccione y haga clic en la máquina virtual de Hola que se usa como el dispositivo en la nube.</span><span class="sxs-lookup"><span data-stu-id="b6093-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="b6093-104">Debe toocreate red seguridad (NSG) del grupo regla toocontrol Hola flujo de tráfico dentro y fuera de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b6093-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="b6093-105">Realizar Hola siguiendo los pasos toocreate una regla de NSG.</span><span class="sxs-lookup"><span data-stu-id="b6093-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="b6093-106">Seleccione **Grupo de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="b6093-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="b6093-107">Haga clic en el grupo de seguridad de red de forma predeterminada de Hola que se presenta.</span><span class="sxs-lookup"><span data-stu-id="b6093-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="b6093-108">Seleccione **Reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="b6093-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="b6093-109">Haga clic en **+ agregar** toocreate una regla de seguridad de entrada.</span><span class="sxs-lookup"><span data-stu-id="b6093-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="b6093-110">En la hoja de regla de seguridad de entrada de hello agregar:</span><span class="sxs-lookup"><span data-stu-id="b6093-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="b6093-111">Para hello **nombre**, escriba lo siguiente Hola nombre para el punto de conexión de hello: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="b6093-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="b6093-112">Para hello **prioridad**, seleccione un número menor que 1000 (que es la prioridad de hello para la regla predeterminada de hello).</span><span class="sxs-lookup"><span data-stu-id="b6093-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="b6093-113">Valor de hello mayor, menor prioridad Hola.</span><span class="sxs-lookup"><span data-stu-id="b6093-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="b6093-114">Conjunto hello **origen** demasiado**cualquier**.</span><span class="sxs-lookup"><span data-stu-id="b6093-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="b6093-115">Para hello **servicio**, seleccione **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="b6093-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="b6093-116">Hola **protocolo** automáticamente se establece demasiado**TCP** hello y **intervalo de puertos** se establece demasiado**5986**.</span><span class="sxs-lookup"><span data-stu-id="b6093-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="b6093-117">Haga clic en **Aceptar** regla de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b6093-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="b6093-118">El paso final es tooassociate grupo de seguridad de su red con una subred o una interfaz de red específica.</span><span class="sxs-lookup"><span data-stu-id="b6093-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="b6093-119">Realizar Hola siguiendo los pasos tooassociate el grupo de seguridad de red con una subred.</span><span class="sxs-lookup"><span data-stu-id="b6093-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="b6093-120">Vaya demasiado**subredes**.</span><span class="sxs-lookup"><span data-stu-id="b6093-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="b6093-121">Haga clic en **+ Asociar**.</span><span class="sxs-lookup"><span data-stu-id="b6093-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="b6093-122">Seleccione la red virtual y, a continuación, seleccione subred adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6093-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="b6093-123">Haga clic en **Aceptar** regla de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b6093-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="b6093-124">Después de crea la regla de hello, puede ver su dirección de IP Virtual pública (VIP) de detalles toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="b6093-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="b6093-125">Anote esta dirección.</span><span class="sxs-lookup"><span data-stu-id="b6093-125">Record this address.</span></span>


