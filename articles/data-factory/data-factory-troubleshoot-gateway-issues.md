---
title: "Solución de problemas de Data Management Gateway | Microsoft Docs"
description: "Ofrece sugerencias para solucionar problemas relacionados con la puerta de enlace de administración de datos."
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
ms.openlocfilehash: b8e50a4e3c0b9c535ccc2344ff22261a356d5acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="a809d-103">Solución de problemas con Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="a809d-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="a809d-104">En este artículo se ofrece información sobre la solución de problemas con Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a809d-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="a809d-105">Para más información sobre la puerta de enlace, vea el artículo [Puerta de enlace de administración de datos](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a809d-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="a809d-106">En el artículo [Mover datos entre implementaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) puede ver un tutorial sobre cómo mover datos entre una base de datos de SQL Server local a Microsoft Azure Blob Storage con la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="a809d-107">Error al instalar o registrar la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a809d-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="a809d-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-108">1. Problem</span></span>
<span data-ttu-id="a809d-109">Se muestra este mensaje de error al instalar y registrar una puerta de enlace (en concreto, al descargar el archivo de instalación de la puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="a809d-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="a809d-110">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-110">Cause</span></span>
<span data-ttu-id="a809d-111">La máquina donde intenta instalar la puerta de enlace no puede descargar la versión más reciente del archivo de instalación de la puerta de enlace del Centro de descarga debido a un problema de red.</span><span class="sxs-lookup"><span data-stu-id="a809d-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-112">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-112">Resolution</span></span>
<span data-ttu-id="a809d-113">Compruebe si la configuración del firewall o del servidor proxy bloquea la conexión de red desde el equipo al [Centro de descarga](https://download.microsoft.com/) y actualice la configuración según corresponda.</span><span class="sxs-lookup"><span data-stu-id="a809d-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="a809d-114">Como alternativa, puede descargar el archivo de instalación para la puerta de enlace más reciente desde el [centro de descarga](https://www.microsoft.com/download/details.aspx?id=39717) en otros equipos que pueden tener acceso al centro de descarga.</span><span class="sxs-lookup"><span data-stu-id="a809d-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="a809d-115">A continuación, puede copiar el archivo del instalador en el equipo de host de puerta de enlace y ejecutarlo manualmente para instalar y actualizar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="a809d-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-116">2. Problem</span></span>
<span data-ttu-id="a809d-117">Se muestra este error al hacer clic en **Instalar directamente en este equipo** en Azure Portal para intentar instalar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="a809d-118">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-118">Cause</span></span>
<span data-ttu-id="a809d-119">Ya hay instalada una puerta de enlace en la máquina.</span><span class="sxs-lookup"><span data-stu-id="a809d-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-120">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-120">Resolution</span></span>
<span data-ttu-id="a809d-121">Desinstale la puerta de enlace existente en la máquina y vuelva a hacer clic en el vínculo **Instalar directamente en este equipo**.</span><span class="sxs-lookup"><span data-stu-id="a809d-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="a809d-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-122">3. Problem</span></span>
<span data-ttu-id="a809d-123">Puede que vea este error al registrar una nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="a809d-124">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-124">Cause</span></span>
<span data-ttu-id="a809d-125">Puede que vea este mensaje por uno de los motivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a809d-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="a809d-126">El formato de la clave de la puerta de enlace no es válido.</span><span class="sxs-lookup"><span data-stu-id="a809d-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="a809d-127">Se ha invalidado la clave de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="a809d-128">Se ha vuelto a generar la clave de la puerta de enlace desde el portal.</span><span class="sxs-lookup"><span data-stu-id="a809d-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="a809d-129">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-129">Resolution</span></span>
<span data-ttu-id="a809d-130">Compruebe si usa la clave de la puerta de enlace correcta en el portal.</span><span class="sxs-lookup"><span data-stu-id="a809d-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="a809d-131">Si es necesario, vuelva a generar una clave y úsela para registrar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="a809d-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-132">4. Problem</span></span>
<span data-ttu-id="a809d-133">Puede que vea el siguiente mensaje de error al volver a registrar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Contenido o formato de la clave no son válidos](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="a809d-135">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-135">Cause</span></span>
<span data-ttu-id="a809d-136">El contenido o el formato de la clave de la puerta de enlace de entrada no son correctos.</span><span class="sxs-lookup"><span data-stu-id="a809d-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="a809d-137">Uno de los motivos puede ser que haya copiado solo una parte de la clave desde el portal o que esté usando una clave no válida.</span><span class="sxs-lookup"><span data-stu-id="a809d-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-138">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-138">Resolution</span></span>
<span data-ttu-id="a809d-139">Genere una clave de puerta de enlace en el portal y use el botón Copiar para copiar la clave completa.</span><span class="sxs-lookup"><span data-stu-id="a809d-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="a809d-140">A continuación, péguela en esta ventana para registrar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="a809d-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-141">5. Problem</span></span>
<span data-ttu-id="a809d-142">Puede que vea el siguiente mensaje de error al volver a registrar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![La clave de la puerta de enlace no es válida o está vacía](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="a809d-144">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-144">Cause</span></span>
<span data-ttu-id="a809d-145">La clave de la puerta de enlace se ha vuelto a generar o la puerta de enlace se ha eliminado en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a809d-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="a809d-146">También puede ocurrir que el programa de instalación de Data Management Gateway no sea el más reciente.</span><span class="sxs-lookup"><span data-stu-id="a809d-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-147">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-147">Resolution</span></span>
<span data-ttu-id="a809d-148">Compruebe si el programa de instalación de Data Management Gateway es la versión más reciente. Puede encontrar la versión más reciente en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="a809d-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="a809d-149">Si se trata de la versión más reciente o la actual y existe una puerta de enlace en el Portal, vuelva a generar una clave de la puerta de enlace en Azure Portal, use el botón Copiar para copiar la clave entera y, después, péguela en esta ventana para registrar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="a809d-150">En caso contrario, vuelva a crear la puerta de enlace y empiece de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a809d-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="a809d-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-151">6. Problem</span></span>
<span data-ttu-id="a809d-152">Puede que vea el siguiente mensaje de error al volver a registrar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![La clave de la puerta de enlace no es válida o está vacía](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="a809d-154">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-154">Cause</span></span>
<span data-ttu-id="a809d-155">Este error puede producirse porque se ha eliminado la puerta de enlace o porque se ha vuelto generar la clave de la puerta de enlace asociada.</span><span class="sxs-lookup"><span data-stu-id="a809d-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-156">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-156">Resolution</span></span>
<span data-ttu-id="a809d-157">Si se ha eliminado la puerta de enlace, vuelva a crear la puerta de enlace desde el portal, haga clic en **Registrar**, copie la clave desde el portal, péguela y, después, intente registrar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="a809d-158">Si la puerta de enlace aún existe, pero su clave se ha vuelto a generar, use la nueva clave para registrar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="a809d-159">Si no tiene la clave, vuelva a generar la clave desde el portal.</span><span class="sxs-lookup"><span data-stu-id="a809d-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="a809d-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-160">7. Problem</span></span>
<span data-ttu-id="a809d-161">Al registrar una puerta de enlace, es posible que tenga que especificar la ruta de acceso y la contraseña de un certificado.</span><span class="sxs-lookup"><span data-stu-id="a809d-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="a809d-163">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-163">Cause</span></span>
<span data-ttu-id="a809d-164">La puerta de enlace se ha registrado en otras máquinas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a809d-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="a809d-165">Durante el registro inicial de una puerta de enlace se ha asociado un certificado de cifrado con la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="a809d-166">El certificado puede ser generado automáticamente por la puerta de enlace o puede proporcionarlo el usuario.</span><span class="sxs-lookup"><span data-stu-id="a809d-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="a809d-167">Este certificado se usa para cifrar las credenciales del almacén de datos (servicio vinculado).</span><span class="sxs-lookup"><span data-stu-id="a809d-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Exportación de certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="a809d-169">Al restaurar la puerta de enlace en un equipo host distinto, el asistente para registro pide este certificado para descifrar las credenciales que se han cifrado anteriormente con este certificado.</span><span class="sxs-lookup"><span data-stu-id="a809d-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="a809d-170">Sin este certificado, las credenciales no se pueden descifrar con la nueva puerta de enlace y las ejecuciones de actividades de copia posteriores asociadas con esta nueva puerta de enlace producirán errores.</span><span class="sxs-lookup"><span data-stu-id="a809d-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="a809d-171">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-171">Resolution</span></span>
<span data-ttu-id="a809d-172">Si ha exportado el certificado de credenciales desde la máquina de la puerta de enlace original con el botón e **Exportar** de la pestaña **Configuración** del administrador de configuración de la puerta de enlace de administración de datos, use el certificado aquí.</span><span class="sxs-lookup"><span data-stu-id="a809d-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="a809d-173">No puede omitir esta fase al recuperar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="a809d-174">Si falta el certificado, necesitará eliminar la puerta de enlace del portal y volver a crear una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="a809d-175">Además, actualice todos los servicios vinculados relacionados con la puerta de enlace volviendo a escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="a809d-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="a809d-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-176">8. Problem</span></span>
<span data-ttu-id="a809d-177">Puede aparecer el siguiente mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="a809d-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="a809d-178">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-178">Cause</span></span>
<span data-ttu-id="a809d-179">Este error se produce cuando la puerta de enlace se encuentra en un entorno que necesita un proxy HTTP para acceder a recursos de Internet, o bien cuando se cambia la contraseña de autenticación del proxy, pero no se actualiza en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-180">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-180">Resolution</span></span>
<span data-ttu-id="a809d-181">Siga las instrucciones de la sección [Consideraciones sobre el servidor proxy](#proxy-server-considerations) en este artículo y establezca la configuración del proxy con el administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="a809d-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="a809d-182">La puerta de enlace está en línea con funcionalidad limitada</span><span class="sxs-lookup"><span data-stu-id="a809d-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="a809d-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-183">1. Problem</span></span>
<span data-ttu-id="a809d-184">El estado de la puerta de enlace es en línea con funciones limitadas.</span><span class="sxs-lookup"><span data-stu-id="a809d-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="a809d-185">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-185">Cause</span></span>
<span data-ttu-id="a809d-186">El estado de la puerta de enlace es "en línea con funciones limitadas" por uno de los motivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a809d-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="a809d-187">La puerta de enlace no se puede conectar al servicio en la nube mediante Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a809d-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="a809d-188">El servicio en la nube no se puede conectar a la puerta de enlace mediante Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a809d-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="a809d-189">Cuando la puerta de enlace está en línea con funcionalidad limitada, no podrá usar el Asistente para copia de Data Factory para crear canalizaciones de datos entre almacenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="a809d-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="a809d-190">Como alternativa, puede usar Data Factory Editor en el portal, Visual Studio o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a809d-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-191">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-191">Resolution</span></span>
<span data-ttu-id="a809d-192">La solución a este problema (en línea con funciones limitadas) depende de si la puerta de enlace se puede conectar al servicio en la nube o viceversa.</span><span class="sxs-lookup"><span data-stu-id="a809d-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="a809d-193">En las secciones siguientes se describen estas soluciones.</span><span class="sxs-lookup"><span data-stu-id="a809d-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="a809d-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-194">2. Problem</span></span>
<span data-ttu-id="a809d-195">Verá este error.</span><span class="sxs-lookup"><span data-stu-id="a809d-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![La puerta de enlace no se puede conectar al servicio en la nube](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="a809d-197">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-197">Cause</span></span>
<span data-ttu-id="a809d-198">La puerta de enlace no se puede conectar al servicio en la nube mediante Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a809d-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-199">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-199">Resolution</span></span>
<span data-ttu-id="a809d-200">Siga estos pasos para poner en línea la puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="a809d-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="a809d-201">Permita reglas de salida de direcciones IP en la máquina de la puerta de enlace y en el firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="a809d-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="a809d-202">Encontrará las direcciones IP en el Registro de eventos de Windows (id. == 401): intento de acceso a un socket no permitido por sus permisos de acceso XX.XX.XX.XX:9350.</span><span class="sxs-lookup"><span data-stu-id="a809d-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="a809d-203">Configure los valores de proxy en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="a809d-204">Consulte la sección [Consideraciones sobre el servidor proxy](#proxy-server-considerations) para más información.</span><span class="sxs-lookup"><span data-stu-id="a809d-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="a809d-205">Habilite los puertos de salida 5671 y 9350-9354 en el Firewall de Windows de la máquina de la puerta de enlace y en el firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="a809d-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="a809d-206">Consulte la sección [Puertos y firewall](#ports-and-firewall) para más información.</span><span class="sxs-lookup"><span data-stu-id="a809d-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="a809d-207">Este paso es opcional, pero se recomienda por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a809d-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="a809d-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-208">3. Problem</span></span>
<span data-ttu-id="a809d-209">Verá este error.</span><span class="sxs-lookup"><span data-stu-id="a809d-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="a809d-210">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-210">Cause</span></span>
<span data-ttu-id="a809d-211">Un error transitorio en la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="a809d-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-212">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-212">Resolution</span></span>
<span data-ttu-id="a809d-213">Siga estos pasos para poner en línea la puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="a809d-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="a809d-214">Espere un par de minutos; la conectividad se recuperará automáticamente cuando desaparezca el error.</span><span class="sxs-lookup"><span data-stu-id="a809d-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="a809d-215">Si el error persiste, reinicie el servicio de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="a809d-216">Error al crear el servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="a809d-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="a809d-217">Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-217">Problem</span></span>
<span data-ttu-id="a809d-218">Puede que vea este error al intentar usar el Administrador de credenciales en el portal para especificar las credenciales de un nuevo servicio vinculado o para actualizar las credenciales de un servicio vinculado existente.</span><span class="sxs-lookup"><span data-stu-id="a809d-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="a809d-219">Cuando aparece este error, la página de configuración del Administrador de configuración de Puerta de enlace de administración de datos tiene un aspecto similar al de la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a809d-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![No se puede establecer conexión con la base de datos](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="a809d-221">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-221">Cause</span></span>
<span data-ttu-id="a809d-222">Es posible que se haya perdido el certificado SSL en la máquina de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="a809d-223">El equipo de la puerta de enlace no puede cargar certificado usado actualmente para el cifrado SSL.</span><span class="sxs-lookup"><span data-stu-id="a809d-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="a809d-224">También puede ver un mensaje de error en el registro de eventos que es similar al siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="a809d-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="a809d-225">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-225">Resolution</span></span>
<span data-ttu-id="a809d-226">Siga estos pasos para solucionar el problema:</span><span class="sxs-lookup"><span data-stu-id="a809d-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="a809d-227">Inicie el Administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="a809d-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="a809d-228">Cambie a la pestaña **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="a809d-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="a809d-229">Haga clic en el botón **Cambiar** para cambiar el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a809d-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![Botón Cambiar certificado](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="a809d-231">Seleccione un nuevo certificado como certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a809d-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="a809d-232">Puede usar cualquier certificado SSL que haya generado por su cuenta o que haya generado una organización.</span><span class="sxs-lookup"><span data-stu-id="a809d-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="a809d-234">Error en la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="a809d-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="a809d-235">Problema</span><span class="sxs-lookup"><span data-stu-id="a809d-235">Problem</span></span>
<span data-ttu-id="a809d-236">Puede que vea el error "UserErrorFailedToConnectToSqlserver" después de configurar una canalización en el portal.</span><span class="sxs-lookup"><span data-stu-id="a809d-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="a809d-237">Causa</span><span class="sxs-lookup"><span data-stu-id="a809d-237">Cause</span></span>
<span data-ttu-id="a809d-238">Esto puede ocurrir por diferentes motivos y la mitigación varía según la causa.</span><span class="sxs-lookup"><span data-stu-id="a809d-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="a809d-239">Resolución</span><span class="sxs-lookup"><span data-stu-id="a809d-239">Resolution</span></span>
<span data-ttu-id="a809d-240">Permita las conexiones TCP de salida a través del puerto TCP/1433 en el lado cliente de Puerta de enlace de administración de datos antes de conectar a una SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a809d-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="a809d-241">Si la base de datos de destino es una Azure SQL Database, compruebe también la configuración del firewall de SQL Server para Azure.</span><span class="sxs-lookup"><span data-stu-id="a809d-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="a809d-242">Vea la sección siguiente para realizar una prueba de conexión en el almacén de datos local.</span><span class="sxs-lookup"><span data-stu-id="a809d-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="a809d-243">Errores relacionados con la conexión al almacén de datos o con los controladores</span><span class="sxs-lookup"><span data-stu-id="a809d-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="a809d-244">Si ve errores relacionados con los controladores o la conexión al almacén de datos, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a809d-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="a809d-245">Inicie el Administrador de configuración de la puerta de enlace de administración de datos en la máquina de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="a809d-246">Cambie a la pestaña **Diagnósticos** .</span><span class="sxs-lookup"><span data-stu-id="a809d-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="a809d-247">En **Probar conexión**, agregue los valores de grupo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="a809d-248">Haga clic en **Probar** para ver si puede conectarse al origen de datos local desde la máquina de la puerta de enlace utilizando las credenciales y la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="a809d-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="a809d-249">Si la conexión de prueba sigue sin funcionar después de instalar un controlador, reinicie la puerta de enlace para recoger los cambios más recientes.</span><span class="sxs-lookup"><span data-stu-id="a809d-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Prueba de conexión en la pestaña Diagnósticos](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="a809d-251">Registros de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a809d-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="a809d-252">Enviar registros de puerta de enlace a Microsoft</span><span class="sxs-lookup"><span data-stu-id="a809d-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="a809d-253">Cuando se ponga en contacto con el equipo de soporte técnico de Microsoft para solucionar problemas de la puerta de enlace, es posible que se le pida que comparta los registros de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="a809d-254">Con la versión de la puerta de enlace, puede compartir registros de puerta de enlace necesarios con dos clics de botón en el Administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="a809d-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="a809d-255">Cambie a la pestaña **Diagnóstico** del Administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="a809d-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Pestaña Diagnóstico de la puerta de enlace de administración de datos](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="a809d-257">Haga clic en **Enviar registros** para ver el siguiente cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a809d-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Puerta de enlace de administración de datos: Enviar registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="a809d-259">(Opcional) Haga clic en **Ver registros** para revisar los registros en el Visor de eventos.</span><span class="sxs-lookup"><span data-stu-id="a809d-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="a809d-260">(Opcional) Haga clic en **Privacidad** para revisar la declaración de privacidad de servicios web de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a809d-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="a809d-261">Una vez que esté satisfecho con lo que va a cargar, haga clic en **Enviar registros** para enviar realmente los registros de los últimos siete días a Microsoft para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="a809d-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="a809d-262">Debería ver el estado de la operación de envío de registros tal y como aparece en la siguiente captura.</span><span class="sxs-lookup"><span data-stu-id="a809d-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Puerta de enlace de administración de datos: Estado del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="a809d-264">Una vez que finalice la operación, verá un cuadro de diálogo como el que se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a809d-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Puerta de enlace de administración de datos: Estado del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="a809d-266">Guarde el **identificador de informe** y envíelo al equipo de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a809d-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="a809d-267">El identificador de informe sirve para encontrar los registros de la puerta de enlace que ha cargado para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="a809d-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="a809d-268">Este identificador del informe también se guarda en el Visor de eventos.</span><span class="sxs-lookup"><span data-stu-id="a809d-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="a809d-269">Lo encontrará si examina el identificador de evento “25” y comprueba la fecha y la hora.</span><span class="sxs-lookup"><span data-stu-id="a809d-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Puerta de enlace de administración de datos: Identificador de informe del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="a809d-271">Archivar registros de puerta de enlace en el equipo host de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a809d-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="a809d-272">Hay veces en las que existen problemas con la puerta de enlace y no es posible compartir los registros de puerta de enlace de forma directa:</span><span class="sxs-lookup"><span data-stu-id="a809d-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="a809d-273">Cuando se instala y registra manualmente la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a809d-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="a809d-274">Cuando se trata de registrar la puerta de enlace con una clave regenerada en el Administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="a809d-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="a809d-275">Cuando se trata de enviar registros, pero el servicio host de la puerta de enlace de administración de datos no se puede conectar.</span><span class="sxs-lookup"><span data-stu-id="a809d-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="a809d-276">Para estos escenarios, puede guardar los registros de puerta de enlace como un archivo ZIP y compartirlo cuando pueda ponerse en contacto con el equipo de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a809d-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="a809d-277">Por ejemplo, si recibe el siguiente error al registrar la puerta de enlace tal y como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a809d-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Puerta de enlace de administración de datos: Error de registro](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="a809d-279">Haga clic en el vínculo **Archivar registros de puerta de enlace** para archivar y guardar los registros y, luego, comparta el archivo ZIP con el equipo de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a809d-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Puerta de enlace de administración de datos: Archivar registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="a809d-281">Buscar registros de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="a809d-281">Locate gateway logs</span></span>
<span data-ttu-id="a809d-282">Puede obtener información detallada de los registros de la puerta de enlace en los registros de eventos de Windows.</span><span class="sxs-lookup"><span data-stu-id="a809d-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="a809d-283">Inicie el **Visor de eventos** de Windows.</span><span class="sxs-lookup"><span data-stu-id="a809d-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="a809d-284">Busque los registros en la carpeta **Registros de aplicaciones y servicios** > **Puerta de enlace de administración de datos**.</span><span class="sxs-lookup"><span data-stu-id="a809d-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="a809d-285">Al solucionar problemas relacionados con la puerta de enlace, busque eventos de error en el Visor de eventos.</span><span class="sxs-lookup"><span data-stu-id="a809d-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Puerta de enlace de administración de datos: Registros en el Visor de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
