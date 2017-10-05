---
title: "Creación y restauración de una copia de seguridad en BizTalk Services | Microsoft Docs"
description: "Entre los Servicios de BizTalk se incluye Copias de seguridad y restauración. Obtenga información acerca de cómo crear y restaurar una copia de seguridad y aprenda a determinar el contenido del que se realizan dichas copias. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="baaeb-105">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="baaeb-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="baaeb-106">Azure BizTalk Services incluye las capacidades de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="baaeb-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="baaeb-107">En este tema se describe cómo realizar la copia de seguridad y la restauración de los servicios de BizTalk con el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="baaeb-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="baaeb-108">También puede realizar la copia de seguridad de los Servicios de BizTalk mediante la [API REST de Servicios de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="baaeb-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="baaeb-109">NO se realiza ninguna copia de seguridad de las conexiones híbridas, independientemente de la edición.</span><span class="sxs-lookup"><span data-stu-id="baaeb-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="baaeb-110">Debe volver a crear las conexiones híbridas.</span><span class="sxs-lookup"><span data-stu-id="baaeb-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="baaeb-111">Introducción</span><span class="sxs-lookup"><span data-stu-id="baaeb-111">Before you Begin</span></span>
* <span data-ttu-id="baaeb-112">Puede que las copias de seguridad y restauración no estén disponible para todas las ediciones.</span><span class="sxs-lookup"><span data-stu-id="baaeb-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="baaeb-113">Consulte [Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="baaeb-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="baaeb-114">En el Portal de Azure clásico puede crear una copia de seguridad bajo demanda o crear una copia de seguridad programada.</span><span class="sxs-lookup"><span data-stu-id="baaeb-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="baaeb-115">El contenido de las copias de seguridad se puede restaurar en el mismo servicio de BizTalk o en uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="baaeb-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="baaeb-116">Para restaurar el servicio de BizTalk con el mismo nombre, es preciso eliminar el servicio de BizTalk existente y el nombre debe estar disponible.</span><span class="sxs-lookup"><span data-stu-id="baaeb-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="baaeb-117">Después de eliminar un servicio de BizTalk, puede tardar más tiempo del deseado para que el mismo nombre esté disponible.</span><span class="sxs-lookup"><span data-stu-id="baaeb-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="baaeb-118">Si no puede esperar a que el mismo nombre esté disponible, restaure a un nuevo servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="baaeb-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="baaeb-119">Se pueden restaurar los servicios de BizTalk en la misma edición o en una posterior.</span><span class="sxs-lookup"><span data-stu-id="baaeb-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="baaeb-120">No se puede realizar la restauración de los Servicios de BizTalk en una edición anterior con respecto a la usada para realizar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="baaeb-121">Por ejemplo, una copia de seguridad que usa la Basic Edition se puede restaurar a la Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="baaeb-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="baaeb-122">Sin embargo, una copia de seguridad que usa la Premium Edition no se puede restaurar a la Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="baaeb-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="baaeb-123">A fin de mantener la continuidad de los números de control del intercambio electrónico de datos (EDI), estos se incluyen en una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="baaeb-124">Si los mensajes se procesan después de la última copia de seguridad y se restaura el contenido de esta copia de seguridad, se pueden duplicar los números de control.</span><span class="sxs-lookup"><span data-stu-id="baaeb-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="baaeb-125">Si un lote tiene mensajes activos, procéselo **antes** de ejecutar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="baaeb-126">Al crear una copia de seguridad (según sea necesario o según se programe), no se almacenan nunca los mensajes en lotes.</span><span class="sxs-lookup"><span data-stu-id="baaeb-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="baaeb-127">**Si se realiza una copia de seguridad con mensajes activos en un lote, estos mensajes no se incluyen en la copia de seguridad y, por lo tanto, se pierden.**</span><span class="sxs-lookup"><span data-stu-id="baaeb-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="baaeb-128">Opcional: en el Portal de Servicios de BizTalk, detenga todas las operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="baaeb-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="baaeb-129">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-129">Create a backup</span></span>
<span data-ttu-id="baaeb-130">Puede realizar una copia de seguridad en cualquier momento y controlarla por completo.</span><span class="sxs-lookup"><span data-stu-id="baaeb-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="baaeb-131">Esta sección muestra los pasos para crear copias de seguridad mediante el Portal de Azure clásico, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="baaeb-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="baaeb-132">Copia de seguridad bajo demanda</span><span class="sxs-lookup"><span data-stu-id="baaeb-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="baaeb-133">Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="baaeb-134"><a name="backupnow"></a>Copia de seguridad bajo demanda</span><span class="sxs-lookup"><span data-stu-id="baaeb-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="baaeb-135">En el Portal de Azure clásico, seleccione **Servicios de BizTalk**y luego el servicio de BizTalk del que quiera realizar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="baaeb-136">En la pestaña **Panel**, seleccione **Hacer una copia de seguridad** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="baaeb-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="baaeb-137">Escriba un nombre para la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-137">Enter a backup name.</span></span> <span data-ttu-id="baaeb-138">Por ejemplo, escriba *myBizTalkService*BU*Fecha*.</span><span class="sxs-lookup"><span data-stu-id="baaeb-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="baaeb-139">Elija una cuenta de almacenamiento de blobs y seleccione la marca de verificación para iniciar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="baaeb-140">Una vez que finalice la copia de seguridad, en la cuenta de almacenamiento se creará un contenedor con el nombre de copia de seguridad que escriba.</span><span class="sxs-lookup"><span data-stu-id="baaeb-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="baaeb-141">Este contenedor contiene la configuración de la copia de seguridad del servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="baaeb-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="baaeb-142"><a name="backupschedule"></a>Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="baaeb-143">En el Portal de Azure clásico, seleccione **Servicios de BizTalk**, seleccione el nombre del servicio de BizTalk del que quiere programar la copia de seguridad y luego seleccione la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="baaeb-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="baaeb-144">Establezca **Estado de la copia de seguridad** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="baaeb-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="baaeb-145">Seleccione la **Cuenta de almacenamiento** para almacenar la copia de seguridad, especifique la **Frecuencia** con la que desea crear las copias de seguridad y cuánto tiempo quiere conservar las copias de seguridad (**Días de retención**):</span><span class="sxs-lookup"><span data-stu-id="baaeb-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="baaeb-146">**Notas**</span><span class="sxs-lookup"><span data-stu-id="baaeb-146">**Notes**</span></span>     
   
   * <span data-ttu-id="baaeb-147">En **Días de retención**, el período de retención debe ser superior a la frecuencia de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="baaeb-148">Seleccione **Conservar siempre al menos una copia de seguridad**, incluso aunque haya pasado el período de retención.</span><span class="sxs-lookup"><span data-stu-id="baaeb-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="baaeb-149">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="baaeb-149">Select **Save**.</span></span>

<span data-ttu-id="baaeb-150">Cuando se ejecuta un trabajo de copia de seguridad programada, se crea un contenedor (para almacenar los datos de la copia de seguridad) en la cuenta de almacenamiento que haya especificado.</span><span class="sxs-lookup"><span data-stu-id="baaeb-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="baaeb-151">El nombre del contenedor se denomina *BizTalk Service Name-date-time*.</span><span class="sxs-lookup"><span data-stu-id="baaeb-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="baaeb-152">Si el panel del Servicios de BizTalk muestra un estado **Con error** :</span><span class="sxs-lookup"><span data-stu-id="baaeb-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Estado de la última copia de seguridad programada][BackupStatus] 

<span data-ttu-id="baaeb-154">El vínculo abre los Registros de operaciones de Servicios de administración para ayudar a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="baaeb-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="baaeb-155">Consulte [Servicios de BizTalk: solución de problemas mediante registros de operaciones](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="baaeb-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="baaeb-156">Restore</span><span class="sxs-lookup"><span data-stu-id="baaeb-156">Restore</span></span>
<span data-ttu-id="baaeb-157">Puede restaurar las copias de seguridad desde el Portal de Azure clásico o desde la [API REST para la restauración del Servicio de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="baaeb-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="baaeb-158">En esta sección se muestran los pasos para realizar la restauración mediante el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="baaeb-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="baaeb-159">Antes de restaurar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-159">Before restoring a backup</span></span>
* <span data-ttu-id="baaeb-160">Se pueden especificar los nuevos almacenes de seguimiento, archivado y supervisión al restaurar un servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="baaeb-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="baaeb-161">Se restauran los mismos datos del tiempo de ejecución de EDI.</span><span class="sxs-lookup"><span data-stu-id="baaeb-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="baaeb-162">La copia de seguridad del tiempo de ejecución de EDI almacena los números de control.</span><span class="sxs-lookup"><span data-stu-id="baaeb-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="baaeb-163">Los números de control se restauran en secuencias desde la hora de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="baaeb-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="baaeb-164">Si los mensajes se procesan después de la última copia de seguridad y se restaura el contenido de esta copia de seguridad, se pueden duplicar los números de control.</span><span class="sxs-lookup"><span data-stu-id="baaeb-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="baaeb-165">Restauración de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-165">Restore a backup</span></span>
1. <span data-ttu-id="baaeb-166">En el Portal de Azure clásico, seleccione **Nuevo** > **App Services** > **BizTalk Service** > **Restaurar**:</span><span class="sxs-lookup"><span data-stu-id="baaeb-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restauración de una copia de seguridad][Restore]
2. <span data-ttu-id="baaeb-168">En **URL de copia de seguridad**, seleccione el icono de la carpeta y expanda la cuenta de almacenamiento de Azure que almacena la copia de seguridad de configuración del Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="baaeb-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="baaeb-169">Expanda el contenedor y, en el panel derecho, seleccione el archivo .txt de copia de seguridad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="baaeb-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="baaeb-170">seleccione **Open**(Abrir).</span><span class="sxs-lookup"><span data-stu-id="baaeb-170">Select **Open**.</span></span>
3. <span data-ttu-id="baaeb-171">En la página **Restaurar servicio de BizTalk**, escriba un **Nombre del servicio de BizTalk** y compruebe la **URL de dominio**, **Edición** y la **Región** para el Servicio de BizTalk restaurado.</span><span class="sxs-lookup"><span data-stu-id="baaeb-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="baaeb-172">**Cree una nueva instancia de base de datos SQL** para la base de datos de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="baaeb-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="baaeb-173">Seleccione la flecha siguiente.</span><span class="sxs-lookup"><span data-stu-id="baaeb-173">Select the next arrow.</span></span>
4. <span data-ttu-id="baaeb-174">Compruebe el nombre de la base de datos SQL, especifique el servidor físico en el que se creará la base de datos SQL, y el nombre de usuario y la contraseña de dicho servidor.</span><span class="sxs-lookup"><span data-stu-id="baaeb-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="baaeb-175">Si desea configurar la edición de SQL Database, el tamaño y otras propiedades, seleccione **Configurar las opciones avanzadas de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="baaeb-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="baaeb-176">Seleccione la flecha siguiente.</span><span class="sxs-lookup"><span data-stu-id="baaeb-176">Select the next arrow.</span></span>

1. <span data-ttu-id="baaeb-177">Cree una nueva cuenta de almacenamiento o especifique una cuenta de almacenamiento existente para los Servicios de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="baaeb-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="baaeb-178">Seleccione la marca de verificación para iniciar la restauración.</span><span class="sxs-lookup"><span data-stu-id="baaeb-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="baaeb-179">Cuando se haya realizado correctamente la restauración, se incluye un nuevo servicio de BizTalk cuyo estado está suspendido en la página de servicios de BizTalk del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="baaeb-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="baaeb-180"><a name="postrestore"></a>Después de restaurar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="baaeb-181">El servicio de BizTalk siempre está restaurado en un estado **Suspendido** .</span><span class="sxs-lookup"><span data-stu-id="baaeb-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="baaeb-182">En este estado, puede realizar cambios de configuración antes de que el nuevo entorno sea funcional, incluyendo:</span><span class="sxs-lookup"><span data-stu-id="baaeb-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="baaeb-183">Si ha creado aplicaciones del servicio de BizTalk mediante el SDK de los Servicios de BizTalk de Azure, puede que tenga que actualizar las credenciales de control de acceso (ACS) en dichas aplicaciones para que puedan funcionar con el entorno restaurado.</span><span class="sxs-lookup"><span data-stu-id="baaeb-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="baaeb-184">Restaure un Servicio de BizTalk para replicar un entorno de Servicio de BizTalk existente.</span><span class="sxs-lookup"><span data-stu-id="baaeb-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="baaeb-185">En esta situación, si hay contratos configurados en el portal de Servicios de BizTalk original que usa una carpeta FTP de origen, quizá desee actualizar los contratos del entorno recién restaurado para que usen una carpeta FTP con otro origen.</span><span class="sxs-lookup"><span data-stu-id="baaeb-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="baaeb-186">De lo contrario, puede haber dos contratos diferentes intentando extraer el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="baaeb-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="baaeb-187">Si ha llevado a cabo la restauración para tener varios entornos del Servicio de BizTalk, asegúrese de elegir el entorno correcto en las aplicaciones de Visual Studio, los cmdlets de PowerShell, las API de REST o las API de OM de administración de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="baaeb-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="baaeb-188">Es recomendable configurar copias de seguridad automatizadas en el entorno del Servicio de BizTalk recién restaurado.</span><span class="sxs-lookup"><span data-stu-id="baaeb-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="baaeb-189">Para iniciar el Servicio de BizTalk en el Portal de Azure clásico, seleccione el Servicio de BizTalk restaurado y seleccione **Reanudar** en la barra de tareas.</span><span class="sxs-lookup"><span data-stu-id="baaeb-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="baaeb-190">¿Qué se incluye en la copia de seguridad?</span><span class="sxs-lookup"><span data-stu-id="baaeb-190">What gets backed up</span></span>
<span data-ttu-id="baaeb-191">Se incluyen los elementos siguientes al crear una copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="baaeb-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="baaeb-192">Elementos incluidos en la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="baaeb-193">
 <strong>Portal de Azure BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="baaeb-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="baaeb-194">Configuración y tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="baaeb-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="baaeb-195">Detalles del asociado y perfil</span><span class="sxs-lookup"><span data-stu-id="baaeb-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="baaeb-196">Acuerdos de socios</span><span class="sxs-lookup"><span data-stu-id="baaeb-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="baaeb-197">Ensamblados personalizados implementados</span><span class="sxs-lookup"><span data-stu-id="baaeb-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="baaeb-198">Puentes implementados</span><span class="sxs-lookup"><span data-stu-id="baaeb-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="baaeb-199">Certificados</span><span class="sxs-lookup"><span data-stu-id="baaeb-199">Certificates</span></span></li>
<li><span data-ttu-id="baaeb-200">Transformaciones implementadas</span><span class="sxs-lookup"><span data-stu-id="baaeb-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="baaeb-201">Procesos</span><span class="sxs-lookup"><span data-stu-id="baaeb-201">Pipelines</span></span></li>
<li><span data-ttu-id="baaeb-202">Plantillas creadas y guardadas en el portal de servicios de BizTalk</span><span class="sxs-lookup"><span data-stu-id="baaeb-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="baaeb-203">Asignaciones X12 ST01 y GS01</span><span class="sxs-lookup"><span data-stu-id="baaeb-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="baaeb-204">Números de control (EDI)</span><span class="sxs-lookup"><span data-stu-id="baaeb-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="baaeb-205">Valores MIC de mensaje AS2</span><span class="sxs-lookup"><span data-stu-id="baaeb-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="baaeb-206">
 <strong>Servicio Azure BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="baaeb-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="baaeb-207">Certificado SSL</span><span class="sxs-lookup"><span data-stu-id="baaeb-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="baaeb-208">Datos del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="baaeb-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="baaeb-209">Contraseña del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="baaeb-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="baaeb-210">Configuración del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="baaeb-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="baaeb-211">Recuento de unidades de escalado</span><span class="sxs-lookup"><span data-stu-id="baaeb-211">Scale unit count</span></span></li>
<li><span data-ttu-id="baaeb-212">Edition</span><span class="sxs-lookup"><span data-stu-id="baaeb-212">Edition</span></span></li>
<li><span data-ttu-id="baaeb-213">Versión del producto</span><span class="sxs-lookup"><span data-stu-id="baaeb-213">Product Version</span></span></li>
<li><span data-ttu-id="baaeb-214">Región/Centro de datos</span><span class="sxs-lookup"><span data-stu-id="baaeb-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="baaeb-215">Clave y espacio de nombres del servicio de control de acceso (ACS)</span><span class="sxs-lookup"><span data-stu-id="baaeb-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="baaeb-216">Cadena de conexión de la base de datos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="baaeb-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="baaeb-217">Cadena de conexión de la cuenta de almacenamiento de archivado</span><span class="sxs-lookup"><span data-stu-id="baaeb-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="baaeb-218">Cadena de conexión de la cuenta de almacenamiento de supervisión</span><span class="sxs-lookup"><span data-stu-id="baaeb-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="baaeb-219">
 <strong>Elementos adicionales</strong></span><span class="sxs-lookup"><span data-stu-id="baaeb-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="baaeb-220">Tracking Database</span><span class="sxs-lookup"><span data-stu-id="baaeb-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="baaeb-221">Cuando se crea el Servicio de BizTalk, se definen los detalles de la base de datos de seguimiento, entre los que se incluyen el servidor de Base de datos SQL de Azure y el nombre de la base de datos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="baaeb-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="baaeb-222">No se realiza la copia de seguridad de la base de datos de seguimiento de forma automática.</span><span class="sxs-lookup"><span data-stu-id="baaeb-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="baaeb-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="baaeb-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="baaeb-224">Si la base de datos de seguimiento se elimina y hay que recuperarla, debe existir una copia de seguridad previa.</span><span class="sxs-lookup"><span data-stu-id="baaeb-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="baaeb-225">Si no la hay, no se podrán recuperar la base de datos de seguimiento ni sus datos.</span><span class="sxs-lookup"><span data-stu-id="baaeb-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="baaeb-226">En esta situación, cree una nueva base de datos de seguimiento con el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="baaeb-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="baaeb-227">Además, se recomienda la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="baaeb-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="baaeb-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="baaeb-228">Next</span></span>
<span data-ttu-id="baaeb-229">Para crear los Servicios de BizTalk de Azure en el Portal de Azure clásico, vaya a [Creación de Servicios de BizTalk mediante el Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="baaeb-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="baaeb-230">Para comenzar a crear aplicaciones, vaya a [Servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="baaeb-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="baaeb-231">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="baaeb-231">See Also</span></span>
* [<span data-ttu-id="baaeb-232">Copia de seguridad del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="baaeb-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="baaeb-233">Restauración del servicio de BizTalk a partir de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="baaeb-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="baaeb-234">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="baaeb-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="baaeb-235">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="baaeb-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="baaeb-236">Servicios de BizTalk: gráfico del estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="baaeb-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="baaeb-237">Servicios de BizTalk: pestañas Panel, Monitor y Escala</span><span class="sxs-lookup"><span data-stu-id="baaeb-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="baaeb-238">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="baaeb-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="baaeb-239">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="baaeb-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="baaeb-240">¿Cómo puedo comenzar a utilizar el SDK de Servicios de BizTalk de Azure?</span><span class="sxs-lookup"><span data-stu-id="baaeb-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

