---
title: aaaCreate y restaurar una copia de seguridad en servicios de BizTalk | Documentos de Microsoft
description: "Entre los Servicios de BizTalk se incluye Copias de seguridad y restauración. Obtenga información acerca de cómo toocreate y restaurar una copia de seguridad y determinar qué obtiene la copia de seguridad. MABS, WABS"
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="9ba54-105">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="9ba54-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="9ba54-106">Azure BizTalk Services incluye las capacidades de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="9ba54-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="9ba54-107">Este tema describe cómo toobackup y restauración de los servicios de BizTalk mediante Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="9ba54-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="9ba54-108">También puede hacer una servicios de BizTalk mediante hello [API de REST de servicios de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="9ba54-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="9ba54-109">Las conexiones híbridas no se copian de seguridad, independientemente de hello Edition.</span><span class="sxs-lookup"><span data-stu-id="9ba54-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="9ba54-110">Debe volver a crear las conexiones híbridas.</span><span class="sxs-lookup"><span data-stu-id="9ba54-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="9ba54-111">Introducción</span><span class="sxs-lookup"><span data-stu-id="9ba54-111">Before you Begin</span></span>
* <span data-ttu-id="9ba54-112">Puede que las copias de seguridad y restauración no estén disponible para todas las ediciones.</span><span class="sxs-lookup"><span data-stu-id="9ba54-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="9ba54-113">Consulte [Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="9ba54-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="9ba54-114">Hola portal de Azure clásico puede crear una copia de seguridad a petición o crear una copia de seguridad programada.</span><span class="sxs-lookup"><span data-stu-id="9ba54-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="9ba54-115">Contenido de copia de seguridad puede ser restaurada toohello mismo BizTalk Service u tooa nueva BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="9ba54-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="9ba54-116">toorestore Hola BizTalk Service mediante Hola debe eliminarse el mismo nombre, existentes BizTalk Service de Hola y Hola nombre debe estar disponible.</span><span class="sxs-lookup"><span data-stu-id="9ba54-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="9ba54-117">Después de eliminar un BizTalk Service, puede tardar más tiempo del que deseaba Hola igual nombre toobe disponible.</span><span class="sxs-lookup"><span data-stu-id="9ba54-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="9ba54-118">Si no puede esperar Hola igual nombre toobe disponible, a continuación, restaurar tooa nueva BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="9ba54-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="9ba54-119">Servicios de BizTalk puede ser restaurada toohello misma edición o una edición superior.</span><span class="sxs-lookup"><span data-stu-id="9ba54-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="9ba54-120">No se admite la restauración de servicios de BizTalk tooa edición anterior de cuando se realizó la copia de seguridad de hello.</span><span class="sxs-lookup"><span data-stu-id="9ba54-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="9ba54-121">Por ejemplo, una copia de seguridad mediante Hola que edición básica se puede restaura toohello Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="9ba54-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="9ba54-122">Una copia de seguridad mediante Hola que Premium Edition no se puede restaura toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="9ba54-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="9ba54-123">números de Control de EDI de Hola se copian la continuidad de toomaintain Hola de números de control.</span><span class="sxs-lookup"><span data-stu-id="9ba54-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="9ba54-124">Si los mensajes se procesan después de la última copia de seguridad de hello, restaurar el contenido de esta copia de seguridad puede producir números de control duplicados.</span><span class="sxs-lookup"><span data-stu-id="9ba54-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="9ba54-125">Si un lote tiene mensajes activos, procesar por lotes de hello **antes de** ejecuta una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9ba54-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="9ba54-126">Al crear una copia de seguridad (según sea necesario o según se programe), no se almacenan nunca los mensajes en lotes.</span><span class="sxs-lookup"><span data-stu-id="9ba54-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="9ba54-127">**Si se realiza una copia de seguridad con mensajes activos en un lote, estos mensajes no se incluyen en la copia de seguridad y, por lo tanto, se pierden.**</span><span class="sxs-lookup"><span data-stu-id="9ba54-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="9ba54-128">Opcional: Hola Portal de servicios de BizTalk, detenga las operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="9ba54-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="9ba54-129">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-129">Create a backup</span></span>
<span data-ttu-id="9ba54-130">Puede realizar una copia de seguridad en cualquier momento y controlarla por completo.</span><span class="sxs-lookup"><span data-stu-id="9ba54-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="9ba54-131">Esta sección enumeran Hola pasos toocreate copias de seguridad con hello Azure clásico portal, incluidos:</span><span class="sxs-lookup"><span data-stu-id="9ba54-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="9ba54-132">Copia de seguridad bajo demanda</span><span class="sxs-lookup"><span data-stu-id="9ba54-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="9ba54-133">Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="9ba54-134"><a name="backupnow"></a>Copia de seguridad bajo demanda</span><span class="sxs-lookup"><span data-stu-id="9ba54-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="9ba54-135">Hola portal de Azure clásico, seleccione **servicios de BizTalk**, y, a continuación, seleccione Hola BizTalk Service desea toobackup.</span><span class="sxs-lookup"><span data-stu-id="9ba54-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="9ba54-136">Hola **panel** ficha, seleccione **copia de seguridad** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="9ba54-137">Escriba un nombre para la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9ba54-137">Enter a backup name.</span></span> <span data-ttu-id="9ba54-138">Por ejemplo, escriba *myBizTalkService*BU*Fecha*.</span><span class="sxs-lookup"><span data-stu-id="9ba54-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="9ba54-139">Elija una cuenta de almacenamiento blob y copia de seguridad de hello seleccione marca de verificación toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="9ba54-140">Una vez completada la copia de seguridad de hello, se crea un contenedor con nombre de copia de seguridad de Hola que especifique en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="9ba54-141">Este contenedor contiene la configuración de la copia de seguridad del servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="9ba54-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="9ba54-142"><a name="backupschedule"></a>Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="9ba54-143">Hola portal de Azure clásico, seleccione **servicios de BizTalk**, seleccione Hola nombre de BizTalk Service que desee copia de seguridad de tooschedule hello y, a continuación, seleccione hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="9ba54-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="9ba54-144">Conjunto hello **estado de copia de seguridad** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="9ba54-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="9ba54-145">Seleccione hello **cuenta de almacenamiento** toostore Hola copia de seguridad, escriba Hola **frecuencia** toocreate Hola copias de seguridad y cuánto tiempo tookeep Hola (**días de retención**):</span><span class="sxs-lookup"><span data-stu-id="9ba54-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="9ba54-146">**Notas**</span><span class="sxs-lookup"><span data-stu-id="9ba54-146">**Notes**</span></span>     
   
   * <span data-ttu-id="9ba54-147">En **días de retención**, período de retención de hello debe ser mayor que la frecuencia de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="9ba54-148">Seleccione **mantenga siempre al menos una copia de seguridad**, incluso si ya ha transcurrido el período de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="9ba54-149">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9ba54-149">Select **Save**.</span></span>

<span data-ttu-id="9ba54-150">Cuando se ejecuta un trabajo de copia de seguridad programado, crea un contenedor (datos de copia de seguridad de toostore) en la cuenta de almacenamiento de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="9ba54-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="9ba54-151">Hola nombre del contenedor de Hola se denomina *BizTalk Service Name-date-time*.</span><span class="sxs-lookup"><span data-stu-id="9ba54-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="9ba54-152">Si muestra un panel de BizTalk Service Hola un **error** estado:</span><span class="sxs-lookup"><span data-stu-id="9ba54-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Estado de la última copia de seguridad programada][BackupStatus] 

<span data-ttu-id="9ba54-154">vínculo de Hello abre Hola registros de operaciones de administración de servicios toohelp solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="9ba54-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="9ba54-155">Consulte [Servicios de BizTalk: solución de problemas mediante registros de operaciones](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="9ba54-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="9ba54-156">Restauración</span><span class="sxs-lookup"><span data-stu-id="9ba54-156">Restore</span></span>
<span data-ttu-id="9ba54-157">Puede restaurar las copias de seguridad de portal de Azure clásico de Hola o de hello [API de REST de servicios de BizTalk restaurar](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="9ba54-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="9ba54-158">Esta sección enumeran Hola pasos toorestore mediante el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="9ba54-159">Antes de restaurar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-159">Before restoring a backup</span></span>
* <span data-ttu-id="9ba54-160">Se pueden especificar los nuevos almacenes de seguimiento, archivado y supervisión al restaurar un servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="9ba54-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="9ba54-161">Hola se restauran los mismos datos en tiempo de ejecución de EDI.</span><span class="sxs-lookup"><span data-stu-id="9ba54-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="9ba54-162">copia de seguridad de Hello en tiempo de ejecución de EDI almacena números de control de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="9ba54-163">números de control de Hello restaurar están en orden desde el momento de Hola de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="9ba54-164">Si los mensajes se procesan después de la última copia de seguridad de hello, restaurar el contenido de esta copia de seguridad puede producir números de control duplicados.</span><span class="sxs-lookup"><span data-stu-id="9ba54-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="9ba54-165">Restauración de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-165">Restore a backup</span></span>
1. <span data-ttu-id="9ba54-166">Hola portal de Azure clásico, seleccione **New** > **servicios de aplicaciones** > **BizTalk Service** > **restaurar** :</span><span class="sxs-lookup"><span data-stu-id="9ba54-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restauración de una copia de seguridad][Restore]
2. <span data-ttu-id="9ba54-168">En **dirección URL de la copia de seguridad**, seleccione el icono de carpeta de Hola y expanda la cuenta de almacenamiento de Azure de Hola que almacenes Hola copia de seguridad de configuración de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="9ba54-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="9ba54-169">Expanda el contenedor de Hola y en el panel derecho de hello, seleccione Hola correspondiente archivo .txt de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9ba54-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="9ba54-170">seleccione **Open**(Abrir).</span><span class="sxs-lookup"><span data-stu-id="9ba54-170">Select **Open**.</span></span>
3. <span data-ttu-id="9ba54-171">En hello **restaurar el servicio de BizTalk** página, escriba un **el nombre del servicio de BizTalk** y compruebe hello **dirección URL del dominio**, **edición**y **Región** para hello restaura BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="9ba54-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="9ba54-172">**Crear una nueva instancia de base de datos SQL** para hello base de datos de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="9ba54-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="9ba54-173">Seleccione la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="9ba54-174">Comprobar nombre de Hola de base de datos SQL de hello, escriba Hola servidor físico donde se creará la base de datos SQL de Hola y un nombre de usuario y una contraseña para ese servidor.</span><span class="sxs-lookup"><span data-stu-id="9ba54-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="9ba54-175">Si desea edición de base de datos SQL tooconfigure hello, tamaño y otras propiedades, seleccione **configurar opciones de base de datos avanzada**.</span><span class="sxs-lookup"><span data-stu-id="9ba54-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="9ba54-176">Seleccione la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="9ba54-177">Crear una nueva cuenta de almacenamiento o escriba una cuenta de almacenamiento existente Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="9ba54-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="9ba54-178">Seleccione Hola marca de verificación toostart Hola restaurar.</span><span class="sxs-lookup"><span data-stu-id="9ba54-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="9ba54-179">Una vez que se complete correctamente la restauración de hello, aparece un nuevo BizTalk Service en un estado suspendido en la página de servicios de BizTalk de Hola Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="9ba54-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="9ba54-180"><a name="postrestore"></a>Después de restaurar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="9ba54-181">Hello BizTalk Service se restaura siempre en un **Suspended** estado.</span><span class="sxs-lookup"><span data-stu-id="9ba54-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="9ba54-182">En este estado, puede realizar los cambios de configuración antes de hello nuevo entorno es funcional, incluyendo:</span><span class="sxs-lookup"><span data-stu-id="9ba54-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="9ba54-183">Si ha creado aplicaciones de BizTalk Service mediante Hola SDK de servicios de BizTalk de Azure, deberá credenciales de Control de acceso (ACS) de tootooupdate hello en esos toowork de aplicaciones con el entorno de hello restaurar.</span><span class="sxs-lookup"><span data-stu-id="9ba54-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="9ba54-184">Restaurar un tooreplicate un entorno de BizTalk Service existente de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="9ba54-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="9ba54-185">En esta situación, si hay contratos configurados en el portal de servicios de BizTalk original de Hola que use una carpeta de origen FTP, deberá tooupdate contratos de hello en hello recién restaurado entorno toouse una carpeta FTP de origen diferente.</span><span class="sxs-lookup"><span data-stu-id="9ba54-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="9ba54-186">En caso contrario, puede haber dos contratos diferentes intentar toopull Hola mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="9ba54-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="9ba54-187">Si ha restaurado toohave varios entornos de BizTalk Service, asegúrese de que el destino correcto del entorno hello en aplicaciones de Visual Studio de hello, cmdlets de PowerShell, las API de REST o API de OM de administración de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="9ba54-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="9ba54-188">Es una copias de seguridad de buena práctica tooconfigure automatizada en el entorno del servicio de BizTalk de hello recién restaurado.</span><span class="sxs-lookup"><span data-stu-id="9ba54-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="9ba54-189">Hola toostart BizTalk Service Hola portal de Azure clásico, seleccione Hola restaura BizTalk Service y seleccione **reanudar** en la barra de tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba54-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="9ba54-190">¿Qué se incluye en la copia de seguridad?</span><span class="sxs-lookup"><span data-stu-id="9ba54-190">What gets backed up</span></span>
<span data-ttu-id="9ba54-191">Cuando se crea una copia de seguridad, hello siguientes elementos se copian:</span><span class="sxs-lookup"><span data-stu-id="9ba54-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="9ba54-192">Elementos incluidos en la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="9ba54-193">
 <strong>Portal de Azure BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="9ba54-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="9ba54-194">Configuración y tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="9ba54-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="9ba54-195">Detalles del asociado y perfil</span><span class="sxs-lookup"><span data-stu-id="9ba54-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="9ba54-196">Acuerdos de socios</span><span class="sxs-lookup"><span data-stu-id="9ba54-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="9ba54-197">Ensamblados personalizados implementados</span><span class="sxs-lookup"><span data-stu-id="9ba54-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="9ba54-198">Puentes implementados</span><span class="sxs-lookup"><span data-stu-id="9ba54-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="9ba54-199">Certificados</span><span class="sxs-lookup"><span data-stu-id="9ba54-199">Certificates</span></span></li>
<li><span data-ttu-id="9ba54-200">Transformaciones implementadas</span><span class="sxs-lookup"><span data-stu-id="9ba54-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="9ba54-201">Procesos</span><span class="sxs-lookup"><span data-stu-id="9ba54-201">Pipelines</span></span></li>
<li><span data-ttu-id="9ba54-202">Plantillas creado y guardado en hello Portal de servicios de BizTalk</span><span class="sxs-lookup"><span data-stu-id="9ba54-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="9ba54-203">Asignaciones X12 ST01 y GS01</span><span class="sxs-lookup"><span data-stu-id="9ba54-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="9ba54-204">Números de control (EDI)</span><span class="sxs-lookup"><span data-stu-id="9ba54-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="9ba54-205">Valores MIC de mensaje AS2</span><span class="sxs-lookup"><span data-stu-id="9ba54-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="9ba54-206">
 <strong>Servicio Azure BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="9ba54-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="9ba54-207">Certificado SSL</span><span class="sxs-lookup"><span data-stu-id="9ba54-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="9ba54-208">Datos del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="9ba54-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="9ba54-209">Contraseña del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="9ba54-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="9ba54-210">Configuración del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="9ba54-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="9ba54-211">Recuento de unidades de escalado</span><span class="sxs-lookup"><span data-stu-id="9ba54-211">Scale unit count</span></span></li>
<li><span data-ttu-id="9ba54-212">Edition</span><span class="sxs-lookup"><span data-stu-id="9ba54-212">Edition</span></span></li>
<li><span data-ttu-id="9ba54-213">Versión del producto</span><span class="sxs-lookup"><span data-stu-id="9ba54-213">Product Version</span></span></li>
<li><span data-ttu-id="9ba54-214">Región/Centro de datos</span><span class="sxs-lookup"><span data-stu-id="9ba54-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="9ba54-215">Clave y espacio de nombres del servicio de control de acceso (ACS)</span><span class="sxs-lookup"><span data-stu-id="9ba54-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="9ba54-216">Cadena de conexión de la base de datos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="9ba54-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="9ba54-217">Cadena de conexión de la cuenta de almacenamiento de archivado</span><span class="sxs-lookup"><span data-stu-id="9ba54-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="9ba54-218">Cadena de conexión de la cuenta de almacenamiento de supervisión</span><span class="sxs-lookup"><span data-stu-id="9ba54-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="9ba54-219">
 <strong>Elementos adicionales</strong></span><span class="sxs-lookup"><span data-stu-id="9ba54-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="9ba54-220">Tracking Database</span><span class="sxs-lookup"><span data-stu-id="9ba54-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="9ba54-221">Cuando se crea Hola BizTalk Service, se especifican detalles de la base de datos de seguimiento de hello, incluidos el nombre de base de datos de seguimiento de Hola y Hola servidor de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba54-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="9ba54-222">Hola base de datos de seguimiento no se copia automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9ba54-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="9ba54-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="9ba54-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="9ba54-224">Si Hola base de datos de seguimiento se elimina y Hola necesidades de base de datos recuperadas, debe existir una copia de seguridad anterior.</span><span class="sxs-lookup"><span data-stu-id="9ba54-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="9ba54-225">Si no existe una copia de seguridad, base de datos de seguimiento de Hola y sus datos no son recuperables.</span><span class="sxs-lookup"><span data-stu-id="9ba54-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="9ba54-226">En esta situación, cree una nueva base de datos de seguimiento con hello mismo nombre de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9ba54-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="9ba54-227">Además, se recomienda la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="9ba54-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="9ba54-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ba54-228">Next</span></span>
<span data-ttu-id="9ba54-229">Servicios de BizTalk de Azure toocreate en hello Azure clásico, vaya demasiado[servicios de BizTalk: portal clásico de aprovisionamiento con Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="9ba54-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="9ba54-230">toostart crear aplicaciones, vaya demasiado[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="9ba54-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="9ba54-231">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9ba54-231">See Also</span></span>
* [<span data-ttu-id="9ba54-232">Copia de seguridad del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="9ba54-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="9ba54-233">Restauración del servicio de BizTalk a partir de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9ba54-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="9ba54-234">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="9ba54-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="9ba54-235">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="9ba54-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="9ba54-236">Servicios de BizTalk: gráfico del estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="9ba54-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="9ba54-237">Servicios de BizTalk: pestañas Panel, Monitor y Escala</span><span class="sxs-lookup"><span data-stu-id="9ba54-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="9ba54-238">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="9ba54-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="9ba54-239">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="9ba54-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="9ba54-240">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="9ba54-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

