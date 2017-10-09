---
title: problemas de Data Management Gateway aaaTroubleshoot | Documentos de Microsoft
description: Proporciona sugerencias tootroubleshoot problemas relacionados tooData Management Gateway.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="4e597-103">Solución de problemas con Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="4e597-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="4e597-104">En este artículo se ofrece información sobre la solución de problemas con Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4e597-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="4e597-105">Vea hello [Data Management Gateway](data-factory-data-management-gateway.md) artículo para obtener información detallada acerca de la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="4e597-106">Vea hello [mover datos entre local y nube](data-factory-move-data-between-onprem-and-cloud.md) artículo para ver un tutorial de mover datos desde una base de datos de SQL Server local tooMicrosoft almacenamiento de blobs de Azure mediante el uso de la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="4e597-107">Puerta de enlace tooinstall o registrar errores</span><span class="sxs-lookup"><span data-stu-id="4e597-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="4e597-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-108">1. Problem</span></span>
<span data-ttu-id="4e597-109">Verá este mensaje de error al instalar y registrar una puerta de enlace, en concreto, al descargar el archivo de instalación de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="4e597-110">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-110">Cause</span></span>
<span data-ttu-id="4e597-111">máquina de Hello en el que está tratando de puerta de enlace de hello tooinstall error en archivo de instalación puerta de enlace más reciente de toodownload de hello desde centro de descarga de hello debido tooa problema de red.</span><span class="sxs-lookup"><span data-stu-id="4e597-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-112">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-112">Resolution</span></span>
<span data-ttu-id="4e597-113">Compruebe su toosee de configuración del servidor de proxy de firewall si configuración de hello bloquea la conexión de red de Hola de hello equipo toohello [centro de descarga de](https://download.microsoft.com/)y actualizar la configuración de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="4e597-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="4e597-114">Como alternativa, puede descargar archivo de instalación de hello para puerta de enlace más reciente de Hola de hello [centro de descarga de](https://www.microsoft.com/download/details.aspx?id=39717) en otros equipos que pueden tener acceso a centro de descarga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="4e597-115">También puede, a continuación, puerta de enlace de copia Hola instalador archivo toohello equipo host y ejecutarlo manualmente puerta de enlace de hello tooinstall y actualización.</span><span class="sxs-lookup"><span data-stu-id="4e597-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="4e597-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-116">2. Problem</span></span>
<span data-ttu-id="4e597-117">Verá este error al tratar de tooinstall una puerta de enlace, haga clic en **instalar directamente en este equipo** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e597-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="4e597-118">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-118">Cause</span></span>
<span data-ttu-id="4e597-119">Una puerta de enlace ya está instalado en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-120">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-120">Resolution</span></span>
<span data-ttu-id="4e597-121">Desinstalar Hola puerta de enlace existente en la máquina de Hola y haga clic en hello **instalar directamente en este equipo** volver a vincular.</span><span class="sxs-lookup"><span data-stu-id="4e597-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="4e597-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-122">3. Problem</span></span>
<span data-ttu-id="4e597-123">Puede que vea este error al registrar una nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="4e597-124">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-124">Cause</span></span>
<span data-ttu-id="4e597-125">Podría aparecer este mensaje para uno de hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="4e597-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="4e597-126">Hola formato de clave de puerta de enlace de hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="4e597-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="4e597-127">se ha invalidado la clave de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="4e597-128">se ha vuelto generar clave de puerta de enlace de Hola desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="4e597-129">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-129">Resolution</span></span>
<span data-ttu-id="4e597-130">Compruebe si está utilizando la clave de puerta de enlace correcto de Hola desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="4e597-131">Si es necesario, volver a generar una clave y usar puerta de enlace de hello tooregister clave Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="4e597-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-132">4. Problem</span></span>
<span data-ttu-id="4e597-133">Es posible que vea Hola siguiente mensaje de error cuando se está registrando una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Contenido o formato de la clave no son válidos](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="4e597-135">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-135">Cause</span></span>
<span data-ttu-id="4e597-136">Hello contenido o el formato de clave de puerta de enlace de entrada de hello es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="4e597-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="4e597-137">Uno de los motivos de hello puede ser que solo una parte de la clave de Hola que copió desde el portal de Hola o si está usando una clave no válida.</span><span class="sxs-lookup"><span data-stu-id="4e597-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-138">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-138">Resolution</span></span>
<span data-ttu-id="4e597-139">Generar una clave de puerta de enlace en el portal de Hola y usar Hola copia toocopy botón Hola clave todo.</span><span class="sxs-lookup"><span data-stu-id="4e597-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="4e597-140">A continuación, péguelo en esta puerta de enlace de ventana tooregister Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="4e597-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-141">5. Problem</span></span>
<span data-ttu-id="4e597-142">Es posible que vea Hola siguiente mensaje de error cuando se está registrando una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![La clave de la puerta de enlace no es válida o está vacía](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="4e597-144">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-144">Cause</span></span>
<span data-ttu-id="4e597-145">se ha vuelto generar clave de puerta de enlace de Hola o se ha eliminado la puerta de enlace de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e597-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="4e597-146">También puede ocurrir si el programa de instalación de Data Management Gateway de hello no es más reciente.</span><span class="sxs-lookup"><span data-stu-id="4e597-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-147">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-147">Resolution</span></span>
<span data-ttu-id="4e597-148">Compruebe si el programa de instalación de Data Management Gateway de hello es la versión más reciente de hello, puede encontrar la versión más reciente de Hola en hello Microsoft [centro de descarga de](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="4e597-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="4e597-149">Si el programa de instalación es actual / más reciente y puerta de enlace sigue existiendo en el Portal, regenerar la clave de puerta de enlace de Hola Hola portal de Azure y usar Hola copia toocopy botón Hola clave completa y, a continuación, péguelo en esta puerta de enlace de ventana tooregister Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="4e597-150">En caso contrario, vuelva a crear la puerta de enlace de Hola y empezar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4e597-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="4e597-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-151">6. Problem</span></span>
<span data-ttu-id="4e597-152">Es posible que vea Hola siguiente mensaje de error cuando se está registrando una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![La clave de la puerta de enlace no es válida o está vacía](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="4e597-154">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-154">Cause</span></span>
<span data-ttu-id="4e597-155">Este error puede ocurrir porque se ha eliminado la puerta de enlace de Hola o se ha vuelto generar clave de puerta de enlace asociada Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-156">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-156">Resolution</span></span>
<span data-ttu-id="4e597-157">Si se ha eliminado la puerta de enlace de hello, volver a crear la puerta de enlace de Hola desde el portal de hello, haga clic en **registrar**, copie la clave de Hola desde el portal de hello, péguelo e intente puerta de enlace de tooregister Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="4e597-158">Si la puerta de enlace de hello sigue existiendo, pero se ha vuelto generar su clave, utilice Hola nueva clave tooregister Hola puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="4e597-159">Si no tiene clave hello, Regenerar clave de hello nuevo desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="4e597-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-160">7. Problem</span></span>
<span data-ttu-id="4e597-161">Cuando se está registrando una puerta de enlace, podría necesitar tooenter ruta de acceso y una contraseña para un certificado.</span><span class="sxs-lookup"><span data-stu-id="4e597-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="4e597-163">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-163">Cause</span></span>
<span data-ttu-id="4e597-164">se ha registrado la puerta de enlace de Hello en otras máquinas antes.</span><span class="sxs-lookup"><span data-stu-id="4e597-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="4e597-165">Durante el registro inicial de Hola de una puerta de enlace, un certificado de cifrado se ha asociado con la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="4e597-166">certificado de Hello puede generado automáticamente por puerta de enlace de Hola o proporcionado por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="4e597-167">Este certificado es tooencrypt usa credenciales Hola del almacén de datos (servicio vinculado).</span><span class="sxs-lookup"><span data-stu-id="4e597-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Exportación de certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="4e597-169">Al restaurar puerta de enlace de hello en otra máquina, solicita el Asistente para registro de hello para este certificado toodecrypt credenciales previamente cifrado con este certificado.</span><span class="sxs-lookup"><span data-stu-id="4e597-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="4e597-170">Sin este certificado, no puede descifrar las credenciales de hello nueva puerta de enlace de Hola y se producirá un error en las ejecuciones de actividad de copia posteriores asociadas a esta nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="4e597-171">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-171">Resolution</span></span>
<span data-ttu-id="4e597-172">Si ha exportado certificado de credencial de Hola de máquina de puerta de enlace de hello original mediante el uso de hello **exportar** botón en hello **configuración** del Administrador de configuración de Data Management Gateway, utilice Hola certificado aquí.</span><span class="sxs-lookup"><span data-stu-id="4e597-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="4e597-173">No puede omitir esta fase al recuperar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="4e597-174">Si falta el certificado de hello, puerta de enlace de toodelete Hola desde el portal de hello es necesario y volver a crear una nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="4e597-175">Además, actualice todos los servicios vinculados que están relacionados toohello puerta de enlace, volver a escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="4e597-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="4e597-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-176">8. Problem</span></span>
<span data-ttu-id="4e597-177">Es posible que vea Hola siguiente mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="4e597-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="4e597-178">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-178">Cause</span></span>
<span data-ttu-id="4e597-179">Este error se produce cuando la puerta de enlace está en un entorno que requiere una tooaccess de proxy HTTP recursos de Internet, o se cambia la contraseña de autenticación del servidor de proxy pero no se actualiza en consecuencia en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-180">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-180">Resolution</span></span>
<span data-ttu-id="4e597-181">Siga las instrucciones de Hola Hola [consideraciones acerca del servidor Proxy](#proxy-server-considerations) sección de este artículo y configurar el proxy del Administrador de configuración con Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4e597-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="4e597-182">La puerta de enlace está en línea con funcionalidad limitada</span><span class="sxs-lookup"><span data-stu-id="4e597-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="4e597-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-183">1. Problem</span></span>
<span data-ttu-id="4e597-184">Ver estado de Hola de puerta de enlace de hello como en línea con una funcionalidad limitada.</span><span class="sxs-lookup"><span data-stu-id="4e597-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="4e597-185">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-185">Cause</span></span>
<span data-ttu-id="4e597-186">Ver estado de Hola de puerta de enlace de hello en línea con una funcionalidad limitada para uno de hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="4e597-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="4e597-187">Puerta de enlace no puede conectar toocloud servicio a través de Service Bus de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e597-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="4e597-188">Servicio de nube no puede conectar toogateway a través del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="4e597-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="4e597-189">Cuando la puerta de enlace de hello está en línea con una funcionalidad limitada, no es posible que toouse pueda Hola Asistente para copiar de factoría de datos toocreate las canalizaciones de datos para copiar datos tooor de almacenes de datos local.</span><span class="sxs-lookup"><span data-stu-id="4e597-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="4e597-190">Como alternativa, puede usar el Editor de generador de datos en el portal de hello, Visual Studio o PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e597-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-191">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-191">Resolution</span></span>
<span data-ttu-id="4e597-192">Resolución de este problema (en línea con una funcionalidad limitada) se basa en que no se puede conectar el servicio de nube toohello u Hola otra forma de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="4e597-193">Hola las secciones siguientes proporciona estas soluciones.</span><span class="sxs-lookup"><span data-stu-id="4e597-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="4e597-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-194">2. Problem</span></span>
<span data-ttu-id="4e597-195">Vea Hola siguiente error.</span><span class="sxs-lookup"><span data-stu-id="4e597-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Puerta de enlace no puede conectar el servicio de toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="4e597-197">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-197">Cause</span></span>
<span data-ttu-id="4e597-198">Puerta de enlace no puede conectar el servicio en la nube toohello a través del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="4e597-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-199">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-199">Resolution</span></span>
<span data-ttu-id="4e597-200">Siga estos pasos tooget Hola puerta de enlace en línea:</span><span class="sxs-lookup"><span data-stu-id="4e597-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="4e597-201">Permitir que las reglas de salida en la máquina de puerta de enlace de Hola y el firewall corporativo de Hola de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="4e597-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="4e597-202">Puede encontrar direcciones IP de registro de eventos de Windows hello (Id. de == 401): fue un intento realizado tooaccess un socket de una manera prohibida por los permisos de acceso XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="4e597-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="4e597-203">Configurar el proxy de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="4e597-204">Vea hello [consideraciones acerca del servidor Proxy](#proxy-server-considerations) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4e597-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="4e597-205">Habilitar los puertos de salida 5671 y 9350-9354 en ambos Hola Firewall de Windows en la máquina de puerta de enlace de Hola y el firewall corporativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="4e597-206">Vea hello [puertos y firewall](#ports-and-firewall) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4e597-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="4e597-207">Este paso es opcional, pero se recomienda por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="4e597-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="4e597-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-208">3. Problem</span></span>
<span data-ttu-id="4e597-209">Vea Hola siguiente error.</span><span class="sxs-lookup"><span data-stu-id="4e597-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="4e597-210">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-210">Cause</span></span>
<span data-ttu-id="4e597-211">Un error transitorio en la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="4e597-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-212">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-212">Resolution</span></span>
<span data-ttu-id="4e597-213">Siga estos pasos tooget Hola puerta de enlace en línea:</span><span class="sxs-lookup"><span data-stu-id="4e597-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="4e597-214">Espere unos minutos, conectividad de Hola se podrán recuperar automáticamente al error de hello ha desaparecido.</span><span class="sxs-lookup"><span data-stu-id="4e597-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="4e597-215">Si Hola error persiste, reinicie el servicio de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="4e597-216">Servicio de tooauthor errores vinculado</span><span class="sxs-lookup"><span data-stu-id="4e597-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="4e597-217">Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-217">Problem</span></span>
<span data-ttu-id="4e597-218">Puede ver este error cuando intente toouse Administrador de credenciales en credenciales de hello tooinput portal para un nuevo servicio vinculado, o actualizar las credenciales para un servicio vinculado existente.</span><span class="sxs-lookup"><span data-stu-id="4e597-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="4e597-219">Cuando aparece este error, página de configuración de hello del Administrador de configuración de Data Management Gateway sería Hola siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="4e597-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![No se puede establecer conexión con la base de datos](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="4e597-221">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-221">Cause</span></span>
<span data-ttu-id="4e597-222">certificado SSL de Hola se podría haber perdido en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="4e597-223">equipo de puerta de enlace de Hello no puede cargar el certificado de hello actualmente que se usa para el cifrado SSL.</span><span class="sxs-lookup"><span data-stu-id="4e597-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="4e597-224">También puede ver un mensaje de error en registro de eventos de hello es similar toohello siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="4e597-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="4e597-225">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-225">Resolution</span></span>
<span data-ttu-id="4e597-226">Siga estos pasos toosolve problema de hello:</span><span class="sxs-lookup"><span data-stu-id="4e597-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="4e597-227">Inicie el Administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="4e597-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="4e597-228">Cambiar toohello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="4e597-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="4e597-229">Haga clic en hello **cambio** certificado SSL de botón toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Botón Cambiar certificado](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="4e597-231">Seleccione un nuevo certificado como certificado SSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="4e597-232">Puede usar cualquier certificado SSL que haya generado por su cuenta o que haya generado una organización.</span><span class="sxs-lookup"><span data-stu-id="4e597-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="4e597-234">Error en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="4e597-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="4e597-235">Problema</span><span class="sxs-lookup"><span data-stu-id="4e597-235">Problem</span></span>
<span data-ttu-id="4e597-236">Quizás haya notado Hola después de un error "UserErrorFailedToConnectToSqlserver" después de configurar una canalización en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="4e597-237">Causa</span><span class="sxs-lookup"><span data-stu-id="4e597-237">Cause</span></span>
<span data-ttu-id="4e597-238">Esto puede ocurrir por diferentes motivos y la mitigación varía según la causa.</span><span class="sxs-lookup"><span data-stu-id="4e597-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="4e597-239">Resolución</span><span class="sxs-lookup"><span data-stu-id="4e597-239">Resolution</span></span>
<span data-ttu-id="4e597-240">Permitir las conexiones TCP salientes en el puerto TCP/1433 en hello cliente de Data Management Gateway antes de conectar la base de datos SQL tooan.</span><span class="sxs-lookup"><span data-stu-id="4e597-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="4e597-241">Si la base de datos de destino de hello es una base de datos de SQL Azure, comprobar SQL Server configuración de firewall de Azure también.</span><span class="sxs-lookup"><span data-stu-id="4e597-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="4e597-242">Vea Hola después de almacén de datos local de sección tootest Hola conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="4e597-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="4e597-243">Errores relacionados con la conexión al almacén de datos o con los controladores</span><span class="sxs-lookup"><span data-stu-id="4e597-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="4e597-244">Si ve datos almacenar conexión o errores relacionados con el controlador, complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4e597-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="4e597-245">Inicie el Administrador de configuración de Data Management Gateway en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="4e597-246">Cambiar toohello **diagnósticos** ficha.</span><span class="sxs-lookup"><span data-stu-id="4e597-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="4e597-247">En **Probar conexión**, agregar valores de grupo de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="4e597-248">Haga clic en **prueba** toosee si se puede conectar toohello local origen de datos de la máquina de puerta de enlace de hello usando información de conexión de Hola y credenciales.</span><span class="sxs-lookup"><span data-stu-id="4e597-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="4e597-249">Si la conexión de prueba de hello sigue sin funciona después de instalar un controlador, reinicio Hola puerta de enlace para el mismo toopick cambio más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Prueba de conexión en la pestaña Diagnósticos](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="4e597-251">Registros de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="4e597-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="4e597-252">Enviar tooMicrosoft de registros de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="4e597-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="4e597-253">Cuando se comunique con Microsoft Support tooget ayuda para solucionar problemas de la puerta de enlace, que se le pida tooshare los registros de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4e597-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="4e597-254">Con la versión de Hola de puerta de enlace de hello, puede compartir los registros de puerta de enlace necesaria con dos clics del botón del Administrador de configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4e597-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="4e597-255">Cambiar toohello **diagnósticos** ficha del Administrador de configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4e597-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Pestaña Diagnóstico de la puerta de enlace de administración de datos](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="4e597-257">Haga clic en **enviar registros** hello toosee después el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e597-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Puerta de enlace de administración de datos: Enviar registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="4e597-259">(Opcional) Haga clic en **ver registros** tooreview inicia sesión en el Visor de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="4e597-260">(Opcional) Haga clic en **privacidad** declaración de privacidad de los servicios web de Microsoft tooreview.</span><span class="sxs-lookup"><span data-stu-id="4e597-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="4e597-261">Cuando esté satisfecho con lo que está a punto de tooupload, haga clic en **enviar registros** tooactually enviar registros de Hola desde Hola últimos siete días tooMicrosoft para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="4e597-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="4e597-262">Debería ver estado de Hola de operación de registros de envío de hello tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Puerta de enlace de administración de datos: Estado del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="4e597-264">Una vez completada la operación de hello, verá un cuadro de diálogo como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Puerta de enlace de administración de datos: Estado del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="4e597-266">Guardar hello **ID informe** y compartirlo con Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="4e597-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="4e597-267">Id. de informe de Hello es registros de puerta de enlace de hello toolocate usado que ha cargado para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="4e597-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="4e597-268">Id. de informe de Hello también se guarda en el Visor de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="4e597-269">Puede buscar examinando Hola de Id. de evento "25" y comprobar Hola fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="4e597-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Puerta de enlace de administración de datos: Identificador de informe del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="4e597-271">Archivar registros de puerta de enlace en el equipo host de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="4e597-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="4e597-272">Hay veces en las que existen problemas con la puerta de enlace y no es posible compartir los registros de puerta de enlace de forma directa:</span><span class="sxs-lookup"><span data-stu-id="4e597-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="4e597-273">Instalar puerta de enlace de Hola y registrar la puerta de enlace de hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="4e597-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="4e597-274">Intente puerta de enlace de hello tooregister con una nueva clave del Administrador de configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4e597-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="4e597-275">Intente toosend registros y no se puede conectar el servicio de host de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="4e597-276">Para estos escenarios, puede guardar los registros de puerta de enlace como un archivo ZIP y compartirlo cuando pueda ponerse en contacto con el equipo de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e597-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="4e597-277">Por ejemplo, si recibe un error al registrar la puerta de enlace de hello como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Puerta de enlace de administración de datos: Error de registro](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="4e597-279">Haga clic en hello **almacene los registros de puerta de enlace** vinculan tooarchive y guardar los registros y, a continuación, compartir el archivo zip de hello con soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e597-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Puerta de enlace de administración de datos: Archivar registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="4e597-281">Buscar registros de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="4e597-281">Locate gateway logs</span></span>
<span data-ttu-id="4e597-282">Puede encontrar información de registro de puerta de enlace detallada en registros de eventos de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4e597-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="4e597-283">Inicie el **Visor de eventos** de Windows.</span><span class="sxs-lookup"><span data-stu-id="4e597-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="4e597-284">Buscar registros en hello **registros de aplicaciones y servicios** > **Data Management Gateway** carpeta.</span><span class="sxs-lookup"><span data-stu-id="4e597-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="4e597-285">Cuando esté solucionando problemas relacionados con la puerta de enlace, busque eventos de nivel de error en el Visor de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e597-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Puerta de enlace de administración de datos: Registros en el Visor de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
