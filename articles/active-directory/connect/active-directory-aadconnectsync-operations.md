---
title: "Sincronización de Azure AD Connect: tareas y consideraciones operativas | Microsoft Docs"
description: "En este tema se describe las tareas operativas para la sincronización de Azure AD Connect y cómo tooprepare para el funcionamiento de este componente."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="0aa9c-103">Sincronización de Azure AD Connect: tareas y consideraciones operativas</span><span class="sxs-lookup"><span data-stu-id="0aa9c-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="0aa9c-104">objetivo de Hola de este tema es toodescribe tareas operativas para la sincronización de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="0aa9c-105">Modo provisional</span><span class="sxs-lookup"><span data-stu-id="0aa9c-105">Staging mode</span></span>
<span data-ttu-id="0aa9c-106">Se puede usar el modo provisional para distintos escenarios como:</span><span class="sxs-lookup"><span data-stu-id="0aa9c-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="0aa9c-107">Alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-107">High availability.</span></span>
* <span data-ttu-id="0aa9c-108">Prueba e implementación de nuevos cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="0aa9c-109">Introducir a un nuevo servidor y retirar Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="0aa9c-110">Con un servidor en modo de almacenamiento provisional, puede realizar cambios toohello vista previa y configuración Hola cambios antes de realizar active server Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="0aa9c-111">También permite importación completa toorun y tooverify de sincronización completa que se esperan que todos los cambios antes de realizar estos cambios en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="0aa9c-112">Durante la instalación, puede seleccionar Hola server toobe en **modo de almacenamiento provisional**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="0aa9c-113">Esta acción hace que el servidor hello activo para importación y sincronización, pero no ejecuta las exportaciones.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="0aa9c-114">Un servidor en modo provisional no ejecutará la sincronización de contraseñas ni habilitará la escritura diferida de contraseñas, aunque se seleccionen estas características durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="0aa9c-115">Cuando se deshabilita el modo de almacenamiento provisional, servidor hello inicia la exportación, habilita la sincronización de contraseña y permite la escritura diferida de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="0aa9c-116">Todavía puede forzar una exportación mediante el Administrador de servicio de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="0aa9c-117">Un servidor en modo de almacenamiento provisional continuará tooreceive cambios de Active Directory y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="0aa9c-118">Siempre tiene una copia de los cambios más recientes de Hola y que pueden tomar muy rápido a través de las responsabilidades de Hola de otro servidor.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="0aa9c-119">Si realiza el servidor principal de tooyour de cambios de configuración, es su responsabilidad toomake Hola el mismo servidor de toohello de cambios en el modo de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="0aa9c-120">Para los usuarios que tienen conocimientos de tecnologías de sincronización anteriores, Hola modo de almacenamiento provisional es diferente puesto que servidor hello tiene su propia base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="0aa9c-121">Esta arquitectura permite Hola modo servidor toobe ubicado en otro centro de datos de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="0aa9c-122">Comprobar la configuración de Hola de un servidor</span><span class="sxs-lookup"><span data-stu-id="0aa9c-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="0aa9c-123">tooapply este método, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0aa9c-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="0aa9c-124">Preparación</span><span class="sxs-lookup"><span data-stu-id="0aa9c-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="0aa9c-125">Configuración</span><span class="sxs-lookup"><span data-stu-id="0aa9c-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="0aa9c-126">Importación y sincronización</span><span class="sxs-lookup"><span data-stu-id="0aa9c-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="0aa9c-127">Verify</span><span class="sxs-lookup"><span data-stu-id="0aa9c-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="0aa9c-128">Cambio de servidor activo</span><span class="sxs-lookup"><span data-stu-id="0aa9c-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="0aa9c-129">Preparación</span><span class="sxs-lookup"><span data-stu-id="0aa9c-129">Prepare</span></span>
1. <span data-ttu-id="0aa9c-130">Instalar Azure AD Connect, seleccione **modo de almacenamiento provisional**y anule la selección de **iniciar la sincronización de** en la última página del Asistente para instalación Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="0aa9c-131">Este modo le permite motor de sincronización de hello toorun manualmente.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="0aa9c-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="0aa9c-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="0aa9c-133">Inicio de sesión desactivado/inicio de sesión y de hello iniciar menú, seleccione **servicio de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="0aa9c-134">Configuración</span><span class="sxs-lookup"><span data-stu-id="0aa9c-134">Configuration</span></span>
<span data-ttu-id="0aa9c-135">Si ha realizado cambios personalizados toohello principal configuración del servidor y desea toocompare Hola con hello servidor de ensayo, a continuación, utilice [Documentador de configuración de Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="0aa9c-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="0aa9c-136">Importación y sincronización</span><span class="sxs-lookup"><span data-stu-id="0aa9c-136">Import and Synchronize</span></span>
1. <span data-ttu-id="0aa9c-137">Seleccione **conectores**, y seleccione Hola primer conector con el tipo de hello **los servicios de dominio de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="0aa9c-138">Haga clic en **Ejecutar** y seleccione **Importación completa** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="0aa9c-139">Realice estos pasos para todos los conectores de este tipo.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="0aa9c-140">Seleccione Hola conector con el tipo de **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="0aa9c-141">Haga clic en **Ejecutar** y seleccione **Importación completa** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="0aa9c-142">Asegúrese de que todavía se selecciona la ficha de hello conectores.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="0aa9c-143">Para cada conector de tipo **Active Directory Domain Services**, haga clic en **Ejecutar**, y seleccione **Sincronización diferencial** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="0aa9c-144">Seleccione Hola conector con el tipo de **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="0aa9c-145">Haga clic en **Ejecutar**, seleccione **Sincronización diferencial** y, después, **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="0aa9c-146">Tiene ahora la exportación preconfigurada cambia tooAzure AD y AD local (si está utilizando la implementación híbrida de Exchange).</span><span class="sxs-lookup"><span data-stu-id="0aa9c-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="0aa9c-147">pasos siguientes Hola permiten tooinspect novedades sobre toochange antes de empezar realmente directorios de toohello de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="0aa9c-148">Verify</span><span class="sxs-lookup"><span data-stu-id="0aa9c-148">Verify</span></span>
1. <span data-ttu-id="0aa9c-149">Inicie un símbolo del sistema y vaya demasiado`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="0aa9c-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="0aa9c-150">Para ejecutar: `csexport "Name of Connector" %temp%\export.xml /f:x` nombre Hola de hello conector puede encontrarse en el servicio de sincronización.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="0aa9c-151">Tiene un too"contoso.com similar nombre – AAD" para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="0aa9c-152">Copie el script de PowerShell de Hola de sección de hello [CSAnalyzer](#appendix-csanalyzer) archivo tooa denominado `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="0aa9c-153">Abra una ventana de PowerShell y busque la carpeta toohello donde se creó la secuencia de comandos de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="0aa9c-154">Ejecute `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="0aa9c-155">Ahora tiene un archivo denominado "**processedusers1.csv**" que se puede examinar en Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="0aa9c-156">Todos los cambios almacenados provisionalmente toobe exportar tooAzure AD se encuentran en este archivo.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="0aa9c-157">Realice los cambios necesarios toohello datos o la configuración y ejecute estos pasos nuevo (importación y sincronización y comprobar) hasta Hola se esperan que los cambios que tienen aproximadamente toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="0aa9c-158">Cambio de servidor activo</span><span class="sxs-lookup"><span data-stu-id="0aa9c-158">Switch active server</span></span>
1. <span data-ttu-id="0aa9c-159">En servidor actualmente activo de hello, desactive la opción servidor hello (DirSync/FIM/Azure AD Sync) por lo que no está exportando tooAzure AD o establecerla en el modo (Azure AD Connect) de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="0aa9c-160">Ejecutar el Asistente para la instalación de hello en servidor de hello en **modo de almacenamiento provisional** y deshabilitar **modo de almacenamiento provisional**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="0aa9c-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="0aa9c-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="0aa9c-162">Recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="0aa9c-162">Disaster recovery</span></span>
<span data-ttu-id="0aa9c-163">Parte del diseño de la implementación de hello es tooplan para qué toodo en caso de que hay un desastre que pierde el servidor de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="0aa9c-164">Existen distintos modelos toouse y qué uno toouse depende de varios factores como:</span><span class="sxs-lookup"><span data-stu-id="0aa9c-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="0aa9c-165">¿Qué es la tolerancia para que no se puede hacer cambios tooobjects en Azure AD durante el tiempo de inactividad de hello?</span><span class="sxs-lookup"><span data-stu-id="0aa9c-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="0aa9c-166">¿Si utiliza la sincronización de contraseña, los usuarios de hello acepta que tienen contraseña antigua de toouse hello en Azure AD en caso de cambian local?</span><span class="sxs-lookup"><span data-stu-id="0aa9c-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="0aa9c-167">¿Tiene una dependencia en operaciones en tiempo real, como la escritura diferida de contraseñas?</span><span class="sxs-lookup"><span data-stu-id="0aa9c-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="0aa9c-168">Función hello respuestas toothese preguntas y directiva de su organización, se puede implementar uno Hola siguientes estrategias:</span><span class="sxs-lookup"><span data-stu-id="0aa9c-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="0aa9c-169">Recompilación si es necesario.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-169">Rebuild when needed.</span></span>
* <span data-ttu-id="0aa9c-170">Servidor en espera de reserva, conocido como **modo provisional**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="0aa9c-171">Uso de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-171">Use virtual machines.</span></span>

<span data-ttu-id="0aa9c-172">Si no utiliza la base de datos SQL Express integrado hello, también debe revisar hello [alta disponibilidad de SQL](#sql-high-availability) sección.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="0aa9c-173">Recompilación si es necesario</span><span class="sxs-lookup"><span data-stu-id="0aa9c-173">Rebuild when needed</span></span>
<span data-ttu-id="0aa9c-174">Una estrategia viable es tooplan para una regeneración del servidor cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="0aa9c-175">Por lo general, instalar motor de sincronización de Hola y Hola importación inicial y sincronización puede realizarse dentro de unas pocas horas.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="0aa9c-176">Si no hay un servidor de repuesto disponibles, es posible tootemporarily utilice un motor de sincronización de dominio controlador toohost Hola.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="0aa9c-177">servidor de motor de sincronización de Hello no almacenan cualquier estado acerca de los objetos de hello, por lo que se puede volver a generar base de datos de Hola de datos de hello en Active Directory y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="0aa9c-178">Hola **sourceAnchor** atributo es toojoin usado Hola objetos desde el entorno local y hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="0aa9c-179">Si se vuelve a generar Hola servidor con objetos locales existentes y hello en la nube, a continuación, el motor de sincronización de hello coincide con esos objetos conjuntamente nuevo de reinstalación.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="0aa9c-180">las cosas de Hello necesite toodocument y guarde son cambios de configuración de hello realizados toohello server, como las reglas de filtrado y la sincronización.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="0aa9c-181">Estas configuraciones personalizadas deben volver a aplicarse antes de iniciar la sincronización.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="0aa9c-182">Servidor en espera de reserva - modo provisional</span><span class="sxs-lookup"><span data-stu-id="0aa9c-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="0aa9c-183">Si tiene un entorno más complejo, se recomienda tener uno o más servidores en espera.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="0aa9c-184">Durante la instalación, puede habilitar un toobe server en **modo de almacenamiento provisional**.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="0aa9c-185">Para obtener más información, consulte [Modo provisional](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="0aa9c-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="0aa9c-186">Uso de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="0aa9c-186">Use virtual machines</span></span>
<span data-ttu-id="0aa9c-187">Un método común y se admite es el motor de sincronización de hello toorun en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="0aa9c-188">En caso de que el host de hello tiene un problema, imagen de hello con servidor de motor de sincronización de hello puede ser servidor tooanother migrados.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="0aa9c-189">alta disponibilidad de SQL</span><span class="sxs-lookup"><span data-stu-id="0aa9c-189">SQL High Availability</span></span>
<span data-ttu-id="0aa9c-190">Si no utilizas Hola SQL Server Express que viene con Azure AD Connect, alta disponibilidad para SQL Server también debe considerarse.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="0aa9c-191">soluciones de alta disponibilidad de Hello admitidas incluyen la agrupación en clústeres de SQL y AOA (grupos de disponibilidad AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="0aa9c-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="0aa9c-192">Entre las soluciones no admitidas se incluye la creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="0aa9c-193">Se agregó compatibilidad con SQL AOA tooAzure AD Connect en la versión 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="0aa9c-194">Debe habilitar AOA de SQL antes de instalar Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="0aa9c-195">Durante la instalación, Azure AD Connect detecta si la instancia SQL Hola proporcionada está habilitada para SQL AOA o no.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="0aa9c-196">Si está habilitado SQL AOA, Azure AD Connect más averigua si SQL AOA es toouse configurada la replicación sincrónica o replicación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="0aa9c-197">Al configurar el agente de escucha del grupo de disponibilidad de hello, se recomienda que establezca hello RegisterAllProvidersIP propiedad too0.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="0aa9c-198">Esto es porque Azure AD Connect utiliza actualmente SQL Native Client tooconnect tooSQL y SQL Native Client no admite el uso de Hola de propiedad MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="0aa9c-199">Apéndice: CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="0aa9c-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="0aa9c-200">Consulte la sección de hello [comprobar](#verify) acerca de cómo toouse esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="0aa9c-200">See hello section [verify](#verify) on how toouse this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="0aa9c-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0aa9c-201">Next steps</span></span>
<span data-ttu-id="0aa9c-202">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="0aa9c-202">**Overview topics**</span></span>  

* [<span data-ttu-id="0aa9c-203">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="0aa9c-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="0aa9c-204">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0aa9c-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
