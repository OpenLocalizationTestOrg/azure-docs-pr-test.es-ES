---
title: "aplicación de Java aaaCompute intensiva en una máquina virtual | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se puede supervisar toocreate una máquina virtual de Azure que ejecuta una aplicación de Java de proceso intensivo que otra aplicación de Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="bb56a-103">¿Cómo toorun un proceso intensivo de tareas en Java en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bb56a-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="bb56a-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb56a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bb56a-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="bb56a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bb56a-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="bb56a-107">Con Azure, puede utilizar una tarea de proceso intensivo de toohandle de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb56a-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="bb56a-108">Por ejemplo, una máquina virtual puede administrar las tareas y entregar máquinas tooclient de resultados o aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="bb56a-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="bb56a-109">Después de leer este artículo, tendrá una descripción de cómo se puede supervisar toocreate una máquina virtual que ejecuta una aplicación de Java de proceso intensivo que otra aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="bb56a-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="bb56a-110">Este tutorial se supone que ya sabe cómo toocreate aplicaciones de consola de Java, puede importar la aplicación de Java de tooyour de bibliotecas y puede generar un archivo de Java (JAR).</span><span class="sxs-lookup"><span data-stu-id="bb56a-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="bb56a-111">Se presupone que no tiene conocimiento sobre Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bb56a-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="bb56a-112">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bb56a-112">You will learn:</span></span>

* <span data-ttu-id="bb56a-113">¿Cómo toocreate una máquina virtual con un Kit de desarrollo de Java (JDK) ya instalado.</span><span class="sxs-lookup"><span data-stu-id="bb56a-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="bb56a-114">¿Cómo tooremotely inicie sesión en la máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="bb56a-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="bb56a-115">¿Cómo toocreate un servicio de bus de espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="bb56a-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="bb56a-116">¿Cómo toocreate una aplicación Java que realiza una tarea de proceso intensivo.</span><span class="sxs-lookup"><span data-stu-id="bb56a-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="bb56a-117">¿Cómo toocreate una aplicación Java que supervisa Hola progreso de la tarea de proceso intensivo de hello.</span><span class="sxs-lookup"><span data-stu-id="bb56a-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="bb56a-118">¿Cómo toorun Hola aplicaciones Java.</span><span class="sxs-lookup"><span data-stu-id="bb56a-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="bb56a-119">¿Cómo toostop Hola aplicaciones Java.</span><span class="sxs-lookup"><span data-stu-id="bb56a-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="bb56a-120">Este tutorial usará Hola problema del viajante de tarea de proceso intensivo de hello.</span><span class="sxs-lookup"><span data-stu-id="bb56a-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="bb56a-121">Hola aquí te mostramos un ejemplo de Hola Java aplicación Hola proceso intensivo tarea en ejecución.</span><span class="sxs-lookup"><span data-stu-id="bb56a-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Solucionador del problema del viajante (TSP)][solver_output]

<span data-ttu-id="bb56a-123">Hola aquí te mostramos un ejemplo de Hola tarea de proceso intensivo de supervisión de aplicaciones de Java Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Cliente del problema del viajante][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="bb56a-125">toocreate una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bb56a-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="bb56a-126">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bb56a-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bb56a-127">Haga clic en **Nuevo**, **Proceso**, **Máquina virtual** y, a continuación, en **De la galería**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="bb56a-128">Hola **seleccione de la imagen de máquina Virtual** cuadro de diálogo, seleccione **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="bb56a-129">Tenga en cuenta que **Windows Server 2012 de JDK 6** está disponible si tiene aplicaciones heredadas que aún no están listo toorun en JDK 7.</span><span class="sxs-lookup"><span data-stu-id="bb56a-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="bb56a-130">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-130">Click **Next**.</span></span>
5. <span data-ttu-id="bb56a-131">Hola **configuración de máquina Virtual** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="bb56a-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="bb56a-132">Especifique un nombre para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="bb56a-133">Especifique hello toouse de tamaño de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="bb56a-134">Escriba un nombre para el Administrador de Hola Hola **nombre de usuario** campo.</span><span class="sxs-lookup"><span data-stu-id="bb56a-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="bb56a-135">Recuerde esta contraseña hello y nombre que pasará a continuación, se usa al registrar de forma remota en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="bb56a-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="bb56a-136">Escriba una contraseña en hello **nueva contraseña** campo y vuelva a escribirla en hello **confirmar** campo.</span><span class="sxs-lookup"><span data-stu-id="bb56a-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="bb56a-137">Se trata de una contraseña de cuenta de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="bb56a-138">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-138">Click **Next**.</span></span>
6. <span data-ttu-id="bb56a-139">Hola siguiente **configuración de máquina Virtual** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="bb56a-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="bb56a-140">Para **servicio en la nube**, usar valor predeterminado de hello **crear un nuevo servicio de nube**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="bb56a-141">Hola valor para **nombre DNS del servicio de nube** debe ser único en cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="bb56a-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="bb56a-142">Si es necesario, modifique este valor para que Azure indique que es exclusivo.</span><span class="sxs-lookup"><span data-stu-id="bb56a-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="bb56a-143">Especifique una región, un grupo de afinidad o una red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb56a-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="bb56a-144">En este tutorial, especifique una región como **Oeste de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="bb56a-145">En **Cuenta de almacenamiento**, seleccione **Usar una cuenta de almacenamiento generada automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="bb56a-146">En **Conjunto de disponibilidad**, seleccione **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="bb56a-147">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-147">Click **Next**.</span></span>
7. <span data-ttu-id="bb56a-148">Hola final **configuración de máquina Virtual** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="bb56a-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="bb56a-149">Aceptar entradas de punto de conexión de hello predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="bb56a-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="bb56a-150">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="bb56a-151">registro de tooremotely en la máquina virtual de tooyour</span><span class="sxs-lookup"><span data-stu-id="bb56a-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="bb56a-152">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bb56a-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bb56a-153">Haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="bb56a-154">Haga clic en el nombre de Hola de máquina virtual de Hola que desea toolog en.</span><span class="sxs-lookup"><span data-stu-id="bb56a-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="bb56a-155">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-155">Click **Connect**.</span></span>
5. <span data-ttu-id="bb56a-156">Responder mensajes toohello como máquina virtual de toohello de tooconnect necesarios.</span><span class="sxs-lookup"><span data-stu-id="bb56a-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="bb56a-157">Cuando se le solicite para contraseña y nombre de administrador de hello, utilice valores de hello que proporcionó cuando se creó la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="bb56a-158">Tenga en cuenta que Hola funcionalidad de Service Bus de Azure requiere toobe de certificado raíz de Baltimore CyberTrust Hola instalado como parte de su JRE **cacerts** almacenar.</span><span class="sxs-lookup"><span data-stu-id="bb56a-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="bb56a-159">Este certificado se incluye automáticamente en hello Java Runtime Environment (JRE) utilizado por este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bb56a-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="bb56a-160">Si no tiene este certificado en su JRE **cacerts** almacenar, consulte [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java] [ add_ca_cert] para obtener información sobre cómo agregarlo (así como obtener información acerca de cómo ver los certificados de hello en el almacén de cacerts).</span><span class="sxs-lookup"><span data-stu-id="bb56a-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="bb56a-161">¿Cómo toocreate un servicio de bus de espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="bb56a-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="bb56a-162">toobegin uso del Bus de servicio pone en cola en Azure, primero debe crear un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="bb56a-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="bb56a-163">Un espacio de nombres de servicio proporciona un contenedor con un ámbito para el desvío de recursos del Bus de servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb56a-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="bb56a-164">toocreate un espacio de nombres de servicio:</span><span class="sxs-lookup"><span data-stu-id="bb56a-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="bb56a-165">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bb56a-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bb56a-166">En el panel de navegación inferior izquierda de Hola de hello portal de Azure clásico, haga clic en **Bus de servicio, el Control de acceso y el almacenamiento en caché**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="bb56a-167">En el panel superior izquierdo de Hola de hello portal de Azure clásico, haga clic en hello **Service Bus** nodo y, a continuación, haga clic en hello **New** botón.</span><span class="sxs-lookup"><span data-stu-id="bb56a-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="bb56a-168">![Captura de pantalla del nodo Service Bus][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="bb56a-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="bb56a-169">Hola **crear un nuevo Namespace de servicio** diálogo cuadro, escriba un **Namespace**, y, a continuación, haga clic en toomake seguro de que es único, el **Comprobar disponibilidad** botón.</span><span class="sxs-lookup"><span data-stu-id="bb56a-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="bb56a-170">![Captura de pantalla de la creación de un nuevo espacio de nombres][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="bb56a-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="bb56a-171">Después de asegurarse el nombre del espacio de nombres de hello está disponible, elija el país o región en la que el espacio de nombres debe hospedarse y, a continuación, haga clic en hello **crear Namespace** botón.</span><span class="sxs-lookup"><span data-stu-id="bb56a-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="bb56a-172">espacio de nombres de Hola creado aparecerá en el portal de Azure clásico de Hola y toma un tooactivate este momento.</span><span class="sxs-lookup"><span data-stu-id="bb56a-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="bb56a-173">Espere hasta que el estado de hello **Active** antes de continuar con el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="bb56a-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="bb56a-174">Obtener credenciales de administración predeterminado de hello para el espacio de nombres de Hola</span><span class="sxs-lookup"><span data-stu-id="bb56a-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="bb56a-175">En las operaciones de administración del tooperform de orden, como la creación de una cola, en hello nuevo espacio de nombres, debe tener credenciales de administración de Hola de tooobtain para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="bb56a-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="bb56a-176">En el panel de navegación izquierdo de hello, haga clic en hello **Service Bus** nodo para mostrar lista de Hola de espacios de nombres disponibles.</span><span class="sxs-lookup"><span data-stu-id="bb56a-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="bb56a-177">![Captura de pantalla de los espacios de nombres disponibles][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="bb56a-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="bb56a-178">Seleccione el espacio de nombres de Hola que acaba de crear desde la lista de Hola que se muestra.</span><span class="sxs-lookup"><span data-stu-id="bb56a-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="bb56a-179">![Captura de pantalla de lista de espacio de nombres][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="bb56a-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="bb56a-180">Hola derecho **propiedades** panel muestra las propiedades de hello para el nuevo espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="bb56a-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="bb56a-181">![Captura de pantalla del panel de propiedades][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="bb56a-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="bb56a-182">Hola **clave predeterminada** está oculto.</span><span class="sxs-lookup"><span data-stu-id="bb56a-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="bb56a-183">Haga clic en hello **vista** botón credenciales de seguridad de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="bb56a-184">![Captura de pantalla de la clave predeterminada][default_key]</span><span class="sxs-lookup"><span data-stu-id="bb56a-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="bb56a-185">Tome nota de hello **emisor predeterminado** hello y **clave predeterminada** ya que usará esta información a continuación tooperform operaciones con el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="bb56a-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="bb56a-186">¿Cómo toocreate una aplicación Java que realiza una tarea de proceso intensivo</span><span class="sxs-lookup"><span data-stu-id="bb56a-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="bb56a-187">En el equipo de desarrollo (que no tiene la máquina virtual de toobe Hola que ha creado), descarga hello [Azure SDK para Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="bb56a-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="bb56a-188">Crear una aplicación de consola de Java mediante el código de ejemplo de Hola final Hola de esta sección.</span><span class="sxs-lookup"><span data-stu-id="bb56a-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="bb56a-189">En este tutorial, usaremos **TSPSolver.java** como nombre de archivo de hello Java.</span><span class="sxs-lookup"><span data-stu-id="bb56a-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="bb56a-190">Modificar hello **su\_servicio\_bus\_espacio de nombres**, **su\_servicio\_bus\_propietario**y **su\_servicio\_bus\_clave** toouse de marcadores de posición del bus de servicio **espacio de nombres**, **emisor predeterminado** y  **Clave predeterminada** valores, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bb56a-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="bb56a-191">Después de codificar, hello de paquete y de exportación Hola aplicación tooa ejecutable archivo Java (JAR) requiere bibliotecas en hello generan JAR.</span><span class="sxs-lookup"><span data-stu-id="bb56a-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="bb56a-192">En este tutorial, usaremos **TSPSolver.jar** como nombre de archivo JAR de hello generado.</span><span class="sxs-lookup"><span data-stu-id="bb56a-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="bb56a-193">¿Cómo toocreate una aplicación Java que supervisa Hola progreso de la tarea de proceso intensivo de hello</span><span class="sxs-lookup"><span data-stu-id="bb56a-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="bb56a-194">En el equipo de desarrollo, cree una aplicación de consola de Java con código de ejemplo de Hola final Hola de esta sección.</span><span class="sxs-lookup"><span data-stu-id="bb56a-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="bb56a-195">En este tutorial, usaremos **TSPClient.java** como nombre de archivo de hello Java.</span><span class="sxs-lookup"><span data-stu-id="bb56a-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="bb56a-196">Como se muestra anteriormente, modificar hello **su\_servicio\_bus\_espacio de nombres**, **su\_servicio\_bus\_propietario**, y **su\_servicio\_bus\_clave** toouse de marcadores de posición del bus de servicio **espacio de nombres**, **emisor predeterminado**y **clave predeterminada** valores, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bb56a-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="bb56a-197">Exportar Hola aplicación tooa JAR ejecutable y Hola de paquete requieren bibliotecas en hello generan JAR.</span><span class="sxs-lookup"><span data-stu-id="bb56a-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="bb56a-198">En este tutorial, usaremos **TSPClient.jar** como nombre de archivo JAR de hello generado.</span><span class="sxs-lookup"><span data-stu-id="bb56a-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="bb56a-199">¿Cómo toorun Hola aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="bb56a-199">How toorun hello Java applications</span></span>
<span data-ttu-id="bb56a-200">Ejecutar la aplicación de proceso intensivo de hello, primera cola de hello toocreate y, a continuación, toosolve Hola viaja Saleseman problema, que agregará Hola actual mejor ruta toohello cola de service bus.</span><span class="sxs-lookup"><span data-stu-id="bb56a-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="bb56a-201">Mientras Hola los aplicación de proceso intensivo es ejecutando (o posteriormente), resultados de ejecución Hola cliente toodisplay de cola de bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="bb56a-202">aplicación de proceso intensivo de hello toorun</span><span class="sxs-lookup"><span data-stu-id="bb56a-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="bb56a-203">Inicie sesión en la máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="bb56a-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="bb56a-204">Cree una carpeta en la que ejecutará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb56a-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="bb56a-205">Por ejemplo, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="bb56a-206">Copia **TSPSolver.jar** demasiado**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="bb56a-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="bb56a-207">Cree un archivo denominado **c:\TSP\cities.txt** con hello después de contenido.</span><span class="sxs-lookup"><span data-stu-id="bb56a-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="bb56a-208">En un símbolo del sistema, cambie los directorios tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="bb56a-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="bb56a-209">Asegúrese de carpeta bin de hello JRE está en la variable de entorno PATH de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="bb56a-210">Necesitará cola de bus de servicio de hello toocreate antes de ejecutar permutaciones de hello TSP solver.</span><span class="sxs-lookup"><span data-stu-id="bb56a-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="bb56a-211">Ejecute hello después de cola de bus de servicio de comando toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="bb56a-212">Hello cola una vez creada, puede ejecutar permutaciones de hello TSP solver.</span><span class="sxs-lookup"><span data-stu-id="bb56a-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="bb56a-213">Por ejemplo, ejecute hello después solver de hello toorun de comando para 8 ciudades.</span><span class="sxs-lookup"><span data-stu-id="bb56a-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="bb56a-214">Si no especifica un número, se ejecutará en 10 ciudades.</span><span class="sxs-lookup"><span data-stu-id="bb56a-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="bb56a-215">Como solver Hola encuentra rutas más cortas actuales, agregará toohello cola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="bb56a-216">Hola número que especifique, se ejecutará solver hello más larga de Hola Hola mayor.</span><span class="sxs-lookup"><span data-stu-id="bb56a-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="bb56a-217">Por ejemplo, si la ejecución en 14 ciudades puede tardar varios minutos, la ejecución en 15 ciudades podría tardar varias horas.</span><span class="sxs-lookup"><span data-stu-id="bb56a-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="bb56a-218">Aumentar too16 o ciudades más podrían en días de tiempo de ejecución (finalmente semanas, meses y años).</span><span class="sxs-lookup"><span data-stu-id="bb56a-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="bb56a-219">Esto es debido a toohello rápido aumento en número de Hola de permutaciones evaluada solver hello como Hola aumenta número de ciudades.</span><span class="sxs-lookup"><span data-stu-id="bb56a-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="bb56a-220">¿Cómo toorun Hola aplicación supervisión de cliente</span><span class="sxs-lookup"><span data-stu-id="bb56a-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="bb56a-221">Inicie sesión en la máquina de tooyour donde se ejecutará la aplicación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="bb56a-222">Esto no es necesario toobe Hola el mismo equipo que ejecuta hello **TSPSolver** aplicación, aunque puede ser.</span><span class="sxs-lookup"><span data-stu-id="bb56a-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="bb56a-223">Cree una carpeta en la que ejecutará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb56a-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="bb56a-224">Por ejemplo, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="bb56a-225">Copia **TSPClient.jar** demasiado**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="bb56a-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="bb56a-226">Asegúrese de carpeta bin de hello JRE está en la variable de entorno PATH de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="bb56a-227">En un símbolo del sistema, cambie los directorios tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="bb56a-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="bb56a-228">Ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb56a-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="bb56a-229">Opcionalmente, especifique el número de Hola de toosleep de minutos entre la comprobación de cola de hello, pasando un argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="bb56a-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="bb56a-230">Hello período de espera predeterminado para la comprobación de cola de Hola es 3 minutos, que se usa si se pasa ningún argumento de línea de comandos demasiado**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="bb56a-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="bb56a-231">Si desea toouse un valor diferente para el intervalo de suspensión de saludo, por ejemplo, un minuto, ejecute hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="bb56a-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="bb56a-232">Hola cliente se ejecutará hasta que ve un mensaje de la cola de "Completar".</span><span class="sxs-lookup"><span data-stu-id="bb56a-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="bb56a-233">Tenga en cuenta que si ejecuta varias repeticiones de solver Hola sin ejecutar el cliente de hello, deberá a cliente de hello toorun cola de hello vacía toocompletely varias veces.</span><span class="sxs-lookup"><span data-stu-id="bb56a-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="bb56a-234">Como alternativa, puede eliminar la cola de hello y, a continuación, vuelva a crearlo.</span><span class="sxs-lookup"><span data-stu-id="bb56a-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="bb56a-235">cola de hello toodelete, ejecute hello siguiente **TSPSolver** (no **TSPClient**) comando.</span><span class="sxs-lookup"><span data-stu-id="bb56a-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="bb56a-236">solver Hola se ejecutará hasta que finalice el examen de todas las rutas.</span><span class="sxs-lookup"><span data-stu-id="bb56a-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="bb56a-237">¿Cómo toostop Hola aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="bb56a-237">How toostop hello Java applications</span></span>
<span data-ttu-id="bb56a-238">Para solver hello y las aplicaciones cliente, puede presionar **Ctrl + C** tooexit si desea tooend toonormal anterior finalización.</span><span class="sxs-lookup"><span data-stu-id="bb56a-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
