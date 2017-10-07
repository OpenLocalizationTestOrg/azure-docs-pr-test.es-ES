---
title: "blobs en tooaccess aaaUsing Hola CDN de Azure con dominios personalizados a través de HTTPS"
description: "Obtenga información acerca de cómo los blobs toointegrate Hola CDN de Azure con tooaccess de almacenamiento de blobs con dominios personalizados a través de HTTPS"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: f6cee36ca5495983545f2f6a8ff140677cf6914b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>Uso de blobs de tooaccess de Azure CDN Hola con dominios personalizados a través de HTTPS

Ahora, Azure Content Delivery Network (CDN) admite HTTPS para los nombres de dominio personalizados.
Puede aprovechar esta blobs de almacenamiento de tooaccess característica mediante su dominio personalizado a través de HTTPS. toodo por lo tanto, primero deberá tooenable CDN de Azure en blob extremo y mapa Hola CDN tooa nombre de dominio personalizado. Una vez realizadas estas acciones, habilitar HTTPS para su dominio personalizado se ha simplificado mediante la habilitación de un solo clic, la administración de certificados completa y todos los datos con ningún precios de coste adicional toonormal CDN.

Esta capacidad es importante porque permite privacidad hello tooprotect y la integridad de los datos de los datos de aplicación web confidenciales mientras están en tránsito. El uso de tráfico de tooserve de protocolo Hola SSL a través de HTTPS garantiza que los datos se cifran cuando se envía a través de hello internet. HTTPS proporciona confianza y autenticación, y protege las aplicaciones web de posibles ataques.

> [!NOTE]
> Además tooproviding compatibilidad con SSL para los nombres de dominio personalizado, Azure CDN Hola puede ayudarle a escalar el contenido de gran ancho de banda de aplicación toodeliver alrededor de Hola a todos.
> más información, consulte toolearn [información general sobre Azure CDN Hola](../../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Inicio rápido

Se trata de hello pasos necesarios tooenable HTTPS para el extremo de almacenamiento de blobs personalizado:

1.  [Integración de una cuenta de una instancia de Azure Storage con la red CDN de Azure](../../cdn/cdn-create-a-storage-account-with-cdn.md).
    Este artículo le guiará por la creación de una cuenta de almacenamiento en hello Portal de Azure si aún no lo ha hecho.
2.  [Dominio personalizado de tooa contenido de CDN de Azure de mapa](../../cdn/cdn-map-content-to-custom-domain.md).
3.  [Habilitación de HTTPS en un dominio personalizado de la red CDN de Azure](../../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>Las firmas de acceso compartido

Si el extremo de almacenamiento de blobs es configurado toodisallow acceso de lectura anónimo, deberá tooprovide un [firma de acceso compartido (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) token en cada solicitud que realice tooyour de dominio personalizado. De forma predeterminada, los puntos de conexión de Blob Storage no permiten el acceso de lectura anónimo. Vea [Administración del acceso de lectura anónimo a contenedores y blobs](storage-manage-access-to-resources.md) para obtener más información sobre las firmas de acceso compartidas.

Red CDN de Azure no respeta cualquier token SAS toohello agregada de restricciones. Por ejemplo, todos los tokens de SAS tienen una fecha de expiración. Esto significa que el contenido todavía puede tener acceso mediante una SAS que expiró hasta que el contenido se purga de nodos de borde CDN Hola. Puede controlar cuánto tiempo los datos en caché en CDN Hola por establecer un encabezado de respuesta de caché de Hola. Vea [Administración de la expiración de Azure Storage Blob en la red CDN de Azure](../../cdn/cdn-manage-expiration-of-blob-content.md) para obtener instrucciones.

Si crea varias direcciones URL de SAS para hello mismo extremo de blob, se recomienda activar el almacenamiento en caché de cadena de consulta para la red CDN de Azure. Se trata de tooensure que cada dirección URL se trata como una entidad única. Vea [Control del comportamiento del almacenamiento en caché de la red CDN de Azure con cadenas de consulta](../../cdn/cdn-query-string.md) para obtener más información.

## <a name="http-toohttps-redirection"></a>Redirección de HTTP tooHTTPS

Puede elegir tooredirect HTTP tráfico tooHTTPS. Requiere el uso de la oferta de premium de Azure CDN Hola desde Verizon. Necesita demasiado[comportamiento de invalidación HTTP mediante el motor de reglas de red CDN de Azure](../../cdn/cdn-rules-engine.md) con la siguiente regla:

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Nombre de punto de conexión de Cdn" hace referencia nombre toohello que ha configurado para el punto de conexión. Puede seleccionar este valor de lista desplegable de Hola. "Ruta de origen" hace referencia a la ruta de acceso de hello dentro de su cuenta de almacenamiento de origen en el que reside el contenido estático.
Si está hospedando todo el contenido estático en un único contenedor, reemplace "ruta de origen" por nombre de Hola de ese contenedor.

Para obtener un análisis más profundo en reglas, vea hello [características del motor de reglas de red CDN de Azure](../../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Precios y facturación

Cuando tiene acceso a blobs a través de una red CDN de Azure, usted paga [los precios de almacenamiento de blobs](https://azure.microsoft.com/pricing/details/storage/blobs/) para el tráfico entre nodos de hello borde y el origen de hello (almacenamiento de blobs), y [precios CDN](https://azure.microsoft.com/pricing/details/cdn/) para los datos que se obtiene acceso desde los nodos de hello borde.

Por ejemplo, supongamos que tiene una cuenta de almacenamiento en el oeste de EE. UU. a la que se obtiene acceso mediante una red CDN de Azure. Si algún elemento de hello del Reino Unido intenta tooaccess uno Hola blobs de esa cuenta de almacenamiento a través de la red CDN Hola, Azure comprueba en primer lugar el nodo del borde de hello es más cercano a saludos del Reino Unido para ese blob. Si encuentra, se tiene acceso a esa copia de blob de Hola y utilizarán CDN sobre los precios, ya que se tiene acceso en la red CDN Hola. Si no se encuentra, Azure copiará Hola blob toohello nodo del borde, lo que hará en salida y cargos de transacción como Hola especificado en precios del almacenamiento de blobs y, a continuación, obtener acceso a archivo hello en el nodo del borde de hello, lo que dará lugar en la facturación de CDN.

Cuando se examinan hello [CDN página de precios](https://azure.microsoft.com/pricing/details/cdn/), tenga en cuenta que la compatibilidad con HTTPS para los nombres de dominio personalizado solo está disponible para la red CDN de Azure de productos de Verizon (ediciones Standard y Premium).

## <a name="next-steps"></a>Pasos siguientes

[Configurar un nombre de dominio personalizado para el punto de conexión de Blob Storage](storage-custom-domain-name.md)
