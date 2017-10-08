---
title: aaaCreate un servidor de Analysis Services en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un servidor de Analysis Services de instancia de Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Creación de un servidor de Azure Analysis Services en Azure Portal
Este artículo lo guiará por la creación de un recurso de servidor de Analysis Services en la suscripción de Azure.

## <a name="before-you-begin"></a>Antes de empezar
toocomplete este tutorial rápido, necesita:

* **Suscripción de Azure**: visite [evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate una cuenta.
* **Azure Active Directory**: la suscripción debe estar asociada a un inquilino de Azure Active Directory. Y necesita toobe iniciado sesión tooAzure con una cuenta en que Azure Active Directory. No se admiten cuentas de Microsoft. más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).
* **Grupo de recursos**: use un grupo de recursos que ya tenga o [cree uno nuevo](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> La creación de un servidor puede dar lugar a un nuevo servicio facturable. más información, consulte toolearn [precios de Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate un servidor en el portal de Azure
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).  
2. Haga clic en **+ Nuevo** > **Datos y análisis** > **Analysis Services**.
3. Hola **Analysis Services** hoja, rellene los campos de hello necesario y, a continuación, presione **crear**.
   
    ![Crear un servidor](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Nombre del servidor**: escriba un servidor de nombre único usado tooreference Hola.
   * **Suscripción**: seleccione suscripción Hola facturas de este servidor a.
   * **Grupo de recursos**: estos contenedores están diseñado toohelp administrar una colección de recursos de Azure. más información, consulte toolearn [grupos de recursos](../azure-resource-manager/resource-group-overview.md).
   * **Ubicación**: Hola de hosts de ubicación de centro de datos de Azure de este servidor. Elija una ubicación más cercana a su base de usuarios más grande.
   * **Plan de tarifa**: seleccione un plan de tarifa. Se admiten los modelos tabulares backup too400 GB. más información, consulte toolearn [precios de Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Haga clic en **Crear**.

La creación normalmente tarda menos de un minuto, a menudo solo unos pocos segundos. Si seleccionó **agregar tooPortal**, vaya a tooyour portal toosee el nuevo servidor. O bien, navegue demasiado**más servicios** > **Analysis Services** toosee si el servidor está listo.

 ![Panel](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Pasos siguientes
Una vez que haya creado el servidor, puede [implementar un modelo](analysis-services-deploy.md) tooit mediante SSDT o con SSMS.

Si un modelo se implementa tooyour servidor conecta a orígenes de datos locales de tooon, deberá tooinstall un [puerta de enlace de datos local](analysis-services-gateway.md) en un equipo de la red.

