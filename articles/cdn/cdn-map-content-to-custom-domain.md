---
title: dominio personalizado del contenido tooa aaaMap CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomap CDN de Azure contenido tooa de dominio personalizado."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Asignar un dominio personalizado de CDN de Azure tooa contenido
Puede asignar un punto de conexión de la red CDN de tooa de dominio personalizado en orden toouse su propio nombre de dominio en las direcciones URL toocached contenido en lugar de utilizar un subdominio de azureedge.net.

El punto de conexión de red CDN de tooa de dominio personalizado no hay toomap de dos maneras:

1. [Crear un registro CNAME con su registrador de dominios y asignar el extremo de red CDN de toohello dominio y subdominio personalizado](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Un registro CNAME es una característica DNS que se asigna un dominio de origen, como `www.contosocdn.com` o `cdn.contoso.com`, tooa dominio de destino. En este caso, el dominio de origen de hello es su dominio y subdominio personalizados (un subdominio, como **www** o **cdn** siempre es necesario). dominio de destino de Hello es el punto de conexión.  
   
    proceso de Hola de asignar el dominio personalizado tooyour punto de conexión, sin embargo, podría en un breve período de tiempo de inactividad para el dominio de hello mientras está registrando dominio Hola Hola Portal de Azure.
2. [Agregar un paso de registro intermedio con **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Si el dominio personalizado atiende actualmente una aplicación con un contrato de nivel de servicio (SLA) exige que no haya ningún tiempo de inactividad, puede usar hello Azure **cdnverify** tooprovide subdominio un registro intermedio paso de modo que los usuarios será capaz de tooaccess su dominio mientras Hola DNS asignación tiene lugar.  

Después de registrar su dominio personalizado utilizando uno de Hola por encima de los procedimientos, le interesará demasiado[Compruebe el punto de conexión hace referencia a ese subdominio personalizado de hello](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> Debe crear un registro CNAME con su toomap del registrador de dominios el dominio toohello punto de conexión. Los registros CNAME asignan subdominios específicos, como `www.contoso.com` o `cdn.contoso.com`. No es posible toomap un dominio raíz de tooa registro CNAME, como `contoso.com`.
> 
> Un subdominio solamente se puede asociar con un extremo de red CDN. Hola registro CNAME que crea enrutará todo el tráfico dirigido toohello subdominio toohello especifica el punto de conexión.  Por ejemplo, si asocia `www.contoso.com` con su punto de conexión de CDN, no puede asociarlo con otros puntos de conexión de Azure, como un punto de conexión de cuenta de almacenamiento o un punto de conexión de servicio en la nube. Sin embargo, puede usar distintos subdominios de hello mismo dominio de los puntos de conexión de servicio diferente. También puede asignar diversos subdominios toohello mismo punto de conexión de red CDN.
> 
> Para **CDN de Azure de Verizon** en los puntos de conexión (ediciones Standard y Premium), tenga en cuenta que ocupe demasiado**90 minutos** para nodos de borde de toopropagate tooCDN de cambios de dominio personalizado.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Registrar un dominio personalizado para un punto de conexión de red CDN de Azure
1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).
2. Haga clic en **examinar**, a continuación, **perfiles de red CDN**, Hola, a continuación, perfil de CDN con el punto de conexión de Hola se desea dominio personalizado de toomap tooa.  
3. Hola **perfil de CDN** hoja, haga clic en el extremo de red CDN Hola con el que desea subdominio de hello tooassociate.
4. Hola parte superior de hoja de punto de conexión de hello, haga clic en hello **agregar un dominio personalizado** botón.  Hola **agregar un dominio personalizado** hoja, podrá ver el nombre de host del punto de conexión de hello, derivado del extremo de red CDN, toouse para crear un nuevo registro CNAME. Hola formato de dirección del nombre de host de hello aparecerá como  **&lt;EndpointName >. azureedge.net**.  Puede copiar este toouse de nombre de host en la creación de registro CNAME Hola.  
5. Navegar por el sitio web del registrador de dominios de tooyour y busque la sección hello para la creación de registros DNS. Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.
6. Busque la sección de Hola para administrar registros CNAME. Puede tener una página de configuración avanzada de toogo tooan y buscar palabras hello CNAME, Alias o subdominios.
7. Crear un nuevo registro CNAME que asigne el subdominio elegido (por ejemplo, **www** o **cdn**) nombre de host de toohello proporcionado en hello **agregar un dominio personalizado** hoja. 
8. Devolver toohello **agregar un dominio personalizado** hoja y escriba su dominio personalizado, incluido el subdominio de hello, en el cuadro de diálogo de Hola. Por ejemplo, escriba el nombre de dominio de hello en formato de hello `www.contoso.com` o `cdn.contoso.com`.   
   
   Azure comprobará que existe el registro CNAME de hello para el nombre de dominio de Hola que ha escrito. Si Hola CNAME es correcto, se valida su dominio personalizado.  Para **CDN de Azure de Verizon** puntos de conexión (ediciones Standard y Premium), pueden tardar hasta too90 minutos para los nodos de borde CDN, de dominio personalizado configuración toopropagate tooall sin embargo.  
   
   Tenga en cuenta que en algunos casos, puede tardar tiempo para los servidores de tooname de hello CNAME toopropagate registro de hello Internet. Si el dominio no se valida inmediatamente y cree Hola registro CNAME es correcto, espere unos minutos y vuelva a intentarlo.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Registrar un dominio personalizado para un punto de conexión de red CDN de Azure mediante el subdominio cdnverify intermedio de Hola
1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).
2. Haga clic en **examinar**, a continuación, **perfiles de red CDN**, Hola, a continuación, perfil de CDN con el punto de conexión de Hola se desea dominio personalizado de toomap tooa.  
3. Hola **perfil de CDN** hoja, haga clic en el extremo de red CDN Hola con el que desea subdominio de hello tooassociate.
4. Hola parte superior de hoja de punto de conexión de hello, haga clic en hello **agregar un dominio personalizado** botón.  Hola **agregar un dominio personalizado** hoja, podrá ver el nombre de host del punto de conexión de hello, derivado del extremo de red CDN, toouse para crear un nuevo registro CNAME. Hola formato de dirección del nombre de host de hello aparecerá como  **&lt;EndpointName >. azureedge.net**.  Puede copiar este toouse de nombre de host en la creación de registro CNAME Hola.
5. Navegar por el sitio web del registrador de dominios de tooyour y busque la sección hello para la creación de registros DNS. Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.
6. Busque la sección de Hola para administrar registros CNAME. Puede tener una página de configuración avanzada de toogo tooan y buscar palabras hello **CNAME**, **Alias**, o **subdominios**.
7. Crear un nuevo registro CNAME y proporcionar un alias de subdominio que incluya hello **cdnverify** subdominio. Por ejemplo, será el subdominio de Hola que especifique en formato de hello **cdnverify.www** o **cdnverify.cdn**. A continuación, proporcione el nombre de host de hello, que es el punto de conexión, en formato de hello **cdnverify.&lt; EndpointName >. azureedge.net**. La asignación de DNS debe tener el siguiente aspecto:`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Devolver toohello **agregar un dominio personalizado** hoja y escriba su dominio personalizado, incluido el subdominio de hello, en el cuadro de diálogo de Hola. Por ejemplo, escriba el nombre de dominio de hello en formato de hello `www.contoso.com` o `cdn.contoso.com`. Tenga en cuenta que en este paso, no es necesario subdominio de hello toopreface con **cdnverify**.  
   
    Azure comprobará que existe el registro CNAME de Hola Hola cdnverify nombre de dominio que ha escrito.
9. En este momento, Azure ha comprobado su dominio personalizado, pero el dominio de traffic tooyour no está aún tooyour enrutado extremo de red CDN. Después de esperar lo suficientemente largo toopropagate de configuración de dominio personalizado de hello tooallow toohello CDN arista nodos (90 minutos **CDN de Azure de Verizon**, 1 a 2 minutos para **Azure CDN de Akamai**), devuelven tooyour DNS sitio web del registrador y crear otro registro CNAME que asigna el subdominio tooyour punto de conexión. Por ejemplo, especificar subdominio hello como **www** o **cdn**, y el nombre de host de Hola  **&lt;EndpointName >. azureedge.net**. Con este paso, el registro de hello de su dominio personalizado está completando.
10. Por último, puede eliminar el registro CNAME de hello creada con **cdnverify**, tal y como ocurría solo como un paso intermedio.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Compruebe que el punto de conexión hace referencia a ese subdominio personalizado de Hola
* Después de haber completado el registro de hello de su dominio personalizado, puede tener acceso a contenido que se almacena en caché en el punto de conexión con el dominio personalizado de Hola.
  En primer lugar, asegúrese de que tiene contenido público que se almacena en caché en el punto de conexión de Hola. Por ejemplo, si el punto de conexión está asociado a una cuenta de almacenamiento, Hola CDN almacena en caché contenido en contenedores públicos de blobs. dominio personalizado de tootest hello, asegúrese de que el contenedor esté configurado el acceso público de tooallow y que contenga al menos un blob.
* En el explorador, navegue toohello dirección del blob de hello con hello de dominio personalizado. Por ejemplo, si el dominio personalizado está `cdn.contoso.com`, blob almacenados en caché de hello URL tooa será similar toohello después de la dirección URL: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Otras referencias
[¿Cómo tooEnable Hola red de entrega de contenido (CDN) de Azure](cdn-create-new-endpoint.md)  

