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
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Guía de solución de problemas del Explorador de Azure Storage

## <a name="introduction"></a>Introducción

Explorador de almacenamiento de Microsoft Azure (vista previa) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux. aplicación Hello puede conectarse a las cuentas de toStorage hospedadas en Azure, la condición soberano nubes y la pila de Azure.

Esta guía resume las soluciones para problemas comunes en el Explorador de Storage.

## <a name="sign-in-issues"></a>Problemas de inicio de sesión

Antes de continuar, pruebe a reiniciar la aplicación y vea si se pueden corregir los problemas de Hola.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Error: Certificado autofirmado de cadena de certificados

Hay varias razones por las este error puede aparecer, y hello más dos motivos principales son los siguientes:

1. aplicación Hello se conecta a través de "proxy transparente", lo que significa un servidor (por ejemplo, el servidor de la compañía) es interceptar tráfico HTTPS, el descifrado y, a continuación, cifrar mediante un certificado autofirmado.

2. Ejecuta una aplicación, como software antivirus, que se inserte un certificado SSL autofirmado en los mensajes de Hola HTTPS que recibirá.

Cuando el Explorador de almacenamiento se encuentra uno de los problemas de hello, puede ya no se sabe si se manipula el mensaje de bienvenida recibido de HTTPS. Si tiene una copia del certificado autofirmado de hello, puede dejar que el Explorador de almacenamiento confiar en él. Si no está seguro de que inserte certificado hello, siga estos pasos toofind:

1. Instale Open SSL.

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (cualquiera de las versiones claro Hola debería ser suficiente)

    - Mac y Linux: debe estar incluido con el sistema operativo.

2. Ejecute Open SSL.

    - Windows: abrir el directorio de instalación de hello, haga clic en **/bin/**y, a continuación, haga doble clic en **openssl.exe**.
    - Mac y Linux: ejecute **openssl** desde un terminal.

3. Ejecute s_client -showcerts -connect microsoft.com:443.

4. Busque certificados autofirmados. Si no está seguro de que están autofirmados, busque en cualquier lugar asunto Hola ("s:") y emisor ("i") se Hola igual.

5. Cuando haya encontrado los certificados autofirmados, para cada una de ellas, copiar y pegar todo el contenido de e incluidas **---BEGIN CERTIFICATE---** demasiado**---END CERTIFICATE---** tooa nueva CER.

6. Abra el Explorador de almacenamiento, haga clic en **editar** > **certificados SSL** > **importar certificados**y, a continuación, use Hola archivo selector toofind, seleccione esta opción, y abrir archivos de CER Hola que ha creado.

Si no se encuentra ningún certificado autofirmado con hello por encima de los pasos, póngase en contacto con nosotros a través de la herramienta de comentarios de Hola para obtener más ayuda.

### <a name="unable-tooretrieve-subscriptions"></a>No se puede tooretrieve suscripciones

Si es que no se puede tooretrieve las suscripciones después de iniciar sesión correctamente, siga estos pasos tootroubleshoot este problema:

- Compruebe que la cuenta tiene acceso toohello suscripciones al iniciar sesión en hello Portal de Azure.

- Asegúrese de que ha iniciado sesión con entorno correcto de hello (Azure, Azure China, Azure en Alemania, gobierno de EE o personalizado entorno/Azure pila).

- Si está detrás de un proxy, asegúrese de que ha configurado el proxy del explorador de almacenamiento de hello correctamente.

- Intente quitar y volver a agregar la cuenta de hello.

- Intente eliminar Hola siguientes archivos desde el directorio raíz (es decir, C:\Users\ContosoUser) y, a continuación, volver a agregar la cuenta de hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Consola de herramientas de desarrollador de Hola de inspección (presionando F12) cuando se firma los mensajes de error:

![herramientas de desarrollo](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Página de autenticación de hello toosee no se puede

Si es que la página de autenticación de hello toosee no se puede, siga estos pasos tootroubleshoot este problema:

- Según la velocidad de saludo de la conexión, puede tardar un poco para tooload de la página de inicio de sesión de hello, espere al menos un minuto antes de cerrar el cuadro de diálogo de autenticación de Hola.

- Si está detrás de un proxy, asegúrese de que ha configurado el proxy del explorador de almacenamiento de hello correctamente.

- Ver la consola para desarrolladores de hello presionando la tecla F12 de Hola. Ver las respuestas de Hola desde la consola para desarrolladores hello y vea si puede encontrar ninguna pista para saber por qué no funciona la autenticación.

### <a name="cannot-remove-account"></a>No se puede quitar la cuenta

Si no se puede tooremove una cuenta o si Hola volver a autenticar vínculo no hace nada, siga estos pasos tootroubleshoot este problema:

- Intente eliminar Hola siguientes archivos desde el directorio raíz y, a continuación, volver a agregar la cuenta de hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Si desea que tooremove SAS adjunta los recursos de almacenamiento, elimine Hola siguientes archivos:

    - Carpeta %AppData%/StorageExplorer para Windows

    - /Users/<su_nombre>/Library/Applicaiton SUpport/StorageExplorer para Mac

    - ~/.config/StorageExplorer para Linux

> [!NOTE]
>  Tendrá tooreenter todas sus credenciales si elimina estos archivos.

## <a name="proxy-issues"></a>Problemas de proxy

En primer lugar, asegúrese de que ese Hola siguiendo la información que especificó son correctos:

- Hola dirección URL del proxy y el puerto número

- Nombre de usuario y contraseña si es necesario por proxy Hola

### <a name="common-solutions"></a>Soluciones comunes

Si sigue experimentando problemas, siga estos pasos tootroubleshoot ellos:

- Si puede conectarse toohello Internet sin usar al proxy, compruebe que el Explorador de almacenamiento funciona sin la configuración del proxy habilitada. Si éste es el caso de hello, puede haber un problema con la configuración de proxy. Trabajar con sus problemas de proxy administrador tooidentify Hola.

- Compruebe que otras aplicaciones que utilicen el servidor proxy de hello funcionan según lo esperado.

- Compruebe que puede conectar el portal de Microsoft Azure toohello mediante el explorador web

- Compruebe que puede recibir las respuestas de los puntos de conexión de servicio. Especifique una de las direcciones URL de punto de conexión en el explorador. Si puede conectarse, debería recibir un InvalidQueryParameterValue o una respuesta XML similar.

- Si otra persona también usa el Explorador de Storage con el servidor proxy, compruebe que pueda conectarse. Si puede conectar, puede tener toocontact el administrador del servidor proxy.

### <a name="tools-for-diagnosing-issues"></a>Herramientas para el diagnóstico de problemas

Si dispone de herramientas de red, como Fiddler para Windows, es posible que los siguientes problemas de hello toodiagnose capaz de:

- Si tienes toowork a través de proxy, puede tener tooconfigure su red tooconnect de herramienta a través de proxy de Hola.

- Compruebe el número de puerto de hello utilizado por la herramienta de red.

- Escriba la dirección URL del host local de Hola y Hola número de puerto de la herramienta de red como configuración de proxy en el Explorador de almacenamiento. Si este isdone correctamente, la herramienta de red se inicia el registro de las solicitudes de red realizadas por los extremos de servicio y toomanagement de explorador de almacenamiento. Por ejemplo, escriba https://cawablobgrs.blob.core.windows.net/ para el extremo de blob en un explorador, y recibirá una respuesta similar a la siguiente hello, lo que sugiere Hola recurso existe, aunque no se puede obtener acceso a él.

![ejemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Póngase en contacto con el administrador del servidor proxy

Si es correcta la configuración de proxy, puede que tenga toocontact el administrador del servidor proxy, y

- Asegúrese de que el proxy no bloquee el tráfico tooAzure administración o recurso de puntos de conexión.

- Comprobar el protocolo de autenticación de hello utilizada por el servidor proxy. En estos momentos, el Explorador de Storage no admite los servidores proxy NTLM.

## <a name="unable-tooretrieve-children-error-message"></a>Mensaje de error "No se puede tooRetrieve elementos secundarios"

Si está conectado tooAzure a través de un servidor proxy, compruebe que la configuración de proxy es correcta. Si se concede acceso tooa recursos de propietario de Hola de suscripción de Hola o la cuenta, compruebe que ha leído o lista de permisos para dicho recurso.

### <a name="issues-with-sas-url"></a>Problemas con la URL de SAS
Si va a conectar tooa servicio mediante una dirección URL de SAS y experimentando este error:

- Compruebe que Hola URL proporciona los permisos necesarios de hello tooread o una lista de recursos.

- Compruebe que Hola que dirección URL no ha expirado.

- Si Hola URL de SAS se basa en una directiva de acceso, compruebe que la directiva de acceso de hello no ha sido revocada.

## <a name="next-steps"></a>Pasos siguientes

Si ninguna de las soluciones de hello funciona, enviar su problema a través de la herramienta de comentarios de Hola con el correo electrónico y como muchos detalles sobre el problema de hello incluidos como se pueden, por lo que podemos enviarte para corregir el problema de Hola.

toodo, haga clic en **ayuda** menú y, a continuación, haga clic en **enviar comentarios**.

![Comentarios](./media/storage-explorer-troubleshooting/4022503_en_1.png)
