---
title: aaaUsing CDN de Azure con CORS | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toowith de red de entrega contenido (CDN) de Azure de uso compartido de recursos entre orígenes (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Uso de la red CDN de Azure con CORS
## <a name="what-is-cors"></a>¿Qué es CORS?
CORS (Cross origen uso compartido de recursos) es una característica HTTP que permite que una aplicación web que se ejecuta en uno de los recursos de tooaccess de dominio en otro dominio. En la posibilidad de Hola de tooreduce de orden de los ataques de scripts entre sitios, todos los exploradores web modernos implementan una restricción de seguridad que se conoce como [directiva de mismo origen](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Esto impide que una página web llame a las API de un dominio distinto.  CORS proporciona un toocall de (dominio de origen de hello) de un origen de tooallow forma segura las API en otro origen.

## <a name="how-it-works"></a>Cómo funciona
Hay dos tipos de solicitudes de CORS, *solicitudes sencillas* y *solicitudes complejas.*

### <a name="for-simple-requests"></a>Para solicitudes sencillas:

1. Explorador de Hello envía la solicitud de CORS de hello con más **origen** encabezado de solicitud HTTP. valor de Hola de este encabezado es el origen de Hola que pueda servir página primaria de hello, que se define como la combinación de Hola de *protocolo,* *dominio,* y *puerto.*  Cuando una página de https://www.contoso.com intenta tooaccess datos de un usuario en el origen de fabrikam.com hello, se enviarían Hola siguiente encabezado de solicitud toofabrikam.com:

   `Origin: https://www.contoso.com`

2. servidor Hello puede responder con cualquiera de hello siguientes:

   * Un encabezado **Access-Control-Allow-Origin** en la respuesta, que indica cuál de los sitios de origen se permite. Por ejemplo:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Código de error HTTP como 403 si Hola servidor no permite la solicitud entre orígenes de hello después de comprobar el encabezado de origen de Hola

   * Un encabezado **Access-Control-Allow-Origin** con un carácter comodín que permite todos los dominios:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Para solicitudes complejas:

Una solicitud compleja una solicitud de CORS donde hello examinador es necesario toosend una *solicitud preparatoria* (es decir, un análisis preliminar) antes de enviar la solicitud CORS real Hola. Hello solicitud preparatoria solicita Hola server permiso si solicitud CORS de hello original puede continuar y es un `OPTIONS` solicitar toohello misma dirección URL.

> [!TIP]
> Para obtener más detalles sobre los flujos de CORS y los errores comunes, ver hello [guía tooCORS para las API de REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Escenarios de origen único o carácter comodín
CORS en la red CDN de Azure funcionará automáticamente sin ninguna configuración adicional cuando hello **acceso Access-Control-Allow-Origin** encabezado se establece toowildcard (*) o un único origen.  CDN Hola almacenará en memoria caché primera respuesta de Hola y las solicitudes posteriores usarán Hola mismo encabezado.

Si las solicitudes se han realizado ya toohello CDN tooCORS anteriores que se establecen en hello su origen, deberá toopurge contenido en su hello tooreload contenido de punto de conexión contenido con hello **acceso Access-Control-Allow-Origin** encabezado.

## <a name="multiple-origin-scenarios"></a>Escenarios de varios orígenes
Si necesita una lista específica de toobe orígenes permitido para CORS tooallow, puede ser un poco más complicado. se produce un problema de Hello cuando Hola CDN almacena en caché hello **acceso Access-Control-Allow-Origin** encabezado para el primer origen de CORS Hola.  Cuando un origen diferente de CORS realiza una solicitud posterior, CDN Hola servirá hello en caché **acceso Access-Control-Allow-Origin** encabezado, que no coincidirán.  Hay varias toocorrect formas esto.

### <a name="azure-cdn-premium-from-verizon"></a>Red CDN premium de Azure de Verizon
Hola tooenable de mejor manera es toouse **Premium de CDN de Azure de Verizon**, que expone algunas funciones avanzadas. 

Necesitará demasiado[crear una regla de](cdn-rules-engine.md) toocheck hello **origen** encabezado de solicitud de saludo.  Si es un origen válido, la regla establecerá hello **acceso Access-Control-Allow-Origin** encabezado con el origen de hello proporcionado en la solicitud de saludo.  Si especifica el origen Hola Hola **origen** encabezado no está permitido, la regla debe omitir hello **acceso Access-Control-Allow-Origin** encabezado lo que hará que la solicitud de hello explorador tooreject Hola. 

Hay dos toodo formas esto con el motor de reglas de Hola.  En ambos casos, Hola **acceso Access-Control-Allow-Origin** completamente se omite el encabezado de servidor de origen del archivo de hello, motor de reglas de CDN Hola administra completamente Hola permite orígenes CORS.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Una expresión regular con todos los orígenes válidos
En este caso, creará una expresión regular que incluye todos los orígenes de hello desea tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> **red CDN de Azure de Verizon** utiliza las [expresiones regulares compatibles con Perl](http://pcre.org/) como su motor de expresiones regulares.  Puede usar una herramienta como [101 de expresiones regulares](https://regex101.com/) toovalidate la expresión regular.  Tenga en cuenta que Hola "/" de caracteres es válido en expresiones regulares y no necesita toobe caracteres de escape, sin embargo, ese carácter de la secuencia de escape se considera una práctica recomendada y es compatible con algunos controles de validación de expresión regular.
> 
> 

Si se coincide con la expresión regular de hello, la regla reemplazará hello **acceso Access-Control-Allow-Origin** encabezado (si existe) del origen de hello con origen de Hola que envió la solicitud de saludo.  También puede añadir encabezados de CORS adicionales, como **Access-Control-Allow-Methods**.

![Ejemplo de reglas con expresiones regulares](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Regla de encabezado de solicitud para cada origen
En lugar de expresiones regulares, en su lugar, puede crear otro regla para cada origen desea tooallow con hello **comodín del encabezado de solicitud** [coincide con la condición](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Como con el método de expresión regular de hello, Hola el motor de reglas encabezados conjuntos hello CORS por sí solo. 

![Ejemplo de reglas sin expresiones regulares](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> En el ejemplo de Hola anterior, Hola uso del carácter comodín de Hola * indica que el motor de reglas de hello toomatch HTTP y HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Estándar de red CDN de Azure
En los perfiles de red CDN de Azure estándar, Hola solo mecanismo tooallow para varios orígenes sin uso Hola de origen de comodín de hello es toouse [almacenamiento en memoria caché en la cadena de consulta](cdn-query-string.md).  Es necesario tooenable configuración de la cadena de consulta para el extremo de red CDN Hola y, a continuación, utilice una cadena de consulta única para las solicitudes de cada dominio permitido. Esto producirá Hola CDN almacenamiento en caché un objeto independiente para cada cadena de consulta única. Este enfoque no es lo ideal, sin embargo, que se producirá en varias copias de hello mismo archivo almacenado en caché en hello CDN.  

