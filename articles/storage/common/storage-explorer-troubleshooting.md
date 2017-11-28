---
title: "Guía para solucionar problemas del explorador de almacenamiento de aaaAzure | Documentos de Microsoft"
description: "Información general sobre la característica de depuración de hello dos de Azure"
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
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="0c9d4-103">Guía de solución de problemas del Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0c9d4-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="0c9d4-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="0c9d4-104">Introduction</span></span>

<span data-ttu-id="0c9d4-105">Explorador de almacenamiento de Microsoft Azure (vista previa) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="0c9d4-106">aplicación Hello puede conectarse a las cuentas de toStorage hospedadas en Azure, la condición soberano nubes y la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="0c9d4-107">Esta guía resume las soluciones para problemas comunes en el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="0c9d4-108">Problemas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="0c9d4-108">Sign in issues</span></span>

<span data-ttu-id="0c9d4-109">Antes de continuar, pruebe a reiniciar la aplicación y vea si se pueden corregir los problemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="0c9d4-110">Error: Certificado autofirmado de cadena de certificados</span><span class="sxs-lookup"><span data-stu-id="0c9d4-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="0c9d4-111">Hay varias razones por las este error puede aparecer, y hello más dos motivos principales son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="0c9d4-112">aplicación Hello se conecta a través de "proxy transparente", lo que significa un servidor (por ejemplo, el servidor de la compañía) es interceptar tráfico HTTPS, el descifrado y, a continuación, cifrar mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="0c9d4-113">Ejecuta una aplicación, como software antivirus, que se inserte un certificado SSL autofirmado en los mensajes de Hola HTTPS que recibirá.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="0c9d4-114">Cuando el Explorador de almacenamiento se encuentra uno de los problemas de hello, puede ya no se sabe si se manipula el mensaje de bienvenida recibido de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="0c9d4-115">Si tiene una copia del certificado autofirmado de hello, puede dejar que el Explorador de almacenamiento confiar en él.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="0c9d4-116">Si no está seguro de que inserte certificado hello, siga estos pasos toofind:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="0c9d4-117">Instale Open SSL.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-117">Install Open SSL</span></span>

    - <span data-ttu-id="0c9d4-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (cualquiera de las versiones claro Hola debería ser suficiente)</span><span class="sxs-lookup"><span data-stu-id="0c9d4-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="0c9d4-119">Mac y Linux: debe estar incluido con el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="0c9d4-120">Ejecute Open SSL.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-120">Run Open SSL</span></span>

    - <span data-ttu-id="0c9d4-121">Windows: abrir el directorio de instalación de hello, haga clic en **/bin/**y, a continuación, haga doble clic en **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="0c9d4-122">Mac y Linux: ejecute **openssl** desde un terminal.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="0c9d4-123">Ejecute s_client -showcerts -connect microsoft.com:443.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="0c9d4-124">Busque certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-124">Look for self-signed certificates.</span></span> <span data-ttu-id="0c9d4-125">Si no está seguro de que están autofirmados, busque en cualquier lugar asunto Hola ("s:") y emisor ("i") se Hola igual.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="0c9d4-126">Cuando haya encontrado los certificados autofirmados, para cada una de ellas, copiar y pegar todo el contenido de e incluidas **---BEGIN CERTIFICATE---** demasiado**---END CERTIFICATE---** tooa nueva CER.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="0c9d4-127">Abra el Explorador de almacenamiento, haga clic en **editar** > **certificados SSL** > **importar certificados**y, a continuación, use Hola archivo selector toofind, seleccione esta opción, y abrir archivos de CER Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="0c9d4-128">Si no se encuentra ningún certificado autofirmado con hello por encima de los pasos, póngase en contacto con nosotros a través de la herramienta de comentarios de Hola para obtener más ayuda.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="0c9d4-129">No se puede tooretrieve suscripciones</span><span class="sxs-lookup"><span data-stu-id="0c9d4-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="0c9d4-130">Si es que no se puede tooretrieve las suscripciones después de iniciar sesión correctamente, siga estos pasos tootroubleshoot este problema:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="0c9d4-131">Compruebe que la cuenta tiene acceso toohello suscripciones al iniciar sesión en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="0c9d4-132">Asegúrese de que ha iniciado sesión con entorno correcto de hello (Azure, Azure China, Azure en Alemania, gobierno de EE o personalizado entorno/Azure pila).</span><span class="sxs-lookup"><span data-stu-id="0c9d4-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="0c9d4-133">Si está detrás de un proxy, asegúrese de que ha configurado el proxy del explorador de almacenamiento de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="0c9d4-134">Intente quitar y volver a agregar la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="0c9d4-135">Intente eliminar Hola siguientes archivos desde el directorio raíz (es decir, C:\Users\ContosoUser) y, a continuación, volver a agregar la cuenta de hello:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="0c9d4-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="0c9d4-136">.adalcache</span></span>

    - <span data-ttu-id="0c9d4-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="0c9d4-137">.devaccounts</span></span>

    - <span data-ttu-id="0c9d4-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="0c9d4-138">.extaccounts</span></span>

- <span data-ttu-id="0c9d4-139">Consola de herramientas de desarrollador de Hola de inspección (presionando F12) cuando se firma los mensajes de error:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![herramientas de desarrollo](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="0c9d4-141">Página de autenticación de hello toosee no se puede</span><span class="sxs-lookup"><span data-stu-id="0c9d4-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="0c9d4-142">Si es que la página de autenticación de hello toosee no se puede, siga estos pasos tootroubleshoot este problema:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="0c9d4-143">Según la velocidad de saludo de la conexión, puede tardar un poco para tooload de la página de inicio de sesión de hello, espere al menos un minuto antes de cerrar el cuadro de diálogo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="0c9d4-144">Si está detrás de un proxy, asegúrese de que ha configurado el proxy del explorador de almacenamiento de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="0c9d4-145">Ver la consola para desarrolladores de hello presionando la tecla F12 de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="0c9d4-146">Ver las respuestas de Hola desde la consola para desarrolladores hello y vea si puede encontrar ninguna pista para saber por qué no funciona la autenticación.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="0c9d4-147">No se puede quitar la cuenta</span><span class="sxs-lookup"><span data-stu-id="0c9d4-147">Cannot remove account</span></span>

<span data-ttu-id="0c9d4-148">Si no se puede tooremove una cuenta o si Hola volver a autenticar vínculo no hace nada, siga estos pasos tootroubleshoot este problema:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="0c9d4-149">Intente eliminar Hola siguientes archivos desde el directorio raíz y, a continuación, volver a agregar la cuenta de hello:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="0c9d4-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="0c9d4-150">.adalcache</span></span>

    - <span data-ttu-id="0c9d4-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="0c9d4-151">.devaccounts</span></span>

    - <span data-ttu-id="0c9d4-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="0c9d4-152">.extaccounts</span></span>

- <span data-ttu-id="0c9d4-153">Si desea que tooremove SAS adjunta los recursos de almacenamiento, elimine Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="0c9d4-154">Carpeta %AppData%/StorageExplorer para Windows</span><span class="sxs-lookup"><span data-stu-id="0c9d4-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="0c9d4-155">/Users/<su_nombre>/Library/Applicaiton SUpport/StorageExplorer para Mac</span><span class="sxs-lookup"><span data-stu-id="0c9d4-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="0c9d4-156">~/.config/StorageExplorer para Linux</span><span class="sxs-lookup"><span data-stu-id="0c9d4-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="0c9d4-157">Tendrá tooreenter todas sus credenciales si elimina estos archivos.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="0c9d4-158">Problemas de proxy</span><span class="sxs-lookup"><span data-stu-id="0c9d4-158">Proxy issues</span></span>

<span data-ttu-id="0c9d4-159">En primer lugar, asegúrese de que ese Hola siguiendo la información que especificó son correctos:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="0c9d4-160">Hola dirección URL del proxy y el puerto número</span><span class="sxs-lookup"><span data-stu-id="0c9d4-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="0c9d4-161">Nombre de usuario y contraseña si es necesario por proxy Hola</span><span class="sxs-lookup"><span data-stu-id="0c9d4-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="0c9d4-162">Soluciones comunes</span><span class="sxs-lookup"><span data-stu-id="0c9d4-162">Common solutions</span></span>

<span data-ttu-id="0c9d4-163">Si sigue experimentando problemas, siga estos pasos tootroubleshoot ellos:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="0c9d4-164">Si puede conectarse toohello Internet sin usar al proxy, compruebe que el Explorador de almacenamiento funciona sin la configuración del proxy habilitada.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="0c9d4-165">Si éste es el caso de hello, puede haber un problema con la configuración de proxy.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="0c9d4-166">Trabajar con sus problemas de proxy administrador tooidentify Hola.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="0c9d4-167">Compruebe que otras aplicaciones que utilicen el servidor proxy de hello funcionan según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="0c9d4-168">Compruebe que puede conectar el portal de Microsoft Azure toohello mediante el explorador web</span><span class="sxs-lookup"><span data-stu-id="0c9d4-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="0c9d4-169">Compruebe que puede recibir las respuestas de los puntos de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="0c9d4-170">Especifique una de las direcciones URL de punto de conexión en el explorador.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="0c9d4-171">Si puede conectarse, debería recibir un InvalidQueryParameterValue o una respuesta XML similar.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="0c9d4-172">Si otra persona también usa el Explorador de Storage con el servidor proxy, compruebe que pueda conectarse.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="0c9d4-173">Si puede conectar, puede tener toocontact el administrador del servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="0c9d4-174">Herramientas para el diagnóstico de problemas</span><span class="sxs-lookup"><span data-stu-id="0c9d4-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="0c9d4-175">Si dispone de herramientas de red, como Fiddler para Windows, es posible que los siguientes problemas de hello toodiagnose capaz de:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="0c9d4-176">Si tienes toowork a través de proxy, puede tener tooconfigure su red tooconnect de herramienta a través de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="0c9d4-177">Compruebe el número de puerto de hello utilizado por la herramienta de red.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="0c9d4-178">Escriba la dirección URL del host local de Hola y Hola número de puerto de la herramienta de red como configuración de proxy en el Explorador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="0c9d4-179">Si este isdone correctamente, la herramienta de red se inicia el registro de las solicitudes de red realizadas por los extremos de servicio y toomanagement de explorador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="0c9d4-180">Por ejemplo, escriba https://cawablobgrs.blob.core.windows.net/ para el extremo de blob en un explorador, y recibirá una respuesta similar a la siguiente hello, lo que sugiere Hola recurso existe, aunque no se puede obtener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![ejemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="0c9d4-182">Póngase en contacto con el administrador del servidor proxy</span><span class="sxs-lookup"><span data-stu-id="0c9d4-182">Contact proxy server admin</span></span>

<span data-ttu-id="0c9d4-183">Si es correcta la configuración de proxy, puede que tenga toocontact el administrador del servidor proxy, y</span><span class="sxs-lookup"><span data-stu-id="0c9d4-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="0c9d4-184">Asegúrese de que el proxy no bloquee el tráfico tooAzure administración o recurso de puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="0c9d4-185">Comprobar el protocolo de autenticación de hello utilizada por el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="0c9d4-186">En estos momentos, el Explorador de Storage no admite los servidores proxy NTLM.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="0c9d4-187">Mensaje de error "No se puede tooRetrieve elementos secundarios"</span><span class="sxs-lookup"><span data-stu-id="0c9d4-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="0c9d4-188">Si está conectado tooAzure a través de un servidor proxy, compruebe que la configuración de proxy es correcta.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="0c9d4-189">Si se concede acceso tooa recursos de propietario de Hola de suscripción de Hola o la cuenta, compruebe que ha leído o lista de permisos para dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="0c9d4-190">Problemas con la URL de SAS</span><span class="sxs-lookup"><span data-stu-id="0c9d4-190">Issues with SAS URL</span></span>
<span data-ttu-id="0c9d4-191">Si va a conectar tooa servicio mediante una dirección URL de SAS y experimentando este error:</span><span class="sxs-lookup"><span data-stu-id="0c9d4-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="0c9d4-192">Compruebe que Hola URL proporciona los permisos necesarios de hello tooread o una lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="0c9d4-193">Compruebe que Hola que dirección URL no ha expirado.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="0c9d4-194">Si Hola URL de SAS se basa en una directiva de acceso, compruebe que la directiva de acceso de hello no ha sido revocada.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c9d4-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c9d4-195">Next steps</span></span>

<span data-ttu-id="0c9d4-196">Si ninguna de las soluciones de hello funciona, enviar su problema a través de la herramienta de comentarios de Hola con el correo electrónico y como muchos detalles sobre el problema de hello incluidos como se pueden, por lo que podemos enviarte para corregir el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="0c9d4-197">toodo, haga clic en **ayuda** menú y, a continuación, haga clic en **enviar comentarios**.</span><span class="sxs-lookup"><span data-stu-id="0c9d4-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Comentarios](./media/storage-explorer-troubleshooting/4022503_en_1.png)
