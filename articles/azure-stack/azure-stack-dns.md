---
title: aaaDNS en la pila de Azure | Documentos de Microsoft
description: DNS en Azure Stack
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/27/2017
ms.author: victorh
ms.openlocfilehash: 8620178833ac29e9653cce332b7c5d89bbdea0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dns-in-azure-stack"></a>DNS en Azure Stack
Pila de Azure incluye Hola siguientes características DNS:
* Compatibilidad con la resolución de nombres de host DNS
* Crear y administrar registros y zonas DNS con API

## <a name="support-for-dns-hostname-resolution"></a>Compatibilidad con la resolución de nombres de host DNS
Puede especificar una etiqueta de nombre de dominio DNS para un recurso IP pública, que se crea una asignación para *domainnamelabel.location*. cloudapp.azurestack.external toohello la dirección IP en hello Azure pila administra servidores DNS.  

Por ejemplo, si crea un recurso IP público con **contoso** como una etiqueta de nombre de dominio en la ubicación de la pila de Azure Local hello, nombre de dominio completo (FQDN) de Hola **contoso.local.cloudapp.azurestack.external** resuelve la dirección IP pública de toohello del recurso de Hola. Puede usar este toocreate FQDN un registro CNAME que señala la dirección IP pública toohello en pila de Azure de dominio personalizado.

> [!IMPORTANT]
> Cada etiqueta de nombre de dominio que se cree debe ser única dentro de su ubicación de Azure Stack.

Si crea la dirección IP pública hello mediante el portal de hello, parece similar al siguiente:

![Creación de una dirección IP pública](media/azure-stack-whats-new-dns/image01.png)

Esta configuración es útil si desea tooassociate una dirección IP pública a un recurso con equilibrio de carga. Por ejemplo, podría tener una solicitud de procesamiento de equilibrador de carga desde una aplicación web. Detrás de la carga de hello equilibrador es un sitio web ubicado en una o más máquinas virtuales. Ahora puede tener acceso a sitios web con equilibrio de carga de hello mediante un nombre DNS, en lugar de una dirección IP.

## <a name="create-and-manage-dns-zones-and-records-using-api"></a>Crear y administrar registros y zonas DNS con API
Puede crear y administrar registros y zonas DNS en Azure Stack.  

Azure Stack proporciona un servicio DNS como Azure mediante API que son coherentes con las API de DNS de Azure.  Mediante el hospedaje de los dominios de DNS de la pila de Azure, puede administrar los registros DNS con hello mismas credenciales, API, herramientas, facturación y soporte a medida que los servicios de Azure. 

Por razones obvias, la infraestructura de DNS de la pila de Azure de hello es más compacto que el de Azure. Por lo tanto, hello ámbito, escalabilidad y rendimiento dependen de escala de Hola de implementación de la pila de Azure de Hola y entorno de hello en los que se implementó.  Por lo tanto, por ejemplo, rendimiento, disponibilidad, distribución global y alta disponibilidad (HA) puede variar de toodeployment de implementación.

## <a name="comparison-with-azure-dns"></a>Comparación con el DNS de Azure
DNS en la pila de Azure es tooDNS similar en Azure, con dos excepciones principales:
* **No admite registros AAAA**.

    Azure Stack NO admite registros AAAA porque no es compatible con las direcciones IPv6.  Se trata de una diferencia clave entre el DNS de Azure y de Azure Stack.
* **No es multiinquilino**.

    A diferencia de Azure, Hola servicio DNS en la pila de Azure no es multiempresa. Por lo que no se puede crear cada inquilino Hola misma zona DNS. Solo Hola primera suscripción que intente zona de hello toocreate se realiza correctamente y producirá un error en las solicitudes posteriores.  Se trata de un problema conocido, y una diferencia clave entre el DNS de Azure y de Azure Stack. El problema se solucionará en una futura versión.

Además, hay algunas pequeñas diferencias en cómo el DNS de Azure Stack implementa las etiquetas, los metadatos, las etiquetas ETag y los límites.

Hola siguiente información aplica específicamente tooAzure DNS de la pila y varía ligeramente de DNS de Azure. toolearn más información acerca de DNS de Azure, consulte [zonas y registros DNS](../dns/dns-zones-records.md) en el sitio de documentación de Microsoft Azure Hola.

### <a name="tags-metadata-and-etags"></a>Etiquetas, metadatos y etiquetas de identidad

**Etiquetas**

El DNS de Azure Stack admite el uso de etiquetas de Azure Resource Manager en recursos de zona DNS. No admite etiquetas en conjuntos de registros de DNS, aunque, como alternativa, se admiten "metadatos" en estos tipos de conjuntos, como se explica a continuación.

**Metadata**

Como una alternativa toorecord conjunto de etiquetas, DNS de la pila de Azure admite la anotación de conjuntos de registros mediante 'metadatos de '. Tootags similar, metadatos permiten a tooassociate pares nombre / valor con cada conjunto de registros. Por ejemplo, esto puede ser útil toorecord propósito de Hola de cada conjunto de registros. A diferencia de las etiquetas, los metadatos no pueden ser tooprovide usa una vista filtrada de la factura de Azure y no se puede especificar en una directiva de Azure Resource Manager.

**Etiquetas de identidad**

Suponga que dos personas o dos procesos intente toomodify un registro DNS en hello mismo tiempo. ¿Cuál gana? ¿Y ganador Hola sabe que han sobrescrito cambios creados por otra persona?

DNS de pila de Azure usa Etags toohandle cambios simultáneos toohello mismo recurso de forma segura. Las etiquetas de entidad (ETag) son independientes de las "etiquetas" de Azure Resource Manager. Cada recurso DNS (zona o conjunto de registros) tiene un valor de Etag asociado a él. Siempre que se recupera un recurso, también se recupera su Etag. Al actualizar un recurso, puede elegir volver toopass Hola Etag para que Azure pila DNS pueda comprobar que Hola Etag en hello coincide con el servidor. Puesto que cada recurso de tooa actualización da como resultado Hola Etag que se va a volver a generar, un error de coincidencia de Etag indica que se ha producido un cambio simultáneo. ETags también puede utilizarse al crear un nuevo tooensure de recursos que ya no existe el recurso de Hola.

De manera predeterminada, Azure pila DNS PowerShell usa Etags tooblock cambios simultáneos toozones y conjuntos de registros. Hola opcional *-sobrescribir* conmutador puede ser utilizados toosuppress Etag comprobaciones, en cuyo caso cualquier simultáneas se sobrescriben los cambios que se han producido.

En el nivel de Hola de hello API de REST de DNS de pila de Azure, Etags se especifican mediante encabezados HTTP. Su comportamiento se expresa en hello en la tabla siguiente:

| Encabezado | Comportamiento|
|--------|---------|
| Ninguna   | PUT always succeeds (no Etag checks)|
| If-match| PUT only succeeds if resource exists and Etag matches|
| If-match *| PUT only succeeds if resource exists|
| If-none-match *| PUT only succeeds if resource does not exist|

### <a name="limits"></a>límites

Hola siguiendo los límites predeterminados se aplica cuando se usa DNS de la pila de Azure:

| Recurso| Límite predeterminado|
|---------|--------------|
| Zonas por suscripción| 100|
| Conjuntos de registros por zona| 5000|
| Registros por conjunto de registros| 20 ||

## <a name="next-steps"></a>Pasos siguientes
[Presentación de iDNS para Azure Stack](azure-stack-understanding-dns.md)
