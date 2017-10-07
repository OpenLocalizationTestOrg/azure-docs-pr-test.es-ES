---
title: compatibilidad con recursos compartidos (CORS) de recursos de origen aaaCross | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooenable compatibilidad con CORS para hello servicios de almacenamiento de Microsoft Azure."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Compatibilidad de uso compartido de recursos entre orígenes (CORS) para hello servicios de almacenamiento de Azure
A partir de la versión 2013-08-15, servicios de almacenamiento de Azure de Hola admiten uso compartido de recursos entre orígenes (CORS) para servicios de Blob, tabla, cola y archivo de Hola. CORS es una característica HTTP que permite que una aplicación web que se ejecuta en uno de los recursos de tooaccess de dominio en otro dominio. Los exploradores Web implementan una restricción de seguridad que se conoce como [directiva de mismo origen](http://www.w3.org/Security/wiki/Same_Origin_Policy) que evita que una página web que realiza la llamada API en un dominio diferente; CORS proporciona un toocall de forma segura tooallow un dominio (dominio de origen de hello) API en otro dominio. Vea hello [especificación CORS](http://www.w3.org/TR/cors/) para obtener detalles sobre CORS.

Puede establecer reglas de CORS individualmente para cada uno de hello servicios de almacenamiento, mediante una llamada a [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [establecer propiedades del servicio cola](https://msdn.microsoft.com/library/hh452232.aspx), y [establecer propiedades del servicio tabla](https://msdn.microsoft.com/library/hh452240.aspx). Una vez establecidas las reglas de CORS de hello para el servicio de hello, una solicitud autenticada correctamente realizada en el servicio de Hola desde un dominio diferente será evaluada toodetermine si se permite según las reglas de toohello que ha especificado.

> [!NOTE]
> Tenga en cuenta que CORS no es ningún mecanismo de autenticación. Cualquier solicitud realizada en un recurso de almacenamiento cuando se ha habilitado CORS debe tener una firma de autenticación adecuada o bien se debe realizar en un recurso público.
> 
> 

## <a name="understanding-cors-requests"></a>Descripción de las solicitudes de CORS
Una solicitud de CORS de un dominio de origen puede estar formada por dos solicitudes diferentes:

* Una solicitud preparatoria, que consulta las restricciones de CORS de hello impuestas por servicio Hola. solicitud preparatoria Hello es necesario a menos que sea el método de solicitud de hello un [método simple](http://www.w3.org/TR/cors/), lo que significa GET, HEAD o POST.
* Hola solicitud real, realizada en un recurso de hello deseado.

### <a name="preflight-request"></a>Solicitud preparatoria
las consultas de solicitud preparatoria de Hola Hola restricciones de CORS que se han establecido por el propietario de la cuenta de hello para el servicio de almacenamiento de Hola. Explorador de web de Hello (u otro agente de usuario) envía una solicitud OPTIONS que incluye los encabezados de solicitud de hello, dominio de origen y de método. servicio de almacenamiento de Hello evalúa operación Hola diseñado basándose en un conjunto preconfigurado de reglas de CORS que especifican qué dominios de origen, métodos de respuesta y encabezados de solicitud se pueden especificar en una solicitud real para un recurso de almacenamiento.

Si se ha habilitado CORS para el servicio de Hola y hay una regla de CORS que coincida con la solicitud preparatoria de hello, servicio de hello responde con el código de estado 200 (OK) e incluye encabezados de Control de acceso de hello necesario en respuesta Hola.

Si no se ha habilitado CORS para el servicio de Hola o no hay ninguna regla CORS coincide con la solicitud preparatoria de hello, servicio de hello responderá con el código de estado 403 (prohibido).

Si no contiene la solicitud OPTIONS de Hola Hola encabezados CORS necesarios (Hola origen y encabezados de acceso-Access-Control-Request-Method), servicio de hello responderá con el código de estado 400 (solicitud incorrecta).

Tenga en cuenta que una solicitud preparatoria se evalúa con el servicio de hello (Blob, cola y tabla) y no con hello recurso solicitado. propietario de la cuenta de Hello debe haber habilitado CORS como parte de las propiedades de servicio de la cuenta de hello en orden para hello solicitud toosucceed.

### <a name="actual-request"></a>Solicitud real
Una vez que se aceptó la solicitud preparatoria de Hola y se devuelve la respuesta de hello, Explorador de hello enviará la solicitud real de hello en un recurso de almacenamiento de Hola. Explorador de Hello denegará la solicitud real Hola inmediatamente si hello se rechaza la solicitud preparatoria.

solicitud real Hola se trata como una solicitud normal en el servicio de almacenamiento de Hola. presencia de Hola de encabezado Origin de Hola indica que hello es una solicitud CORS y servicio de hello comprobará hello CORS reglas de coincidencia. Si se encuentra una coincidencia, encabezados de Control de acceso de hello son toohello agregado respuesta y envían a atrás toohello cliente. Si no se encuentra una coincidencia, no se devuelven los encabezados de Control de acceso de CORS Hola.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Habilitar CORS para servicios de almacenamiento de Azure Hola
Reglas de CORS se establecen en el nivel de servicio de hello, por lo que necesita tooenable o deshabilita CORS para cada servicio (Blob, cola y tabla) por separado. De forma predeterminada, CORS está deshabilitado para todos los servicios. tooenable CORS, necesita propiedades del servicio correspondiente hello tooset con la versión 2013-08-15 o posterior y agregar reglas de CORS toohello propiedades del servicio. Para obtener más información acerca de cómo tooenable o deshabilitar CORS para un servicio y cómo las reglas tooset CORS, por favor, consulte demasiado[Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [establecer propiedades del servicio cola](https://msdn.microsoft.com/library/hh452232.aspx), y [Establecer tabla Propiedades del servicio](https://msdn.microsoft.com/library/hh452240.aspx).

A continuación se muestra un ejemplo de una única regla de CORS que se ha especificado mediante una operación Set Service Properties:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Todos los elementos incluidos en la regla de CORS de Hola se describen a continuación:

* **AllowedOrigins**: dominios de origen de Hola que se permiten toomake una solicitud en el almacenamiento de Hola de servicio a través de CORS. Hola origen dominio es Hola desde qué Hola se origina la solicitud. Tenga en cuenta que el origen de hello debe ser una coincidencia exacta entre mayúsculas y minúsculas con el origen de Hola que el agente de usuario de hello envía toohello servicio. También puede utilizar el carácter comodín de hello ' *' tooallow todas las solicitudes de toomake de dominios de origen a través de CORS. En el ejemplo de Hola anterior, Hola dominios [http://www.contoso.com](http://www.contoso.com) y [http://www.fabrikam.com](http://www.fabrikam.com) pueden realizar solicitudes de servicio de hello mediante CORS.
* **AllowedMethods**: ese dominio de origen Hola los Hola métodos (verbos de solicitud HTTP) puede usar para una solicitud de CORS. En el ejemplo de Hola anterior, se permiten que solamente las solicitudes GET y PUT.
* **AllowedHeaders**: encabezados de solicitud de Hola que puede especificar ese dominio de origen de hello en solicitud CORS de Hola. En el ejemplo de Hola anterior, se permiten todos los encabezados de metadatos que empiecen por x-ms-meta-data, x-ms-meta-destino y x-ms-meta-abc. Tenga en cuenta ese carácter comodín de hello ' *' indica que cualquier encabezado que empiece con hello especificado se permite el prefijo.
* **ExposedHeaders**: Hola encabezados de respuesta que se pueden enviados en la solicitud de CORS de toohello de respuesta de Hola y expuestos por el emisor de solicitud de hello explorador toohello. En el ejemplo de Hola anterior, el Explorador de hello es siguiendo las instrucciones tooexpose cualquier encabezado que empiece con x-ms-meta.
* **MaxAgeInSeconds**: Hola máxima cantidad de tiempo que un explorador debe almacenar en caché solicitud preparatoria de opciones de Hola.

Hello servicios de almacenamiento de Azure admiten especificar encabezados con prefijo para ambos hello **AllowedHeaders** y **ExposedHeaders** elementos. tooallow una categoría de encabezados, puede especificar una categoría de toothat prefijo común. Por ejemplo, si se especifica *x-ms-meta*como un encabezado con prefijo, se establece una regla que coincidirá con todos los encabezados que empiecen por x-ms-meta.

Hola siguientes limitaciones aplica reglas de tooCORS:

* Puede especificar una toofive reglas CORS por servicio de almacenamiento (Blob, tabla y cola).
* tamaño máximo de Hola de todas las reglas cors en la solicitud de hello, excluidas las etiquetas XML, no debe superar los 2 KB.
* longitud de Hola de un encabezado permitido, el encabezado expuesto o el origen permitido no debe superar los 256 caracteres.
* Los encabezados permitidos y los encabezados expuestos pueden ser:
  * Encabezados literales, donde se proporciona nombre exacto del encabezado de hello, como **x-ms-meta-processed**. Puede especificarse un máximo de 64 encabezados literales en la solicitud de saludo.
  * Encabezados con prefijo, donde se proporciona un prefijo de encabezado de hello, como **x-ms-meta-data***. Especificar un prefijo de esta manera se permite o expone cualquier encabezado que comience con hello tiene prefijo. Un máximo de dos encabezados con prefijo puede especificarse en la solicitud de saludo.
* Hola métodos (o verbos HTTP) especificados en hello **AllowedMethods** deben ajustarse métodos toohello compatibles con las API del servicio de almacenamiento de Azure. Los métodos admitidos son DELETE, GET, HEAD, MERGE, POST, OPTIONS y PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Descripción de la lógica de evaluación de reglas de CORS
Cuando un servicio de almacenamiento recibe una solicitud preparatoria o real, evalúa esa solicitud según las reglas de CORS de Hola que ha establecido para el servicio de Hola a través de la operación Set Service Properties adecuada de Hola. Reglas de CORS se evalúan en orden de hello en el que se establecieron en el cuerpo de la solicitud de Hola de hello operación Set Service Properties.

Las reglas de CORS se evalúan de la manera siguiente:

1. En primer lugar, se comprueba el dominio de origen de saludo de solicitud de hello en dominios de hello enumerados para hello **AllowedOrigins** elemento. Si se admiten todos los dominios con carácter comodín de Hola o dominio de origen de Hola se incluye en la lista de hello ' *', continúa de la evaluación de las reglas. Si no se incluye el dominio de origen de hello, solicitud de hello produce un error.
2. A continuación, se comprueba el método hello (o verbo HTTP) de solicitud de hello frente a métodos de hello recogidos en hello **AllowedMethods** elemento. Si el método hello se incluye en la lista de hello, evaluación de reglas continúa; de lo contrario, a continuación, se produce un error en la solicitud de saludo.
3. Si la solicitud de hello coincide con una regla en su dominio de origen y el método, esa regla está seleccionado tooprocess Hola solicitud y no se evalúa ninguna otra regla. Antes de que pueda realizar correctamente la solicitud de hello, sin embargo, se comprueban todos los encabezados especificados en la solicitud de hello en los encabezados Hola Hola **AllowedHeaders** elemento. Si los encabezados de hello enviados no coinciden Hola encabezados permitido, se produce un error en la solicitud de saludo.

Puesto que las reglas de Hola se procesan en orden de hello están presentes en el cuerpo de la solicitud de hello, según los procedimientos recomendados que especifique reglas más restrictivas de hello con respetan tooorigins en primer lugar en la lista de hello, por lo que estos se evalúan primero. Especifique las reglas que sean menos restrictivas; por ejemplo, un tooallow regla final Hola de lista Hola todos los orígenes.

### <a name="example--cors-rules-evaluation"></a>Ejemplo: evaluación de reglas de CORS
Hello en el ejemplo siguiente se muestra un cuerpo de solicitud parcial para un reglas de CORS de tooset de operación para servicios de almacenamiento de Hola. Vea [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [establecer propiedades del servicio cola](https://msdn.microsoft.com/library/hh452232.aspx), y [establecer propiedades del servicio tabla](https://msdn.microsoft.com/library/hh452240.aspx) para obtener más información sobre la creación de solicitud de saludo.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

A continuación, considere la posibilidad de hello siguiendo las solicitudes CORS:

| Solicitud |  |  | Response |  |
| --- | --- | --- | --- | --- |
| **Método** |**Origen** |**Encabezados de solicitud** |**Coincidencia de regla** |**Resultado** |
| **PUT** |http://www.contoso.com |x-ms-blob-content-type |Primera regla |Correcto |
| **GET** |http://www.contoso.com |x-ms-blob-content-type |Segunda regla |Correcto |
| **GET** |http://www.contoso.com |x-ms-client-request-id |Segunda regla |Error |

primera solicitud de Hello coincide con la primera regla de hello: Hola permitida orígenes coincide con el dominio de origen de hello, Hola permitida métodos coincide con el método hello y encabezado Hola coincide con hello encabezados – permitido y por lo que se realiza correctamente.

segunda solicitud de Hello no hace coincidir primera regla de hello porque método hello no coincide con hello permitida métodos. Sin embargo,, coincidir segunda regla hello, para que se realice correctamente.

tercera solicitud de Hello coincide con la segunda regla de hello en su dominio de origen y el método, por lo que no se evalúa ninguna otra regla. Sin embargo, Hola *encabezado x-ms-client-request-id* no está permitido por la segunda regla hello, por lo que se produce un error en solicitud de hello, a pesar de los hechos de Hola que semántica Hola de regla tercer Hola habría permitido que toosucceed.

> [!NOTE]
> Aunque este ejemplo se muestra una regla menos restrictiva antes de otra más restrictiva, por lo general se recomienda hello es reglas más restrictivas de hello toolist por primera vez.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Descripción de cómo se establece el encabezado Vary de Hola
Hola *variación* encabezado es un encabezado HTTP/1.1 estándar que consta de un conjunto de campos de encabezado de solicitud que aconsejan agente de usuario o el explorador Hola acerca de los criterios de Hola que seleccionó Hola server tooprocess Hola solicitud. Hola *variación* encabezado se utiliza principalmente para almacenamiento en caché de servidores proxy, exploradores y redes CDN, que lo utiliza toodetermine cómo debe almacenarse en caché respuesta Hola. Para obtener más información, vea especificación de Hola para hello [encabezado Vary](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Cuando el Explorador de Hola o de otro agente de usuario almacena en caché Hola respuesta de una solicitud CORS, dominio de origen de Hola se almacena en caché como Hola permitido de origen. Cuando un segundo problemas de dominio Hola misma solicitud para un recurso de almacenamiento mientras está activa la memoria caché de hello, agente de usuario de hello recupera el dominio de origen almacenados en caché de Hola. dominio de segundo Hello no coincide con dominio almacenada en caché de hello, por lo que se produce un error en la solicitud de hello cuando de lo contrario se realizaría correctamente. En algunos casos, el almacenamiento de Azure establece encabezado Vary de hello demasiado**origen** tooinstruct Hola usuario toosend Hola posteriores CORS solicitud toohello servicio del agente cuando Hola solicitando dominio difiere de hello almacena en caché de origen.

Almacenamiento de Azure establece hello *variación* encabezado demasiado**origen** para las solicitudes GET/HEAD reales en hello casos siguientes:

* Si la solicitud Hola origen coincide exactamente con hello permite origen definido por una regla de CORS. toobe una coincidencia exacta, regla de CORS de hello no puede incluir un carácter comodín ' * ' caracteres.
* No hay ningún origen de regla de la solicitud de hello coincidente, pero se ha habilitado CORS para el servicio de almacenamiento de Hola.

En el caso de hello donde una solicitud GET/HEAD coincida con una regla CORS que permita todos los orígenes, respuesta de hello indica que se permiten todos los orígenes y memoria caché del agente de usuario de hello permitirá solicitudes posteriores de cualquier dominio de origen mientras está activa la memoria caché de Hola.

Tenga en cuenta que para las solicitudes que utilizan otros métodos distintos de GET/HEAD, servicios de almacenamiento de hello no establecerá encabezado Vary de hello, ya que no se almacenan en caché métodos toothese de respuestas por los agentes de usuario.

Hello tabla siguiente indica el almacenamiento de Azure cómo responderá a las solicitudes tooGET/HEAD según Hola anteriormente mencionados casos:

| Solicitud | Configuración de la cuenta y resultado de la evaluación de reglas |  |  | Response |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Encabezado Origin presente en la solicitud** |**Reglas de CORS especificadas para este servicio** |**Existe una regla de coincidencia que permite todos los orígenes (*)** |**Existe una regla de coincidencia para una coincidencia exacta del origen** |**La respuesta incluye tooOrigin de conjunto de encabezado Vary** |**La respuesta incluye Access-Control-Allowed-Origin: "*"** |**La respuesta incluye Access-Control-Exposed-Headers** |
| No |No |No |No |No |No |No |
| No |Sí |No |No |Sí |No |No |
| No |Sí |Sí |No |No |Sí |Sí |
| Sí |No |No |No |No |No |No |
| Sí |Sí |No |Sí |Sí |No |Sí |
| Sí |Sí |No |No |Sí |No |No |
| Sí |Sí |Sí |No |No |Sí |Sí |

## <a name="billing-for-cors-requests"></a>Facturación de las solicitudes de CORS
Las solicitudes preparatorias correctas se cobran si ha habilitado CORS para cualquiera de los servicios de almacenamiento de Hola para su cuenta (mediante una llamada a [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [establecer propiedades del servicio cola](https://msdn.microsoft.com/library/hh452232.aspx), o [ Establecer propiedades del servicio tabla](https://msdn.microsoft.com/library/hh452240.aspx)). toominimize cargos, considere la posibilidad de establecer hello **MaxAgeInSeconds** elemento en su CORS reglas tooa de valor grande para que hello agente de usuario almacena en caché la solicitud de saludo.

Las solicitudes preparatorias erróneas no se cargan en cuenta.

## <a name="next-steps"></a>Pasos siguientes
[Definición de las propiedades del servicio Blob](https://msdn.microsoft.com/library/hh452235.aspx)

[Definición de las propiedades del servicio Cola](https://msdn.microsoft.com/library/hh452232.aspx)

[Definición de las propiedades del servicio Tabla](https://msdn.microsoft.com/library/hh452240.aspx)

[Especificación de uso compartido de recursos entre orígenes de W3C](http://www.w3.org/TR/cors/)

