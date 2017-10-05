---
title: "Azure AD Connect: Actualizar el certificado SSL para una granja de Servicios de federación de Active Directory (AD FS) | Microsoft Docs"
description: En este documento se detallan los pasos para actualizar el certificado SSL de una granja de AD FS mediante Azure AD Connect.
services: active-directory
keywords: "azure ad connect, actualizar ssl de adfs, actualizar certificado de adfs, cambiar certificado de adfs, nuevo certificado de adfs, certificado de adfs, actualizar certificado ssl de adfs, actualizar certificado ssl de adfs, configurar certificado ssl de adfs, adfs, ssl, certificado, certificado de comunicación de servicio de adfs, actualizar federación, configurar federación, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="402ee-104">Actualizar el certificado SSL para una granja de Servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="402ee-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="402ee-105">Información general</span><span class="sxs-lookup"><span data-stu-id="402ee-105">Overview</span></span>
<span data-ttu-id="402ee-106">En este artículo se describe cómo se puede usar Azure AD Connect para actualizar el certificado SSL para la granja de Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="402ee-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="402ee-107">Puede usar la herramienta Azure AD Connect para actualizar fácilmente el certificado SSL de la granja de AD FS, aun cuando el método de inicio de sesión del usuario seleccionado no sea AD FS.</span><span class="sxs-lookup"><span data-stu-id="402ee-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="402ee-108">Puede realizar toda la operación de actualización del certificado SSL para la granja de AD FS en todos los servidores de federación y de proxy de aplicación web (WAP) en tres sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="402ee-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Tres pasos](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="402ee-110">Para obtener más información sobre los certificados usados por AD FS, consulte el artículo [Descripción de los certificados usados por AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="402ee-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="402ee-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="402ee-111">Prerequisites</span></span>

* <span data-ttu-id="402ee-112">**Granja de AD FS**: asegúrese de que la granja de AD FS se base en Windows Server 2012 R2 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="402ee-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="402ee-113">**Azure AD Connect**: asegúrese de que la versión de Azure AD Connect es 1.1.443.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="402ee-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="402ee-114">Usará la tarea **Actualización del certificado SSL de AD FS**.</span><span class="sxs-lookup"><span data-stu-id="402ee-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![Tarea de actualización de SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="402ee-116">Paso 1: Proporcionar información de la granja de AD FS</span><span class="sxs-lookup"><span data-stu-id="402ee-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="402ee-117">Azure AD Connect trata de obtener automáticamente la información sobre la granja de AD FS. Para ello, realiza las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="402ee-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="402ee-118">Consultar la información de la granja de AD FS (Windows Server 2016 o posterior).</span><span class="sxs-lookup"><span data-stu-id="402ee-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="402ee-119">Hacer referencia a la información de las ejecuciones anteriores (que se almacena localmente con Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="402ee-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="402ee-120">Puede modificar la lista de servidores que aparecen mediante la adición o eliminación de los servidores a fin de reflejar la configuración actual de la granja de AD FS.</span><span class="sxs-lookup"><span data-stu-id="402ee-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="402ee-121">Tan pronto como se proporciona la información del servidor, Azure AD Connect muestra la conectividad y el estado actual del certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="402ee-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![Información del servidor de AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="402ee-123">Si la lista contiene un servidor que ya no forma parte de la granja de AD FS, haga clic en **Quitar** para eliminar el servidor de la lista de servidores de la granja de AD FS.</span><span class="sxs-lookup"><span data-stu-id="402ee-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![Servidor sin conexión en la lista](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="402ee-125">La eliminación de un servidor de la lista de servidores de la granja de AD FS en Azure AD Connect es una operación local y actualiza la información de la granja de AD FS que Azure AD Connect mantiene localmente.</span><span class="sxs-lookup"><span data-stu-id="402ee-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="402ee-126">Azure AD Connect no modifica la configuración en AD FS para reflejar el cambio.</span><span class="sxs-lookup"><span data-stu-id="402ee-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="402ee-127">Paso 2: Proporcionar el nuevo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="402ee-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="402ee-128">Después de confirmar la información sobre los servidores de la granja de AD FS, Azure AD Connect solicita el nuevo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="402ee-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="402ee-129">Proporcione un certificado PFX protegido con contraseña para continuar con la instalación.</span><span class="sxs-lookup"><span data-stu-id="402ee-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![Certificado SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="402ee-131">Después de proporcionar el certificado, Azure AD Connect pasa por una serie de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="402ee-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="402ee-132">Compruebe el certificado para asegurarse de que es correcto para la granja de AD FS:</span><span class="sxs-lookup"><span data-stu-id="402ee-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="402ee-133">El nombre de sujeto o el nombre alternativo de sujeto para el certificado es igual que el nombre del servicio de federación o es un certificado comodín.</span><span class="sxs-lookup"><span data-stu-id="402ee-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="402ee-134">El certificado es válido durante más de 30 días.</span><span class="sxs-lookup"><span data-stu-id="402ee-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="402ee-135">La cadena de confianza del certificado es válida.</span><span class="sxs-lookup"><span data-stu-id="402ee-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="402ee-136">El certificado está protegido con contraseña.</span><span class="sxs-lookup"><span data-stu-id="402ee-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="402ee-137">Paso 3: Seleccionar los servidores para la actualización</span><span class="sxs-lookup"><span data-stu-id="402ee-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="402ee-138">En el paso siguiente, seleccione los servidores que deben tener el certificado SSL actualizado.</span><span class="sxs-lookup"><span data-stu-id="402ee-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="402ee-139">Los servidores que están sin conexión no se pueden seleccionar para la actualización.</span><span class="sxs-lookup"><span data-stu-id="402ee-139">Servers that are offline can't be selected for the update.</span></span>

![Seleccionar los servidores para actualizar](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="402ee-141">Una vez completada la configuración, Azure AD Connect muestra el mensaje que indica el estado de la actualización y proporciona una opción para comprobar el inicio de sesión de AD FS.</span><span class="sxs-lookup"><span data-stu-id="402ee-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Configuración completada](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="402ee-143">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="402ee-143">FAQs</span></span>

* <span data-ttu-id="402ee-144">**¿Cuál debe ser el nombre de sujeto del certificado para el nuevo certificado SSL de AD FS?**</span><span class="sxs-lookup"><span data-stu-id="402ee-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="402ee-145">Azure AD Connect comprueba si el nombre de sujeto o el nombre alternativo de sujeto del certificado contiene el nombre del servicio de federación.</span><span class="sxs-lookup"><span data-stu-id="402ee-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="402ee-146">Por ejemplo, si el nombre del servicio de federación es fs.contoso.com, el nombre de sujeto o el nombre de sujeto alternativo debe ser fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="402ee-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="402ee-147">También se aceptan certificados comodín.</span><span class="sxs-lookup"><span data-stu-id="402ee-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="402ee-148">**¿Por qué me piden de nuevo las credenciales en la página del servidor de WAP?**</span><span class="sxs-lookup"><span data-stu-id="402ee-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="402ee-149">Si las credenciales proporcionadas para conectarse a servidores de AD FS no tienen el privilegio para administrar también los servidores de WAP, Azure AD Connect pide las credenciales que tienen privilegios administrativos en los servidores de WAP.</span><span class="sxs-lookup"><span data-stu-id="402ee-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="402ee-150">**El servidor se muestra como sin conexión. ¿qué debo hacer?**</span><span class="sxs-lookup"><span data-stu-id="402ee-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="402ee-151">Azure AD Connect no puede realizar ninguna operación si el servidor está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="402ee-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="402ee-152">Si el servidor forma parte de la granja de AD FS, compruebe la conectividad con el servidor.</span><span class="sxs-lookup"><span data-stu-id="402ee-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="402ee-153">Después de resolver el problema, pulse el icono de actualización para actualizar el estado en el asistente.</span><span class="sxs-lookup"><span data-stu-id="402ee-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="402ee-154">Si el servidor formó parte de la granja anteriormente pero ahora ya no existe, haga clic en **Quitar** para eliminarlo de la lista de servidores que mantiene Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="402ee-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="402ee-155">El hecho de quitar el servidor de la lista en Azure AD Connect no modifica la propia configuración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="402ee-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="402ee-156">Si usa AD FS en Windows Server 2016 o posterior, el servidor permanece en las opciones de configuración y se mostrará la próxima vez que se ejecute la tarea.</span><span class="sxs-lookup"><span data-stu-id="402ee-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="402ee-157">**¿Puedo actualizar un subconjunto de los servidores de la granja con el nuevo certificado SSL?**</span><span class="sxs-lookup"><span data-stu-id="402ee-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="402ee-158">Sí.</span><span class="sxs-lookup"><span data-stu-id="402ee-158">Yes.</span></span> <span data-ttu-id="402ee-159">Siempre puede ejecutar la tarea **Actualizar certificado SSL** de nuevo para actualizar el resto de servidores.</span><span class="sxs-lookup"><span data-stu-id="402ee-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="402ee-160">En la página **Seleccionar servidores para la actualización del certificado SSL**, puede ordenar la lista de servidores por **Fecha de expiración de SSL** para tener acceso fácilmente a los servidores que todavía no se han actualizado.</span><span class="sxs-lookup"><span data-stu-id="402ee-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="402ee-161">**Quité el servidor en la ejecución anterior, pero todavía se muestra como sin conexión y aparece en la página de servidores de AD FS. ¿Por qué sigue estando sin conexión el servidor incluso después de la eliminación?**</span><span class="sxs-lookup"><span data-stu-id="402ee-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="402ee-162">Quitar el servidor de la lista en Azure AD Connect no lo quita de la configuración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="402ee-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="402ee-163">Azure AD Connect hace referencia a AD FS (Windows Server 2016 o posterior) para cualquier información sobre la granja.</span><span class="sxs-lookup"><span data-stu-id="402ee-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="402ee-164">Si el servidor sigue estando presente en la configuración de AD FS, aparecerá de nuevo en la lista.</span><span class="sxs-lookup"><span data-stu-id="402ee-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="402ee-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="402ee-165">Next steps</span></span>

- [<span data-ttu-id="402ee-166">Azure AD Connect y la federación</span><span class="sxs-lookup"><span data-stu-id="402ee-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="402ee-167">Servicios de federación de Active Directory y personalización con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="402ee-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
