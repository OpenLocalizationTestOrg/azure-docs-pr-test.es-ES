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
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="db629-103">Carga de un certificado de administración de Azure Management API</span><span class="sxs-lookup"><span data-stu-id="db629-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="db629-104">Certificados de administración permiten tooauthenticate con el modelo de implementación clásica de hello proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="db629-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="db629-105">Muchos programas y herramientas (como Visual Studio o hello Azure SDK) utilizan estos configuración tooautomate de certificados y la implementación de varios servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="db629-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="db629-106">Por lo tanto, tenga cuidado.</span><span class="sxs-lookup"><span data-stu-id="db629-106">Be careful!</span></span> <span data-ttu-id="db629-107">Estos tipos de certificados permiten a ningún usuario que se autentica con su suscripción de hello toomanage que están asociados.</span><span class="sxs-lookup"><span data-stu-id="db629-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="db629-108">Si deseara más información acerca de los certificados de Azure (incluido cómo crear un certificado autofirmado), consulte [Introducción a los certificados para Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="db629-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="db629-109">También puede usar [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate código de cliente para fines de automatización.</span><span class="sxs-lookup"><span data-stu-id="db629-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="db629-110">Carga de un certificado de administración</span><span class="sxs-lookup"><span data-stu-id="db629-110">Upload a management certificate</span></span>
<span data-ttu-id="db629-111">Una vez que tiene un certificado de administración creado (archivo .cer con sólo clave pública de Hola) se puede cargar en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="db629-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="db629-112">Cuando certificado Hola está disponible en el portal de hello, cualquier persona con un certificado correspondiente (clave privada) puede conectarse a través de recursos de Hola de hello API de administración y acceso para la suscripción de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="db629-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="db629-113">Inicie sesión en toohello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db629-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="db629-114">Haga clic en **más servicios** en la lista de servicio de Azure de hello inferior, a continuación, seleccione **suscripciones** en hello _General_ grupo de servicio.</span><span class="sxs-lookup"><span data-stu-id="db629-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Menú Suscripción](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="db629-116">Asegúrese de que tooselect Hola que desea tooassociate con certificado Hola de suscripción correcta.</span><span class="sxs-lookup"><span data-stu-id="db629-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="db629-117">Después de haber seleccionado la suscripción correcta de hello, presione **certificados de administración** en hello _configuración_ grupo.</span><span class="sxs-lookup"><span data-stu-id="db629-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Settings](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="db629-119">Hola presione **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="db629-119">Press hello **Upload** button.</span></span>

    ![Cargar la página Certificados](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="db629-121">Rellene la información del cuadro de diálogo de hello y presione **cargar**.</span><span class="sxs-lookup"><span data-stu-id="db629-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Settings](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="db629-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db629-123">Next steps</span></span>
<span data-ttu-id="db629-124">Ahora que tiene un certificado de administración asociado a una suscripción, puede (después de haber instalado Hola coincidencia certificado localmente) mediante programación conectarse toohello [API de REST de modelo de implementación clásica](https://msdn.microsoft.com/library/azure/mt420159.aspx) y automatizar Hola distintos recursos de Azure que también están asociados a esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="db629-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
