---
title: "aaaMake web, móviles y los usuarios de API aplicaciones disponibles tooyour pila de Azure | Documentos de Microsoft"
description: "Tutorial tooinstall Hola proveedor de recursos de servicio de aplicaciones y crear ofertas que proporcionan la pila de Azure a los usuarios Hola capacidad toocreate web, móviles y aplicaciones de API."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a>Asegúrese de web, móviles y los usuarios de API aplicaciones disponibles tooyour pila de Azure

Como administrador de la nube de Azure Stack, puede crear ofertas que permitan a los usuarios (inquilinos) crear aplicaciones web, móviles y de API, así como de Azure Functions. Si proporciona acceso a los usuarios de toothese a petición, en la nube aplicaciones tooyour, puede guardarlos tiempo y recursos. tooset este servicio, tendrá que:

> [!div class="checklist"]
> * Implementar Hola proveedor de recursos de servicio de aplicaciones
> * Creación de una oferta
> * Oferta de prueba Hola

## <a name="deploy-hello-app-service-resource-provider"></a>Implementar Hola proveedor de recursos de servicio de aplicaciones

1. [Preparar el host del Kit de desarrollo de Azure pila hello](azure-stack-app-service-before-you-get-started.md). Esto incluye la implementación de proveedor de recursos de SQL Server de hello, que es necesario para crear aplicaciones.
2. [Descargar los scripts de instalador y la aplicación auxiliar de hello](azure-stack-app-service-deploy.md#download-the-required-components).
3. [Ejecutar script de aplicación auxiliar de hello toocreate requerido certificados](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).
4. [Instalar el proveedor de recursos de servicio de aplicaciones de hello](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (tardará tooinstall un par de horas y para todos los Hola tooappear de roles de trabajo).
5. [Validar la instalación de hello](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).

## <a name="create-an-offer"></a>Creación de una oferta

Por ejemplo, puede crear una oferta que permita a los usuarios crear sistemas de administración de contenido web DNN. Requiere el servicio de SQL Server de Hola que ya ha habilitado mediante la instalación de proveedor de recursos de SQL Server de Hola.

1.  [Establezca una cuota](azure-stack-setting-quotas.md) y asígnele el nombre *CuotaDeAppService*. Seleccione **Microsoft.Web** para hello **Namespace** campo.
2.  [Cree un plan](azure-stack-create-plan.md). Asígnele el nombre *TestAppServicePlan*, seleccione Hola Hola **Microsoft.SQL** servicio, y **cuota de servicio de aplicaciones** cuota.

    > [!NOTE]
    > los usuarios de toolet crear otras aplicaciones, otros servicios pueden ser necesaria en el plan de Hola. Por ejemplo, las funciones de Azure requiere ese plan Hola incluyen hello **almacenamiento de Microsoft** de servicio, mientras que requiere de Wordpress **Microsoft.MySQL**.
    > 
    >

3.  [Crear una oferta](azure-stack-create-offer.md), asígnele el nombre **TestAppServiceOffer** y seleccione hello **TestAppServicePlan** plan.

## <a name="test-hello-offer"></a>Oferta de prueba Hola

Ahora que ha implementado Hola proveedor de recursos de servicio de aplicaciones y crear una oferta, puede iniciar sesión como un usuario, suscribirse toohello oferta y crear una aplicación. En este ejemplo, vamos a crear un sistema de administración de contenido de la plataforma DNN. Primero debe crear una base de datos SQL y, a continuación, aplicación web de hello DNN.

### <a name="subscribe-toohello-offer"></a>Suscribirse toohello oferta
1. Inicie sesión en toohello portal de Azure pila (https://portal.local.azurestack.external) como un inquilino.
2. Haga clic en **Obtener una suscripción** > escriba **SuscripciónDePruebaDeAppService** en **Nombre para mostrar** > **Seleccionar una oferta**  >  **OfertaDePruebaDeAppService** > **Crear**.

### <a name="create-a-sql-database"></a>Creación de una base de datos SQL

1. Haga clic en **+** > **Datos y almacenamiento** > **SQL Database**.
2. Deje Hola los valores predeterminados para los campos de hello, excepto como se indica a continuación:
    - **Nombre de la base de datos**: DNNdb
    - **Tamaño máximo en MB**: 100
    - **Suscripción**: OfertaDePruebaDeAppService
    - **Grupo de recursos**: DNN-RG
3. Haga clic en **configuración de inicio de sesión**, escriba las credenciales de base de datos de hello y, a continuación, haga clic en **Aceptar**. Usará estas credenciales más adelante en estos pasos.
4. Haga clic en **SKU** > seleccione Hola SQL SKU que ha creado para Hola de hospedaje de SQL Server > **Aceptar**.
5. Haga clic en **Crear**.

### <a name="create-a-dnn-app"></a>Creación de una aplicación DNN    

1. Haga clic en  **+**   >  **Ver todo** > **DNN Platform preview** (Versión preliminar de la plataforma DNN)  > **Crear**.
2. Escriba *AppDNN* en **Nombre de la aplicación** y seleccione **OfertaDePruebaDeAppService** en **Suscripción**.
3. Haga clic en **Configurar los valores obligatorios** > **Crear nuevo** > escriba un nombre de **Plan de App Service**.
4. Haga clic en **Nivel de precios** > **F1 gratuito** > **Seleccionar** > **Aceptar**.
5. Haga clic en **base de datos** y especificar información de hello para la base de datos SQL de Hola que creó anteriormente.
6. Haga clic en **Crear**.

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Implementar Hola proveedor de recursos de servicio de aplicaciones
> * Creación de una oferta
> * Oferta de prueba Hola

Avanzar toohello siguiente tutorial toolearn cómo para:

> [!div class="nextstepaction"]
> [Implementar aplicaciones tooAzure y la pila de Azure](azure-stack-solution-pipeline.md)
