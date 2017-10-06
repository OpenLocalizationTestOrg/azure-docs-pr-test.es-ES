---
title: "toocreate aaaUse 2.0 CLI una aplicación de Azure AD y configúrelo tooaccess API de servicios multimedia de Azure | Documentos de Microsoft"
description: "Este tema se muestra cómo toouse CLI 2.0 toocreate una aplicación de Azure AD y configúrelo tooaccess API de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Utilice CLI 2.0 toocreate una aplicación AAD y configúrelo tooaccess API de servicios multimedia de Azure

Este tema muestra cómo toouse CLI 2.0 toocreate una aplicación de Azure Active Directory (Azure AD) y servicio principal tooaccess servicios multimedia de Azure recursos. 

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta de Azure. Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Una cuenta de Media Services. Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de hello](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Usar hello Shell en la nube de Azure

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Inicie Hola Shell en la nube desde el panel de navegación superior de hello del portal de Hola.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Para más información, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Crear una aplicación de Azure AD y configurar la cuenta de acceso de medios toohello con CLI 2.0
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Por ejemplo:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

En este ejemplo, Hola **ámbito** es ruta de acceso de recurso completo de Hola para medios de hello cuenta de servicios. Sin embargo, Hola **ámbito** puede estar en cualquier nivel.

Por ejemplo, podría ser uno de hello siguientes niveles:
 
* Hola **suscripción** nivel.
* Hola **grupo de recursos** nivel.
* Hola **recursos** (por ejemplo, una cuenta de medios).

Para más información, vea [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Consulte también [Manage Role-Based el Control de acceso con hello Azure interfaz de línea de comandos](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-portal-upload-files.md).
