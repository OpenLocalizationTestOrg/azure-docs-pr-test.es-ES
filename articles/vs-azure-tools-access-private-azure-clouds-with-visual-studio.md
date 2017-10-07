---
title: nubes privadas de Azure aaaAccessing con Visual Studio | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooaccess privada recursos de la nube con Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="275dd-103">Acceso a nubes privadas de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="275dd-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="275dd-104">De forma predeterminada, Visual Studio admite extremos REST de nube pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="275dd-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="275dd-105">En este tema, aprenderá cómo toouse la nube privada del certificado tooaccess - e interactúan: hello en la nube privada desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="275dd-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="275dd-106">tooaccess privada de Azure en la nube en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="275dd-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="275dd-107">Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885) de nube privada de hello, descargue el archivo de configuración de publicación o póngase en contacto con el administrador para un archivo de configuración de la publicación.</span><span class="sxs-lookup"><span data-stu-id="275dd-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="275dd-108">En la versión pública de Hola de Azure, Hola toodownload de vínculo es [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="275dd-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="275dd-109">(archivo descargado Hola debe tener una extensión de `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="275dd-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="275dd-110">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="275dd-110">Open Visual Studio</span></span>

1. <span data-ttu-id="275dd-111">En **Explorador de servidores**, contextual hello **Azure** nodo y, en el menú contextual de hello, seleccione **administrar y filtrar suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="275dd-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Comando Administrar suscripciones](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="275dd-113">Hola **administrar suscripciones de Microsoft Azure** cuadro de diálogo, seleccione hello **certificados** pestaña y, a continuación, seleccione **importación**.</span><span class="sxs-lookup"><span data-stu-id="275dd-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importación de certificados de Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="275dd-115">Hola **Importar suscripciones de Microsoft Azure** cuadro de diálogo, seleccione **examinar**.</span><span class="sxs-lookup"><span data-stu-id="275dd-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Botón del cuadro de diálogo de importación suscripciones de Microsoft Azure Hola examinar](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="275dd-117">Hola **abiertos** cuadro de diálogo, examinar toohello directorio donde se Hola guardado archivo publish-settings, seleccione Hola archivo y, a continuación, seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="275dd-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Seleccione el archivo de configuración de publicación de hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="275dd-119">Cuando se devuelve toohello **Importar suscripciones de Microsoft Azure** cuadro de diálogo, seleccione **importación**.</span><span class="sxs-lookup"><span data-stu-id="275dd-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Importar archivo de configuración de publicación de hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="275dd-121">certificados de Hola se importan desde el archivo de configuración de publicación de hello en Visual Studio y ahora puede interactuar con los recursos de nube privada.</span><span class="sxs-lookup"><span data-stu-id="275dd-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="275dd-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="275dd-122">Next steps</span></span>
- [<span data-ttu-id="275dd-123">Publicación tooan servicio de nube de Azure desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="275dd-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="275dd-124">[Descarga e importación de la configuración de publicación y la información de suscripción](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="275dd-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>