---
title: "Sincronización de Azure AD Connect: tareas y consideraciones operativas | Microsoft Docs"
description: "En este tema se describen las tareas operativas de la sincronización de Azure AD Connect y cómo prepararse para utilizar este componente."
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
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="a49b8-103">Sincronización de Azure AD Connect: tareas y consideraciones operativas</span><span class="sxs-lookup"><span data-stu-id="a49b8-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="a49b8-104">El objetivo de este tema es describir las tareas operativas de la sincronización de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a49b8-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="a49b8-105">Modo provisional</span><span class="sxs-lookup"><span data-stu-id="a49b8-105">Staging mode</span></span>
<span data-ttu-id="a49b8-106">Se puede usar el modo provisional para distintos escenarios como:</span><span class="sxs-lookup"><span data-stu-id="a49b8-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="a49b8-107">Alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a49b8-107">High availability.</span></span>
* <span data-ttu-id="a49b8-108">Prueba e implementación de nuevos cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="a49b8-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="a49b8-109">Introducción de un nuevo servidor y baja del antiguo.</span><span class="sxs-lookup"><span data-stu-id="a49b8-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="a49b8-110">Con un servidor en modo provisional puede realizar cambios en la configuración y obtener una vista previa de los cambios antes de activar el servidor.</span><span class="sxs-lookup"><span data-stu-id="a49b8-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="a49b8-111">También permite ejecutar una importación y sincronización completas para comprobar que se esperan todos los cambios antes de realizarlos en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a49b8-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="a49b8-112">Durante la instalación puede seleccionar que el servidor esté en **modo provisional**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="a49b8-113">Esta acción activará el servidor para la importación y sincronización, pero no realizará ninguna exportación.</span><span class="sxs-lookup"><span data-stu-id="a49b8-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="a49b8-114">Un servidor en modo provisional no ejecutará la sincronización de contraseñas ni habilitará la escritura diferida de contraseñas, aunque se seleccionen estas características durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="a49b8-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="a49b8-115">Cuando se deshabilita el modo provisional, el servidor iniciará la exportación, y habilitará la sincronización de contraseñas y la escritura diferida de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="a49b8-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="a49b8-116">Todavía puede forzar una exportación mediante el administrador del servicio de sincronización.</span><span class="sxs-lookup"><span data-stu-id="a49b8-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="a49b8-117">Un servidor en modo provisional seguirá recibiendo cambios de Active Directory y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a49b8-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="a49b8-118">Siempre tendrá una copia de los cambios más recientes y podrá asumir muy rápidamente las responsabilidades de otro servidor.</span><span class="sxs-lookup"><span data-stu-id="a49b8-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="a49b8-119">Si realiza cambios de configuración en el servidor principal, es su responsabilidad realizar los mismos cambios en el servidor o servidores en modo provisional.</span><span class="sxs-lookup"><span data-stu-id="a49b8-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="a49b8-120">Para aquellos con conocimientos de tecnologías de sincronización anteriores, el modo provisional es diferente, ya que el servidor tiene su propia base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a49b8-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="a49b8-121">Esta arquitectura permite que el servidor en modo provisional se encuentre en otro centro de datos.</span><span class="sxs-lookup"><span data-stu-id="a49b8-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="a49b8-122">Comprobación de la configuración de un servidor</span><span class="sxs-lookup"><span data-stu-id="a49b8-122">Verify the configuration of a server</span></span>
<span data-ttu-id="a49b8-123">Para aplicar este método, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a49b8-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="a49b8-124">Preparación</span><span class="sxs-lookup"><span data-stu-id="a49b8-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="a49b8-125">Configuración</span><span class="sxs-lookup"><span data-stu-id="a49b8-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="a49b8-126">Importación y sincronización</span><span class="sxs-lookup"><span data-stu-id="a49b8-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="a49b8-127">Verify</span><span class="sxs-lookup"><span data-stu-id="a49b8-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="a49b8-128">Cambio de servidor activo</span><span class="sxs-lookup"><span data-stu-id="a49b8-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="a49b8-129">Preparación</span><span class="sxs-lookup"><span data-stu-id="a49b8-129">Prepare</span></span>
1. <span data-ttu-id="a49b8-130">Instale Azure AD Connect, seleccione el **modo provisional** y anule la selección de **Iniciar la sincronización** en la última página del Asistente para instalación.</span><span class="sxs-lookup"><span data-stu-id="a49b8-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="a49b8-131">Esto permitirá ejecutar el motor de sincronización de forma manual.</span><span class="sxs-lookup"><span data-stu-id="a49b8-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="a49b8-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="a49b8-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="a49b8-133">Cierre o inicie la sesión y, en el menú de inicio, seleccione **Servicio de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="a49b8-134">Configuración</span><span class="sxs-lookup"><span data-stu-id="a49b8-134">Configuration</span></span>
<span data-ttu-id="a49b8-135">Si ha realizado cambios personalizados en el servidor principal y desea comparar la configuración con el servidor de almacenamiento provisional, utilice el [documentador de configuración de Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="a49b8-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="a49b8-136">Importación y sincronización</span><span class="sxs-lookup"><span data-stu-id="a49b8-136">Import and Synchronize</span></span>
1. <span data-ttu-id="a49b8-137">Seleccione **Conectores** y elija el primer conector de tipo **Active Directory Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="a49b8-138">Haga clic en **Ejecutar** y seleccione **Importación completa** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="a49b8-139">Realice estos pasos para todos los conectores de este tipo.</span><span class="sxs-lookup"><span data-stu-id="a49b8-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="a49b8-140">Seleccione el conector de tipo **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="a49b8-141">Haga clic en **Ejecutar** y seleccione **Importación completa** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="a49b8-142">Asegúrese de que sigue seleccionada la pestaña Conectores.</span><span class="sxs-lookup"><span data-stu-id="a49b8-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="a49b8-143">Para cada conector de tipo **Active Directory Domain Services**, haga clic en **Ejecutar**, y seleccione **Sincronización diferencial** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="a49b8-144">Seleccione el conector de tipo **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="a49b8-145">Haga clic en **Ejecutar**, seleccione **Sincronización diferencial** y, después, **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="a49b8-146">Ahora ha almacenado provisionalmente los cambios de exportación en Azure AD y AD local (si está usando la implementación híbrida de Exchange).</span><span class="sxs-lookup"><span data-stu-id="a49b8-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="a49b8-147">Los siguientes pasos le permiten inspeccionar lo que está a punto de cambiar antes de que comience realmente la exportación a los directorios.</span><span class="sxs-lookup"><span data-stu-id="a49b8-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="a49b8-148">Verify</span><span class="sxs-lookup"><span data-stu-id="a49b8-148">Verify</span></span>
1. <span data-ttu-id="a49b8-149">Inicie un símbolo del sistema y vaya a `%ProgramFiles%\Microsoft Azure AD Sync\bin`.</span><span class="sxs-lookup"><span data-stu-id="a49b8-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="a49b8-150">Ejecute: `csexport "Name of Connector" %temp%\export.xml /f:x` El nombre del conector puede encontrarse en el Servicio de sincronización.</span><span class="sxs-lookup"><span data-stu-id="a49b8-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="a49b8-151">Tendrá un nombre similar a contoso.com – AAD en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a49b8-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="a49b8-152">Copie el script de PowerShell de la sección [CSAnalyzer](#appendix-csanalyzer) en un archivo denominado "`csanalyzer.ps1`".</span><span class="sxs-lookup"><span data-stu-id="a49b8-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="a49b8-153">Abra una ventana de PowerShell y vaya a la carpeta donde se creó el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a49b8-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="a49b8-154">Ejecute `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="a49b8-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="a49b8-155">Ahora tiene un archivo denominado "**processedusers1.csv**" que se puede examinar en Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="a49b8-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="a49b8-156">Todos los cambios almacenados provisionalmente para ser exportada en Azure AD se encuentran en este archivo.</span><span class="sxs-lookup"><span data-stu-id="a49b8-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="a49b8-157">Realice los cambios necesarios en los datos o la configuración y ejecute estos pasos de nuevo (Importación y sincronización y Comprobación) hasta que se esperen los cambios que se van a exportar.</span><span class="sxs-lookup"><span data-stu-id="a49b8-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="a49b8-158">Cambio de servidor activo</span><span class="sxs-lookup"><span data-stu-id="a49b8-158">Switch active server</span></span>
1. <span data-ttu-id="a49b8-159">En el servidor actualmente activo, desactive el servidor (DirSync/FIM/Azure AD Sync) para que no exporte a Azure AD o establézcalo en modo provisional (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="a49b8-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="a49b8-160">Ejecute el Asistente para instalación en el servidor en **modo provisional** y deshabilite el **modo provisional**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="a49b8-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="a49b8-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="a49b8-162">Recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="a49b8-162">Disaster recovery</span></span>
<span data-ttu-id="a49b8-163">Parte del diseño de implementación es planear qué hacer en caso de que se produzca un desastre en el que se pierda el servidor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="a49b8-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="a49b8-164">Hay diferentes modelos de uso y cuál es el que se debe usar dependerá de varios factores como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a49b8-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="a49b8-165">¿Cuál es su grado de tolerancia por no ser capaz de realizar cambios en objetos en Azure AD durante el tiempo de inactividad?</span><span class="sxs-lookup"><span data-stu-id="a49b8-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="a49b8-166">Si usa la sincronización de contraseñas, ¿aceptarán los usuarios que tienen que usar la antigua contraseña en Azure AD en caso de que la cambien de forma local?</span><span class="sxs-lookup"><span data-stu-id="a49b8-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="a49b8-167">¿Tiene una dependencia en operaciones en tiempo real, como la escritura diferida de contraseñas?</span><span class="sxs-lookup"><span data-stu-id="a49b8-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="a49b8-168">En función de las respuestas a estas preguntas y de la directiva de su organización, puede implementar una de las estrategias siguientes:</span><span class="sxs-lookup"><span data-stu-id="a49b8-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="a49b8-169">Recompilación si es necesario.</span><span class="sxs-lookup"><span data-stu-id="a49b8-169">Rebuild when needed.</span></span>
* <span data-ttu-id="a49b8-170">Servidor en espera de reserva, conocido como **modo provisional**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="a49b8-171">Uso de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a49b8-171">Use virtual machines.</span></span>

<span data-ttu-id="a49b8-172">Si no utiliza la base de datos de SQL Express integrada, también debe revisar la sección sobre [alta disponibilidad de SQL](#sql-high-availability) .</span><span class="sxs-lookup"><span data-stu-id="a49b8-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="a49b8-173">Recompilación si es necesario</span><span class="sxs-lookup"><span data-stu-id="a49b8-173">Rebuild when needed</span></span>
<span data-ttu-id="a49b8-174">Una estrategia viable es planear una recompilación del servidor si es necesario.</span><span class="sxs-lookup"><span data-stu-id="a49b8-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="a49b8-175">Normalmente, la instalación del motor de sincronización y la realización de la importación y sincronización iniciales se pueden completar en unas pocas horas.</span><span class="sxs-lookup"><span data-stu-id="a49b8-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="a49b8-176">Si no hay un servidor de reserva disponible, es posible usar temporalmente un controlador de dominio para hospedar el motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="a49b8-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="a49b8-177">El servidor del motor de sincronización no almacena ningún estado acerca de los objetos, por lo que se puede recompilar la base de datos a partir de los datos de Active Directory y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a49b8-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="a49b8-178">El atributo **sourceAnchor** se usa para unir los objetos de local y de la nube.</span><span class="sxs-lookup"><span data-stu-id="a49b8-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="a49b8-179">Si recompila el servidor con objetos existentes locales y en la nube, el motor de sincronización los hará coincidir de nuevo en la reinstalación.</span><span class="sxs-lookup"><span data-stu-id="a49b8-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="a49b8-180">Las acciones que necesita documentar y guardar son los cambios de configuración realizados en el servidor, como reglas de filtrado y de sincronización.</span><span class="sxs-lookup"><span data-stu-id="a49b8-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="a49b8-181">Estas configuraciones personalizadas deben volver a aplicarse antes de iniciar la sincronización.</span><span class="sxs-lookup"><span data-stu-id="a49b8-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="a49b8-182">Servidor en espera de reserva - modo provisional</span><span class="sxs-lookup"><span data-stu-id="a49b8-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="a49b8-183">Si tiene un entorno más complejo, se recomienda tener uno o más servidores en espera.</span><span class="sxs-lookup"><span data-stu-id="a49b8-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="a49b8-184">Durante la instalación puede habilitar un servidor que esté en **modo provisional**.</span><span class="sxs-lookup"><span data-stu-id="a49b8-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="a49b8-185">Para obtener más información, consulte [Modo provisional](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="a49b8-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="a49b8-186">Uso de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a49b8-186">Use virtual machines</span></span>
<span data-ttu-id="a49b8-187">Un método común y admitido es ejecutar el motor de sincronización en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a49b8-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="a49b8-188">En caso de que el host tenga un problema, la imagen con el servidor del motor de sincronización se puede migrar a otro servidor.</span><span class="sxs-lookup"><span data-stu-id="a49b8-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="a49b8-189">alta disponibilidad de SQL</span><span class="sxs-lookup"><span data-stu-id="a49b8-189">SQL High Availability</span></span>
<span data-ttu-id="a49b8-190">Si no utiliza la versión de SQL Server Express que se incluye con Azure AD Connect, también debe tener en cuenta la alta disponibilidad para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a49b8-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="a49b8-191">Las soluciones de alta disponibilidad compatibles incluyen la agrupación en clústeres de SQL y AOA (Grupos de disponibilidad AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="a49b8-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="a49b8-192">Entre las soluciones no admitidas se incluye la creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="a49b8-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="a49b8-193">Se agregó la compatibilidad de AOA de SQL a Azure AD Connect en la versión 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="a49b8-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="a49b8-194">Debe habilitar AOA de SQL antes de instalar Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a49b8-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="a49b8-195">Durante la instalación, Azure AD Connect detecta si la instancia de SQL proporcionada está habilitada para AOA de SQL o no.</span><span class="sxs-lookup"><span data-stu-id="a49b8-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="a49b8-196">Si AOA de SQL está habilitada, Azure AD Connect averigua si AOA de SQL está configurada para usar la replicación sincrónica o asincrónica.</span><span class="sxs-lookup"><span data-stu-id="a49b8-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="a49b8-197">Cuando configure la escucha de grupo de disponibilidad, se recomienda que establezca la propiedad RegisterAllProvidersIP en 0.</span><span class="sxs-lookup"><span data-stu-id="a49b8-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="a49b8-198">Esto se debe a que Azure AD Connect actualmente usa SQL Native Client para conectarse a SQL y SQL Native Client no admite el uso de la propiedad MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="a49b8-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="a49b8-199">Apéndice: CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="a49b8-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="a49b8-200">Vea la sección de [comprobación](#verify) sobre cómo usar este script.</span><span class="sxs-lookup"><span data-stu-id="a49b8-200">See the section [verify](#verify) on how to use this script.</span></span>

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

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
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

    #now that we have the basics, go get the details

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

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="a49b8-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a49b8-201">Next steps</span></span>
<span data-ttu-id="a49b8-202">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="a49b8-202">**Overview topics**</span></span>  

* [<span data-ttu-id="a49b8-203">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="a49b8-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="a49b8-204">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a49b8-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
