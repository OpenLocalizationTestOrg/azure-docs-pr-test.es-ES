---
title: aaaConfigure un nombre de dominio personalizado en servicios en la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooexpose su toohello Azure de datos de aplicaciones o internet en un dominio personalizado al establecer la configuración de DNS.  Estos ejemplos utilizan Hola portal de Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configuración de un nombre de dominio personalizado para un servicio en la nube de Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-custom-domain-name-portal.md)
> * [Portal de Azure clásico](cloud-services-custom-domain-name.md)
> 
> 

Cuando se crea un servicio de nube, Azure asigna tooa subdominio de **cloudapp.net**. Por ejemplo, si el servicio de nube se denomina "contoso", los usuarios realizarán ser capaz de tooaccess la aplicación en una dirección URL como http://contoso.cloudapp.net. Azure también asigna una dirección IP virtual.

Sin embargo, también puede exponer su aplicación en su propio nombre de dominio, como **contoso.com**. Este artículo se explica cómo tooreserve o configurar un nombre de dominio personalizado para los roles de web de servicio en la nube.

¿Ya entiende qué son los registros CNAME y D? [Salto más allá de la explicación de hello](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> procedimientos de Hello en esta tarea aplican tooAzure servicios en la nube. Para Servicios de aplicaciones, consulte [este artículo](../app-service-web/web-sites-custom-domain-name.md). Para las cuentas de almacenamiento, consulte [este artículo](../storage/blobs/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Póngase en marcha con mayor rapidez: usar hello Azure nueva [interactiva tutorial](http://support.microsoft.com/kb/2990804)!  Con este tutorial, asociar un nombre de dominio personalizado y proteger las comunicaciones (SSL) con los servicios en la nube de Azure o Sitios web Azure es facilísimo.
> 
> 

## <a name="understand-cname-and-a-records"></a>Descripción de los registros D y CNAME
CNAME (o registros de alias) y registros a ambos permiten tooassociate un nombre de dominio con un servidor específico (o servicio en este caso,) sin embargo funcionan de forma distinta. También hay algunas consideraciones específicas al utilizar registros con servicios en la nube de Azure que debería tener en cuenta antes de decidir qué toouse.

### <a name="cname-or-alias-record"></a>Registro de CNAME o Alias
Un registro CNAME asigna un *específico* dominio, como **contoso.com** o **www.contoso.com**, nombre de dominio canónico tooa. En este caso, el nombre de dominio canónico hello es hello **.cloudapp [myapp] .net** nombre de dominio de Azure hospeda la aplicación. Una vez creado, Hola CNAME crea un alias para hello **.cloudapp [myapp] .net**. Hola entrada CNAME resolverá toohello dirección IP de su **.cloudapp [myapp] .net** servicio automáticamente, por lo que si se cambia la dirección IP de hello del servicio de nube de hello, no tiene tootake ninguna acción.

> [!NOTE]
> Algunos registradores de dominios sólo permiten subdominios toomap cuando se usa un registro CNAME, por ejemplo, www.contoso.com y no los nombres de raíz, por ejemplo, contoso.com. Para obtener más información sobre los registros CNAME, vea documentación de hello proporcionada por el registrador, [Hola entrada de Wikipedia en el registro CNAME](http://en.wikipedia.org/wiki/CNAME_record), o hello [nombres de dominio de IETF: implementación y especificación](http://tools.ietf.org/html/rfc1035) documento.
> 
> 

### <a name="a-record"></a>Registro D
Un *A* registro asigna un dominio, como **contoso.com** o **www.contoso.com**, *o un dominio comodín* como  **\*. contoso.com**, dirección IP de tooan. En caso de hello de un servicio de nube de Azure, Hola dirección IP virtual del servicio de Hola. Por lo que la ventaja principal de Hola de un registro a través de un registro CNAME es que puede tener una entrada que use un carácter comodín, como \* **. contoso.com**, que deben controlar las solicitudes de varios subdominios como  **Mail.contoso.com**, **login.contoso.com**, o **www.contso.com**.

> [!NOTE]
> Puesto que está asignado a un registro a una dirección IP estática tooa, no puede resolver automáticamente la dirección IP de toohello de cambios de servicio en la nube. Hola asignar dirección IP utilizada por el servicio en la nube es Hola primera vez que implemente tooan de ranura vacía (producción o ensayo.) Si se elimina la implementación de hello en la ranura de hello, se libera la dirección IP de hello Azure y cualquier ranura de toohello futuras implementaciones puede recibir una nueva dirección IP.
> 
> Por comodidad, dirección IP de Hola de una ranura de implementación determinada (producción o ensayo) se conserva cuando el intercambio entre las implementaciones de producción y ensayo o de realizar una actualización en contexto de una implementación existente. Para obtener más información acerca de cómo realizar estas acciones, consulte [toomanage cómo los servicios de nube](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Incorporación de un CNAME al dominio personalizado
toocreate un registro CNAME, debe agregar una nueva entrada en la tabla DNS de Hola para su dominio personalizado mediante las herramientas de hello proporcionadas por el registrador. Cada registrador tiene un método similar pero ligeramente distinto para especificar un registro CNAME, pero Hola Hola conceptos son iguales.

1. Utilice uno de estos Hola de métodos toofind **. cloudapp.net** nombre de dominio asignado tooyour servicio en la nube.
   
   * Inicio de sesión toohello [portal de Azure], seleccione su servicio en la nube, mire Hola **Essentials** sección y, a continuación, busque Hola **dirección URL del sitio** entrada.
     
       ![sección de vista rápida muestra la URL del sitio de Hola][csurl]
     
       **O bien**
   * Instalar y configurar [Azure Powershell](/powershell/azure/overview), y, a continuación, use Hola siguiente comando:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Guarde el nombre de dominio de hello utilizado en la dirección URL de hello devuelto por cualquiera de los métodos, ya que será necesario cuando se crea un registro CNAME.
2. Inicie sesión en el sitio Web del registrador DNS de tooyour e ir a página toohello para la administración de DNS. Busque los vínculos correspondientes o áreas del sitio de hello etiquetada como **nombre de dominio**, **DNS**, o **gestión de nombre de servidor**.
3. Ahora busque el lugar en el que puede seleccionar o especificar los registros CNAME. Puede que tenga el registro de hello de tooselect escriba en una lista desplegable, o visite tooan página de opciones avanzadas. También debe buscar palabras hello **CNAME**, **Alias**, o **subdominios**.
4. También debe proporcionar Hola dominio o subdominio alias para hello CNAME, como **www** si desea toocreate un alias para **www.customdomain.com**. Si desea toocreate un alias para el dominio raíz de hello, que puede aparecer como hello '**@**' símbolo en las herramientas DNS de su registrador.
5. A continuación, debe proporcionar un nombre de host canónico que, en este caso, es el dominio **cloudapp.net** de su aplicación.

Por ejemplo, hello siguiendo el registro CNAME reenvía todo el tráfico de **www.contoso.com** demasiado**contoso.cloudapp.net**, nombre de dominio personalizado de saludo de la aplicación implementada:

| Alias/Nombre de host/Subdominio | Dominio canónico |
| --- | --- |
| www |contoso.cloudapp.net |

> [!NOTE]
> Un visitante de **www.contoso.com** nunca verá host true de hello (contoso.cloudapp.net), por lo que Hola proceso de reenvío es el usuario final de toothe invisible.
> 
> Hello ejemplo anterior solo aplica tootraffic en hello **www** subdominio. Puesto que no puede usar caracteres comodín con registros CNAME, debe crear un CNAME para cada dominio/subdominio. Si desea que el tráfico toodirect de subdominios, como *. contoso.com, tooyour cloudapp.net dirección, puede configurar un **redireccionamiento de direcciones URL** o **dirección URL al día** entrada en la configuración de DNS, o crear un registro.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Agregar un registro D para el dominio personalizado
toocreate un registro, primero debe buscar la dirección IP virtual de Hola de servicio en la nube. A continuación, agregar una nueva entrada en tabla DNS de hello para el dominio personalizado mediante herramientas de hello proporcionadas por el registrador. Cada registrador tiene un método similar pero ligeramente distinto para especificar un registro, pero Hola Hola conceptos son iguales.

1. Utilice uno de hello siguiente dirección IP de métodos tooget Hola de servicio en la nube.
   
   * Toohello de inicio de sesión [portal de Azure], seleccione su servicio en la nube, mire hello **Essentials** sección y, a continuación, busque hello **direcciones IP públicas** entrada.
     
       ![sección de vista rápida muestra hello VIP][vip]
     
       **O bien**
   * Instalar y configurar [Azure Powershell](/powershell/azure/overview), y, a continuación, use Hola siguiente comando:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Guarde la dirección IP de hello, ya que será necesario cuando se crea un registro.
2. Inicie sesión en el sitio Web del registrador DNS de tooyour e ir a página toohello para la administración de DNS. Busque los vínculos correspondientes o áreas del sitio de hello etiquetada como **nombre de dominio**, **DNS**, o **gestión de nombre de servidor**.
3. Ahora busque el lugar en el que puede seleccionar o especificar los registros D. Puede que tenga el registro de hello de tooselect escriba en una lista desplegable, o visite tooan página de opciones avanzadas.
4. Seleccione o escriba el dominio de Hola o subdominio que utilizará este registro. Por ejemplo, seleccione **www** si desea toocreate un alias para **www.customdomain.com**. Si desea toocreate una entrada de comodín para todos los subdominios, escriba ' ***'. De esta forma, se incluirán todos los subdominios como **mail.customdomain.com**, **login.customdomain.com** y **www.customdomain.com**.
   
    Si desea toocreate un registro para el dominio raíz de hello, que puede aparecer como hello '**@**' símbolo en las herramientas DNS de su registrador.
5. Escriba la dirección IP de Hola de servicio en la nube en hello proporcionada el campo. Esto asocia las entradas del dominio Hola utilizadas en registro Hola con la dirección IP de saludo de la implementación del servicio de nube.

Por ejemplo, después de un registro de hello reenvía todo el tráfico de **contoso.com** demasiado**137.135.70.239**, Hola dirección IP de la aplicación implementada:

| Nombre de host/Subdominio | Dirección IP |
| --- | --- |
| @ |137.135.70.239 |

Este ejemplo muestra cómo crear un registro para el dominio raíz de Hola. Si desea toocreate una toocover de entrada de comodín todos los subdominios, escribiría ' ***' como subdominio Hola.

> [!WARNING]
> Las direcciones IP en Azure son dinámicas de forma predeterminada. Probablemente le interesará toouse una [las direcciones IP reservadas](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure que la dirección IP no cambia.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Cómo tooManage los servicios de nube](cloud-services-how-to-manage.md)
* [¿Cómo tooMap CDN contenido tooa dominio personalizado](../cdn/cdn-map-content-to-custom-domain.md)
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portal de Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
