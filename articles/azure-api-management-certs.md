---
title: "aaaUpload un certificado de API de administración de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupload athe API de administración de certificados para hello Portal clásico de Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Carga de un certificado de administración de Azure Management API
Certificados de administración permiten tooauthenticate con el modelo de implementación clásica de hello proporcionada por Azure. Muchos programas y herramientas (como Visual Studio o hello Azure SDK) utilizan estos configuración tooautomate de certificados y la implementación de varios servicios de Azure. 

> [!WARNING]
> Por lo tanto, tenga cuidado. Estos tipos de certificados permiten a ningún usuario que se autentica con su suscripción de hello toomanage que están asociados.
>
>

Si deseara más información acerca de los certificados de Azure (incluido cómo crear un certificado autofirmado), consulte [Introducción a los certificados para Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

También puede usar [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate código de cliente para fines de automatización.

## <a name="upload-a-management-certificate"></a>Carga de un certificado de administración
Una vez que tiene un certificado de administración creado (archivo .cer con sólo clave pública de Hola) se puede cargar en el portal de Hola. Cuando certificado Hola está disponible en el portal de hello, cualquier persona con un certificado correspondiente (clave privada) puede conectarse a través de recursos de Hola de hello API de administración y acceso para la suscripción de hello asociado.

1. Inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. Haga clic en **más servicios** en la lista de servicio de Azure de hello inferior, a continuación, seleccione **suscripciones** en hello _General_ grupo de servicio.

    ![Menú Suscripción](./media/azure-api-management-certs/subscriptions_menu.png)

3. Asegúrese de que tooselect Hola que desea tooassociate con certificado Hola de suscripción correcta.     
4. Después de haber seleccionado la suscripción correcta de hello, presione **certificados de administración** en hello _configuración_ grupo.

    ![Settings](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Hola presione **cargar** botón.

    ![Cargar la página Certificados](./media/azure-api-management-certs/certificates_page.png)
6. Rellene la información del cuadro de diálogo de hello y presione **cargar**.

    ![Settings](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene un certificado de administración asociado a una suscripción, puede (después de haber instalado Hola coincidencia certificado localmente) mediante programación conectarse toohello [API de REST de modelo de implementación clásica](https://msdn.microsoft.com/library/azure/mt420159.aspx) y automatizar Hola distintos recursos de Azure que también están asociados a esa suscripción.
