---
title: "puntos de conexión de red CDN de Azure de aaaTroubleshooting devolver estado 404 | Documentos de Microsoft"
description: "Solucione problemas de los códigos de error 404 con los puntos de conexión de la red CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Solución de problemas de redes CDN que devuelven errores 404
Este artículo le ayudará a solucionar los problemas con los [puntos de conexión de redes CDN](cdn-create-new-endpoint.md) que devuelven errores 404.

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, también puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**.

## <a name="symptom"></a>Síntoma
Ha creado un perfil de CDN y un punto de conexión, pero parece que su contenido no disponible en la red CDN Hola toobe.  Usuarios que intentan tooaccess su contenido a través de la dirección URL de CDN Hola recibir códigos de estado HTTP 404. 

## <a name="cause"></a>Causa
Hay varias causas posibles, por nombrar algunas:

* origen del archivo de Hello no está visible toohello CDN
* punto de conexión de Hello está mal configurado, provocando toolook CDN Hola en el lugar incorrecto Hola
* host de Hello está rechazando el encabezado de host de Hola de CDN Hola
* punto de conexión de Hello no ha tenido tiempo toopropagate a lo largo de la red CDN Hola

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas
> [!IMPORTANT]
> Después de crear un punto de conexión de red CDN, no inmediatamente estará disponible para su uso, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.  Para los perfiles de la <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completa en un minuto.  Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.  Si completa los pasos de hello en este documento y todavía recibe 404 respuestas, considere la posibilidad de espera unos toocheck horas nuevo antes de abrir una incidencia de soporte técnico.
> 
> 

### <a name="check-hello-origin-file"></a>Compruebe el archivo de origen Hola
En primer lugar, debemos comprobamos Hola ese archivo hello queremos almacenados en memoria caché está disponible en el origen y es accesible públicamente.  Hola toodo de manera más rápida que está tooopen un explorador en una sesión en privado o de incógnito y vaya directamente toohello archivo.  Simplemente escriba o pegue la URL de hello en el cuadro de dirección de Hola y vea si esto da lugar a archivo hello esperados.  En este ejemplo, voy toouse un archivo necesario en una cuenta de almacenamiento de Azure, puede tener acceso en `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Como puede ver, correctamente pasa la prueba de Hola.

![¡Éxito!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Aunque esto es más rápida de hello y tooverify de manera más fácil el archivo esté disponible públicamente, algunas configuraciones de red de su organización pudieron dar Hola en realidad que este archivo se encuentra disponible públicamente cuando es, de hecho, sólo toousers visible de la red ( incluso si está hospedado en Azure).  Si tienes un explorador externo desde las que puede probar, como un dispositivo móvil que no está conectada a la red de la organización tooyour o una máquina virtual en Azure, que sería la mejor.
> 
> 

### <a name="check-hello-origin-settings"></a>Compruebe la configuración de origen de Hola
Ahora que hemos comprobado archivo hello esté disponible públicamente en internet de Hola, debemos comprobamos la configuración de origen.  Hola [Portal de Azure](https://portal.azure.com), perfil de CDN tooyour y haga clic en el punto de conexión de Hola que esté solucionando.  Hola resultante **extremo** hoja, haga clic en el origen de Hola.  

![Hoja de punto de conexión con origen resaltado](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Hola **origen** aparece hoja. 

![Hoja de origen](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Tipo de origen y nombre del host
Comprobar hello **tipo de origen** sea correcto y compruebe hello **nombre de host de origen**.  En el ejemplo, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, parte hostname de Hola de hello dirección URL es `cdndocdemo.blob.core.windows.net`.  Como puede ver en la captura de pantalla de hello, esto es correcto.  Para el almacenamiento de Azure, aplicación Web y orígenes de servicio en la nube, Hola **nombre de host de origen** campo es una lista desplegable, por lo que no es necesario tooworry sobre él correctamente.  Sin embargo, si utiliza un origen personalizado, es *absolutamente necesario* que el nombre de host se haya escrito correctamente.

#### <a name="http-and-https-ports"></a>Puertos HTTP y HTTPS
Hola otro toocheck lo aquí es el **HTTP** y **puertos HTTPS**.  En la mayoría de los casos, los puertos 80 y 443 son correctos y no requerirá ningún cambio.  Sin embargo, si el servidor de origen de hello está escuchando en un puerto diferente, que tendrá toobe que aquí se representa.  Si no está seguro, simplemente mirar Hola URL para el archivo de origen.  especificaciones de HTTPS y HTTP Hola especifican los puertos 80 y 443 como valores predeterminados de Hola. En la dirección URL, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, no se especifica un puerto, por lo que se asume el valor predeterminado de hello 443 y la configuración es correcta.  

Sin embargo, decir Hola URL para el archivo de origen que se ha probado anteriormente es `http://www.contoso.com:8080/file.txt`.  Hola Nota `:8080` final Hola de segmento de nombre de host de Hola.  Que indica el puerto de hello explorador toouse `8080` tooconnect toohello servidor web `www.contoso.com`, por lo que necesitará tooenter 8080 en hello **puerto HTTP** campo.  Es importante toonote esta configuración de puertos sólo afectan a qué punto de conexión de puerto hello usa información de tooretrieve de origen de Hola.

> [!NOTE]
> **Azure CDN de Akamai** puntos de conexión no permita que el intervalo de puertos TCP completa de Hola para orígenes.  Para obtener una lista de los puertos de origen que no se permiten, consulte [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Puertos de origen permitidos de la red CDN de Azure de Akamai).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Compruebe la configuración de punto de conexión de Hola
En hello **extremo** hoja, haga clic en hello **configurar** botón.

![Hoja de punto de conexión con el botón Configurar resaltado](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Hola del punto de conexión **configurar** aparece hoja.

![Hoja Configurar](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protocolos
Para **protocolos**, compruebe que está seleccionado el protocolo de hello utilizado por los clientes de Hola.  Hello mismo protocolo usado por el cliente de hello será Hola utiliza una origen de hello tooaccess, por lo que es puertos de origen de hello toohave importante están configurados correctamente en la sección anterior de Hola.  punto de conexión de Hello solo escucha en hello predeterminado puertos HTTP y HTTPS (80 y 443), independientemente de los puertos de origen Hola.

Volvamos tooour ejemplo hipotético con `http://www.contoso.com:8080/file.txt`.  Como recordará, Contoso especificó `8080` como puerto HTTP, pero supongamos también que se especificó `44300` como puerto HTTPS.  Si se creó un punto de conexión denominado `contoso`, el nombre de host del punto de conexión de la red CDN sería `contoso.azureedge.net`.  Una solicitud de `http://contoso.azureedge.net/file.txt` es una solicitud HTTP, por lo que el punto de conexión de hello utilizaría HTTP en el puerto 8080 tooretrieve desde origen Hola.  Una solicitud segura a través de HTTPS, `https://contoso.azureedge.net/file.txt`, causaría hello toouse de extremo HTTPS en el puerto 44300 al recuperar Hola archivo de origen de Hola.

#### <a name="origin-host-header"></a>Encabezado del host de origen
Hola **encabezado de host de origen** es el valor del encabezado de host de Hola envía toohello origen con cada solicitud.  En la mayoría de los casos, esto debería ser Hola igual como hello **nombre de host de origen** se comprobó anteriormente.  Un valor incorrecto de este campo normalmente no provocará 404 Estados, pero es probable que toocause otros Estados 4xx, dependiendo de qué origen Hola espera.

#### <a name="origin-path"></a>Ruta de acceso de origen
Por último, debemos comprobar la **ruta de acceso de origen**.  De manera predeterminada esta estará en blanco.  Sólo debe usar este campo si desea que el ámbito de hello toonarrow de recursos de hello hospedado por el origen que desee toomake disponible en la red CDN Hola.  

Por ejemplo, en el punto de conexión, deseaba todos los recursos en mi toobe de cuenta de almacenamiento disponible, por lo que deja **ruta de acceso de origen** en blanco.  Esto significa que una solicitud demasiado`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` da como resultado una conexión desde el punto de conexión demasiado`cdndocdemo.core.windows.net` que solicita `/publicblob/lorem.txt`.  Del mismo modo, una solicitud de `https://cdndocdemo.azureedge.net/donotcache/status.png` resultados de solicitud de punto de conexión de hello `/donotcache/status.png` desde origen Hola.

Pero ¿qué ocurre si no desea toouse Hola CDN para cada ruta de acceso en mi origen?  Digamos que deseaba solo tooexpose hello `publicblob` ruta de acceso.  Si especifica */publicblob* en mi **ruta de acceso de origen** campo, lo que hará que Hola extremo tooinsert */publicblob* antes de cada solicitud realizada toohello origen.  Esto significa que esa solicitud de Hola para `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` ahora tendrá realmente parte de la solicitud de Hola de dirección URL de hello, `/publicblob/lorem.txt`y anexar `/publicblob` toohello principio. Esto da como resultado una solicitud para `/publicblob/publicblob/lorem.txt` desde origen Hola.  Si esa ruta de acceso no resuelve tooan real del archivo, el origen de hello devolverá un estado 404.  Hola lorem.txt de tooretrieve de dirección URL correcta en este ejemplo, sería realmente `https://cdndocdemo.azureedge.net/lorem.txt`.  Tenga en cuenta que no incluimos hello */publicblob* ruta de acceso en absoluto, ya que parte de la solicitud de Hola de Hola dirección URL es `/lorem.txt` y agrega el punto de conexión de hello `/publicblob`, da lugar a `/publicblob/lorem.txt` pasarlo solicitud hello toohello origen .

