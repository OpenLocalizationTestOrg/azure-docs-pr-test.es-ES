---
title: aaa "Habilitar HTTPS en un dominio personalizado de CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable HTTPS en el punto de conexión de red CDN de Azure con un dominio personalizado."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Habilitación de HTTPS en un dominio personalizado de la red CDN de Azure

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Compatibilidad con HTTPS para dominios personalizados de CDN de Azure permite toodeliver contenido seguro a través de SSL con su propia seguridad de dominio nombre tooimprove Hola de datos mientras están en tránsito. Hola tooenable de flujo de trabajo de extremo a extremo HTTPS para su dominio personalizado se simplifica mediante la habilitación de un solo clic, la administración de certificados completa y todo sin ningún coste adicional.

Es privacidad de hello tooensure críticos y la integridad de los datos de todos los datos confidenciales de las aplicaciones web mientras están en tránsito. Utilizando el protocolo HTTPS se asegura de que la información confidencial se cifra cuando se envía a través de Hola Hola internet. Proporciona confianza y autenticación, y protege las aplicaciones web de posibles ataques. Actualmente, la red CDN de Azure admite HTTPS en un punto de conexión de la red CDN. Por ejemplo, si crea un punto de conexión de la red CDN desde la propia red CDN de Azure (p.ej., https://contoso.azureedge.net), HTTPS se habilita de manera predeterminada. Ahora, con HTTPS de dominio personalizado, también se puede habilitar la entrega segura para un dominio personalizado (p. ej., https://www.contoso.com). 

Algunos de los atributos de clave de Hola de característica HTTPS son:

- Sin costo adicional: la adquisición o renovación de certificados no tiene costos y el tráfico HTTPS no supone un costo adicional. Solo paga por GB de salida de la red CDN Hola.

- Habilitación simple: haga clic en uno de aprovisionamiento está disponible en hello [portal de Azure](https://portal.azure.com). También puede utilizar la API de REST u otra característica de Hola de tooenable de herramientas de desarrollador.

- Administración de certificados completa: toda la adquisición y administración de certificados se controla de manera automática. Los certificados se aprovisionan automáticamente y renuevan tooexpiration anterior. Esto quita completamente los riesgos de Hola de interrupción del servicio como resultado de un certificado que caduca.

>[!NOTE] 
>Tooenabling anterior la compatibilidad con HTTPS, debe ya se ha establecido un [dominio personalizado de CDN de Azure](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>Paso 1: Habilitar la característica de Hola 

1. Hola [portal de Azure](https://portal.azure.com), examinar el perfil de CDN estándar o premium Verizon de tooyour.

2. Hola lista de puntos de conexión, haga clic en punto de conexión de Hola que contiene el dominio personalizado.

3. Haga clic en el dominio personalizado de hello para el que desea tooenable HTTPS.

    ![Hoja de puntos de conexión](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Haga clic en **en** tooenable HTTPS y guardar el cambio de Hola.

    ![Cuadro de diálogo Personalizar HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Paso 2: Validación de dominio

>[!IMPORTANT] 
>Para que HTTPS pueda activarse en un dominio personalizado, antes es preciso completar la validación del dominio. Tiene 6 business días tooapprove Hola dominio. Si no se realiza la aprobación en 6 días laborables, la solicitud se cancelará.  

Después de habilitar HTTPS en su dominio personalizado, el proveedor de certificados HTTPS DigiCert validará propiedad del dominio poniéndose en contacto persona registrada hello para el dominio, en función de la información del titular WHOIS, a través de correo electrónico (de forma predeterminada) o un teléfono. DigiCert también enviará toohello de correo electrónico de comprobación de hello debajo de direcciones. Si la información del inscrito de WHOIS es privada, asegúrese de que puede realizar las aprobaciones directamente desde una de estas direcciones.

>admin@<su-nombre-de-dominio.com> administrator@<su-nombre-de-dominio.com>  
>webmaster@<su-nombre-de-dominio.com>  
>hostmaster@<su-nombre-de-dominio.com>  
>postmaster@<su-nombre-de-dominio.com>


Al recibir correo electrónico de hello, tienes dos opciones de comprobación:

1. Puede aprobar todas las futuras pedidos realizados a través de hello misma cuenta para hello dominio raíz del mismo, por ejemplo, consoto.com. Éste es un enfoque recomendado si tiene previsto dominios personalizados adicionales de tooadd en futuras para Hola Hola dominio raíz del mismo.
 
2. Solo puede aprobar el nombre de host específico de hello usado en esta solicitud. Para las solicitudes posteriores se requerirá una aprobación adicional.

    Correo electrónico de ejemplo:
    
    ![Cuadro de diálogo Personalizar HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

Tras la aprobación, DigiCert agregará el certificado de SAN de toohello de nombre de dominio personalizado. certificado de Hello será válida durante un año y se auto renovará antes de haya expirado.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>Paso 3: Esperar a la propagación de hello, a continuación, empezar a usar la característica

Después de valida el nombre de dominio de hello ocupará too6-8 horas para hello dominio personalizado HTTPS característica toobe active. Una vez completado el proceso de hello, estado de "HTTPS personalizado" Hola Hola portal de Azure se establecerá demasiado "Enabled". HTTPS con el dominio personalizado ya está listo para su uso.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

1. *¿Quién es el proveedor de certificados de Hola y se utiliza el tipo de certificado?*

    Se usa el certificado SAN (nombres alternativos de firmantes) proporcionado por DigiCert. Un certificado SAN puede proteger varios nombres de dominio completo con un solo certificado.

2. *¿Puedo usar mi certificado dedicado?*
    
    No actualmente, pero su plan de hello en.

3. *¿Qué ocurre si no recibo correo electrónico de comprobación de dominio Hola de DigiCert?*

    Si no recibe un correo electrónico en 24 horas, póngase en contacto con Microsoft.

4. *¿Son menos seguros los certificados SAN que los certificados dedicados?*
    
    Un certificado SAN sigue Hola mismos estándares de cifrado y seguridad, como un certificado dedicado. Todos los certificados SSL emitidos utilizan SHA-256 para mejorar la seguridad del servidor.

5. *¿Puedo usar HTTPS de dominio personalizado con la red CDN de Azure de Akamai?*

    Actualmente, esta característica solo está disponible en la red CDN de Azure de Verizon. Estamos trabajando en la compatibilidad con esta característica con Azure CDN de Akamai en los próximos meses de Hola.


## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo tooset seguridad un [dominio personalizado en el punto de conexión de red CDN de Azure](./cdn-map-content-to-custom-domain.md)


