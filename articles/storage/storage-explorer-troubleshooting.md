---
title: "Guía de solución de problemas del Explorador de Azure Storage | Microsoft Docs"
description: "Información general sobre las dos funciones de depuración de Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: e9b833b07556378f17d9aaff0912c7d73dff44eb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="57ac0-103">Guía de solución de problemas del Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="57ac0-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="57ac0-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="57ac0-104">Introduction</span></span>

<span data-ttu-id="57ac0-105">El Explorador de Microsoft Azure Storage (versión preliminar) es una aplicación independiente que permite trabajar fácilmente con los datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="57ac0-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="57ac0-106">La aplicación puede conectarse a las cuentas de Storage hospedadas en Azure, nubes independientes y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="57ac0-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="57ac0-107">Esta guía resume las soluciones para problemas comunes en el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="57ac0-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="57ac0-108">Problemas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="57ac0-108">Sign in issues</span></span>

<span data-ttu-id="57ac0-109">Solo se admiten las cuentas de Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="57ac0-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="57ac0-110">Si usa una cuenta de AD FS, se espera que el inicio de sesión en el Explorador de Storage no funcione.</span><span class="sxs-lookup"><span data-stu-id="57ac0-110">If you use an ADFS account, it’s expected that signing in to Storage Explorer would not work.</span></span> <span data-ttu-id="57ac0-111">Antes de continuar, pruebe a reiniciar la aplicación para ver si se pueden corregir los problemas.</span><span class="sxs-lookup"><span data-stu-id="57ac0-111">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="57ac0-112">Error: Certificado autofirmado de cadena de certificados</span><span class="sxs-lookup"><span data-stu-id="57ac0-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="57ac0-113">Hay varias razones por las puede encontrar este error, y las dos causas más comunes son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="57ac0-113">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="57ac0-114">La aplicación se conecta a través de un "proxy transparente", lo que significa que un servidor (por ejemplo, el servidor de la compañía) intercepta el tráfico HTTPS, lo descifra y, luego, lo cifrar mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="57ac0-114">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="57ac0-115">Ejecuta una aplicación, como software antivirus, que inserta un certificado SSL autofirmado en los mensajes HTTPS que recibe.</span><span class="sxs-lookup"><span data-stu-id="57ac0-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="57ac0-116">Cuando el Explorador de Storage se encuentra uno de estos problemas, no puede saber si se alteró el mensaje HTTPS recibido.</span><span class="sxs-lookup"><span data-stu-id="57ac0-116">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="57ac0-117">Si tiene una copia del certificado autofirmado, puede dejar que el Explorador de Storage confíe en él.</span><span class="sxs-lookup"><span data-stu-id="57ac0-117">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="57ac0-118">Si no está seguro de quién insertó el certificado, siga estos pasos para descubrirlo:</span><span class="sxs-lookup"><span data-stu-id="57ac0-118">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="57ac0-119">Instale Open SSL.</span><span class="sxs-lookup"><span data-stu-id="57ac0-119">Install Open SSL</span></span>

    - <span data-ttu-id="57ac0-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (cualquiera de las versiones ligeras debería ser suficiente).</span><span class="sxs-lookup"><span data-stu-id="57ac0-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="57ac0-121">Mac y Linux: debe estar incluido con el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="57ac0-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="57ac0-122">Ejecute Open SSL.</span><span class="sxs-lookup"><span data-stu-id="57ac0-122">Run Open SSL</span></span>

    - <span data-ttu-id="57ac0-123">Windows: abra el directorio de instalación, haga clic en **/bin/**y, luego, haga doble clic en **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="57ac0-123">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="57ac0-124">Mac y Linux: ejecute **openssl** desde un terminal.</span><span class="sxs-lookup"><span data-stu-id="57ac0-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="57ac0-125">Ejecute s_client -showcerts -connect microsoft.com:443.</span><span class="sxs-lookup"><span data-stu-id="57ac0-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="57ac0-126">Busque certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="57ac0-126">Look for self-signed certificates.</span></span> <span data-ttu-id="57ac0-127">Si no está seguro de cuáles son autofirmados, busque cualquier lugar en el que el asunto ("s:") y el emisor ("i:") sean el mismo.</span><span class="sxs-lookup"><span data-stu-id="57ac0-127">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="57ac0-128">Cuando haya encontrado cualquier certificado autofirmado, para cada uno, copie y pegue todo el contenido desde **---BEGIN CERTIFICATE---** a **---END CERTIFICATE---** (inclusive) a un archivo .cer nuevo.</span><span class="sxs-lookup"><span data-stu-id="57ac0-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="57ac0-129">Abra el Explorador de Storage, haga clic en **Editar** > **Certificados SSL** > **Importar certificados** y, luego, utilice el selector de archivos para encontrar, seleccionar y abrir los archivos .cer que ha creado.</span><span class="sxs-lookup"><span data-stu-id="57ac0-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="57ac0-130">Si no se encuentra ningún certificado autofirmado siguiendo los pasos anteriores, póngase en contacto con nosotros mediante la herramienta de comentarios para obtener más ayuda.</span><span class="sxs-lookup"><span data-stu-id="57ac0-130">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="57ac0-131">No se pueden recuperar las suscripciones</span><span class="sxs-lookup"><span data-stu-id="57ac0-131">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="57ac0-132">Si no puede recuperar las suscripciones después de iniciar la sesión correctamente, siga estos pasos para solucionar este problema:</span><span class="sxs-lookup"><span data-stu-id="57ac0-132">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="57ac0-133">Verifique que la cuenta tiene acceso a las suscripciones al iniciar sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="57ac0-133">Verify that your account has access to the subscriptions by signing into the Azure portal.</span></span>

- <span data-ttu-id="57ac0-134">Asegúrese de que ha iniciado sesión usando el entorno correcto (Azure, Azure China, Azure Alemania, Azure US Government, o entorno personalizado o Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="57ac0-134">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="57ac0-135">Si está detrás de un proxy, asegúrese de que ha configurado correctamente el proxy del Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="57ac0-135">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="57ac0-136">Pruebe a quitar la cuenta y volver a agregarla.</span><span class="sxs-lookup"><span data-stu-id="57ac0-136">Try removing and readding the account.</span></span>

- <span data-ttu-id="57ac0-137">Intente eliminar los siguientes archivos del directorio raíz (es decir, C:\Users\ContosoUser) y, luego, intente volver a agregar la cuenta:</span><span class="sxs-lookup"><span data-stu-id="57ac0-137">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="57ac0-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="57ac0-138">.adalcache</span></span>

    - <span data-ttu-id="57ac0-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="57ac0-139">.devaccounts</span></span>

    - <span data-ttu-id="57ac0-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="57ac0-140">.extaccounts</span></span>

- <span data-ttu-id="57ac0-141">Revise la consola de las herramientas de desarrollo (presionando F12) cuando se inicie sesión por si aparecieran mensajes de error:</span><span class="sxs-lookup"><span data-stu-id="57ac0-141">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![herramientas de desarrollo](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="57ac0-143">No se puede ver la página de autenticación</span><span class="sxs-lookup"><span data-stu-id="57ac0-143">Unable to see the authentication page</span></span>

<span data-ttu-id="57ac0-144">Si no puede ver la página de autenticación, siga estos pasos para solucionar este problema:</span><span class="sxs-lookup"><span data-stu-id="57ac0-144">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="57ac0-145">Según la velocidad de la conexión, la página de inicio de sesión puede tardar unos instantes en cargar; espere al menos un minuto antes de cerrar el cuadro de diálogo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="57ac0-145">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="57ac0-146">Si está detrás de un proxy, asegúrese de que ha configurado correctamente el proxy del Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="57ac0-146">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="57ac0-147">Consulte la consola del desarrollador presionando la tecla F12.</span><span class="sxs-lookup"><span data-stu-id="57ac0-147">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="57ac0-148">Revise las respuestas de la consola del desarrollador y vea si puede encontrar alguna pista para saber por qué no funciona la autenticación.</span><span class="sxs-lookup"><span data-stu-id="57ac0-148">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="57ac0-149">No se puede quitar la cuenta</span><span class="sxs-lookup"><span data-stu-id="57ac0-149">Cannot remove account</span></span>

<span data-ttu-id="57ac0-150">Si no puede quitar una cuenta, o si el vínculo para volver a autenticar no hace nada, siga estos pasos para solucionar este problema:</span><span class="sxs-lookup"><span data-stu-id="57ac0-150">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="57ac0-151">Intente eliminar los siguientes archivos del directorio raíz y, luego, intente volver a agregar la cuenta:</span><span class="sxs-lookup"><span data-stu-id="57ac0-151">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="57ac0-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="57ac0-152">.adalcache</span></span>

    - <span data-ttu-id="57ac0-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="57ac0-153">.devaccounts</span></span>

    - <span data-ttu-id="57ac0-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="57ac0-154">.extaccounts</span></span>

- <span data-ttu-id="57ac0-155">Si desea quitar recursos de Storage conectados a SAS, elimine los siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="57ac0-155">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="57ac0-156">Carpeta %AppData%/StorageExplorer para Windows</span><span class="sxs-lookup"><span data-stu-id="57ac0-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="57ac0-157">/Users/<su_nombre>/Library/Applicaiton SUpport/StorageExplorer para Mac</span><span class="sxs-lookup"><span data-stu-id="57ac0-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="57ac0-158">~/.config/StorageExplorer para Linux</span><span class="sxs-lookup"><span data-stu-id="57ac0-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="57ac0-159">Tendrá que volver a escribir todas sus credenciales si elimina estos archivos.</span><span class="sxs-lookup"><span data-stu-id="57ac0-159">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="57ac0-160">Problemas de proxy</span><span class="sxs-lookup"><span data-stu-id="57ac0-160">Proxy issues</span></span>

<span data-ttu-id="57ac0-161">En primer lugar, asegúrese de que la siguiente información que especificó sea correcta:</span><span class="sxs-lookup"><span data-stu-id="57ac0-161">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="57ac0-162">La dirección URL del proxy y el número de puerto</span><span class="sxs-lookup"><span data-stu-id="57ac0-162">The proxy URL and port number</span></span>

- <span data-ttu-id="57ac0-163">El nombre de usuario y la contraseña si los exige el proxy</span><span class="sxs-lookup"><span data-stu-id="57ac0-163">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="57ac0-164">Soluciones comunes</span><span class="sxs-lookup"><span data-stu-id="57ac0-164">Common solutions</span></span>

<span data-ttu-id="57ac0-165">Si sigue experimentando problemas, siga estos pasos para solucionarlos:</span><span class="sxs-lookup"><span data-stu-id="57ac0-165">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="57ac0-166">Si puede conectarse a Internet sin usar el proxy, compruebe que el Explorador de Storage funciona sin la configuración del proxy habilitada.</span><span class="sxs-lookup"><span data-stu-id="57ac0-166">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="57ac0-167">Si este es así, puede haber un problema con la configuración de proxy.</span><span class="sxs-lookup"><span data-stu-id="57ac0-167">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="57ac0-168">Trabaje con el administrador del servidor proxy para identificar los problemas.</span><span class="sxs-lookup"><span data-stu-id="57ac0-168">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="57ac0-169">Compruebe que otras aplicaciones que utilicen el servidor proxy funcionen según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="57ac0-169">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="57ac0-170">Compruebe que pueda conectarse a Microsoft Azure Portal mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="57ac0-170">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="57ac0-171">Compruebe que puede recibir las respuestas de los puntos de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="57ac0-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="57ac0-172">Especifique una de las direcciones URL de punto de conexión en el explorador.</span><span class="sxs-lookup"><span data-stu-id="57ac0-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="57ac0-173">Si puede conectarse, debería recibir un InvalidQueryParameterValue o una respuesta XML similar.</span><span class="sxs-lookup"><span data-stu-id="57ac0-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="57ac0-174">Si otra persona también usa el Explorador de Storage con el servidor proxy, compruebe que pueda conectarse.</span><span class="sxs-lookup"><span data-stu-id="57ac0-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="57ac0-175">Si se puede conectar, quizá deba ponerse en contacto con el administrador del servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="57ac0-175">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="57ac0-176">Herramientas para el diagnóstico de problemas</span><span class="sxs-lookup"><span data-stu-id="57ac0-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="57ac0-177">Si dispone de herramientas de red, como Fiddler para Windows, es posible que pueda diagnosticar los problemas como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="57ac0-177">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="57ac0-178">Si tiene que trabajar a través del proxy, es posible que tenga que configurar la herramienta de red para conectarse a través del proxy.</span><span class="sxs-lookup"><span data-stu-id="57ac0-178">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="57ac0-179">Compruebe el número de puerto utilizado por la herramienta de red.</span><span class="sxs-lookup"><span data-stu-id="57ac0-179">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="57ac0-180">Escriba la dirección URL del host local y el número de puerto de la herramienta de red como configuración de proxy en el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="57ac0-180">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="57ac0-181">Si se hace correctamente, la herramienta de red inicia el registro de las solicitudes de red realizadas por el Explorador de Storage para puntos de conexión de servicio y administración.</span><span class="sxs-lookup"><span data-stu-id="57ac0-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="57ac0-182">Por ejemplo, escriba https://cawablobgrs.blob.core.windows.net/ para el punto de conexión de blob en un explorador y recibirá una respuesta similar a la siguiente, lo que sugiere que el recurso existe, aunque no se puede obtener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="57ac0-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![ejemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="57ac0-184">Póngase en contacto con el administrador del servidor proxy</span><span class="sxs-lookup"><span data-stu-id="57ac0-184">Contact proxy server admin</span></span>

<span data-ttu-id="57ac0-185">Si es correcta la configuración de proxy, tendrá que ponerse en contacto con el administrador del servidor proxy y, además, deberá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="57ac0-185">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="57ac0-186">Asegúrese de que el proxy no bloquee el tráfico a los puntos de conexión de administración de Azure o de los recursos.</span><span class="sxs-lookup"><span data-stu-id="57ac0-186">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="57ac0-187">Compruebe el protocolo de autenticación utilizado por el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="57ac0-187">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="57ac0-188">En estos momentos, el Explorador de Storage no admite los servidores proxy NTLM.</span><span class="sxs-lookup"><span data-stu-id="57ac0-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="57ac0-189">Mensaje de error "No se pueden recuperar los elementos secundarios"</span><span class="sxs-lookup"><span data-stu-id="57ac0-189">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="57ac0-190">Si está conectado a Azure a través de un servidor proxy, compruebe que la configuración de proxy sea correcta.</span><span class="sxs-lookup"><span data-stu-id="57ac0-190">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="57ac0-191">Si el propietario de una suscripción o una cuenta concedió acceso a un recurso, compruebe que disponga de permisos de lectura o lista para dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="57ac0-191">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="57ac0-192">Problemas con la URL de SAS</span><span class="sxs-lookup"><span data-stu-id="57ac0-192">Issues with SAS URL</span></span>
<span data-ttu-id="57ac0-193">Si se conecta a un servicio mediante una dirección URL de SAS y se produce este error:</span><span class="sxs-lookup"><span data-stu-id="57ac0-193">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="57ac0-194">Compruebe que la dirección URL proporciona los permisos necesarios para leer o enumerar los recursos.</span><span class="sxs-lookup"><span data-stu-id="57ac0-194">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="57ac0-195">Compruebe que la dirección URL no haya expirado.</span><span class="sxs-lookup"><span data-stu-id="57ac0-195">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="57ac0-196">Si la dirección URL de SAS se basa en una directiva de acceso, compruebe que la directiva de acceso no haya sido revocada.</span><span class="sxs-lookup"><span data-stu-id="57ac0-196">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57ac0-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57ac0-197">Next steps</span></span>

<span data-ttu-id="57ac0-198">Si ninguna de las soluciones funciona, envíe su problema mediante la herramienta de comentarios con su dirección de correo electrónico y todos los detalles sobre el problema como sea posible, para que podemos ponernos en contacto con usted para corregir el problema.</span><span class="sxs-lookup"><span data-stu-id="57ac0-198">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="57ac0-199">Para ello, haga clic en el menú **Ayuda** y, luego, haga clic en **Enviar comentarios**.</span><span class="sxs-lookup"><span data-stu-id="57ac0-199">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Comentarios](./media/storage-explorer-troubleshooting/4022503_en_1.png)
