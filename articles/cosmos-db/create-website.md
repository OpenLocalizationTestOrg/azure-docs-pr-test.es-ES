---
title: "una aplicación web con una plantilla - base de datos de Azure Cosmos aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una cuenta de base de datos de Azure Cosmos, aplicaciones de Web del servicio de aplicación de Azure y un ejemplo de aplicación mediante una plantilla de Azure Resource Manager web."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Implementar Azure Cosmos DB y Azure App Service Web Apps con una plantilla de Azure Resource Manager
Este tutorial muestra cómo toouse una toodeploy de plantilla de Azure Resource Manager e integrar [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/), [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicación web y una aplicación web de ejemplo.

Usar plantillas de Azure Resource Manager, puede automatizar fácilmente Hola implementación y configuración de los recursos de Azure.  Este tutorial se muestra cómo toodeploy una aplicación web y configurar automáticamente la información de conexión de cuenta de base de datos de Azure Cosmos.

Después de completar este tutorial, será hello tooanswer pueda siguientes preguntas:  

* ¿Cómo puedo usar un toodeploy de plantilla de administrador de recursos de Azure e integrar una cuenta de base de datos de Azure Cosmos y una aplicación web en el servicio de aplicación de Azure?
* ¿Cómo puedo usar un toodeploy de plantilla de administrador de recursos de Azure e integrar una cuenta de base de datos de Azure Cosmos, una aplicación web en aplicación del servicio de aplicaciones Web y una aplicación de Webdeploy?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Requisitos previos
> [!TIP]
> Aunque este tutorial no supone experiencia previa con plantillas del Administrador de recursos de Azure o JSON, debe desea hello toomodify hace referencia a plantillas u opciones de implementación, a continuación, se requerirá el conocimiento de cada una de estas áreas.
> 
> 

Antes de seguir las instrucciones de hello en este tutorial, asegúrese de que tiene Hola siguientes:

* Una suscripción de Azure. Azure es una plataforma basada en suscripción.  Para más información sobre cómo obtener una suscripción, consulte [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/), [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) o [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Paso 1: Descargar archivos de plantilla de Hola
Empecemos por descargar los archivos de plantilla de Hola que se usará en este tutorial.

1. Descargar hello [crear una cuenta de base de datos de Azure Cosmos, las aplicaciones Web e implementar un ejemplo de aplicación de demostración](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) carpeta local de plantilla tooa (p. ej. C:\Azure Cosmos DBTemplates). Con esta plantilla se implementará una cuenta de Azure Cosmos DB, una aplicación web de App Service y una aplicación web.  Cuenta de base de datos de Azure Cosmos hello web aplicaciones tooconnect toohello configurará también automáticamente.
2. Descargar hello [crear un ejemplo de aplicaciones Web y la cuenta de base de datos de Azure Cosmos](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) carpeta local de plantilla tooa (p. ej. C:\Azure Cosmos DBTemplates). Esta plantilla implementará una cuenta de base de datos de Azure Cosmos, una aplicación de servicio de aplicaciones web y va a modificar información del sitio de hello aplicación configuración tooeasily superficial base de datos de Azure Cosmos conexión, pero no incluye una aplicación web.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Paso 2: Implementar la cuenta de base de datos de Azure Cosmos hello, ejemplo de aplicación de web app y demostración de servicio de aplicaciones
Ahora vamos a implementar nuestra primera plantilla.

> [!TIP]
> plantilla de Hello no valida que el nombre de la aplicación hello y nombre de cuenta de base de datos de Azure Cosmos especificado a continuación son un) válidos y b) disponibles.  Se recomienda encarecidamente que compruebe la disponibilidad Hola de hello los nombres que planear la implementación de Hola de toosupply toosubmitting anterior.
> 
> 

1. Inicio de sesión toohello [Portal de Azure](https://portal.azure.com), haga clic en nuevo y busque "Implementación de plantilla".
    ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment1.png)
2. Seleccione el elemento de plantilla de implementación de Hola y haga clic en **crear** ![captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment2.png)
3. Haga clic en **Editar plantilla**, pegue contenido de Hola Hola DocDBWebsiteTodo.json del archivo de plantilla y haga clic en **guardar**.
   ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment3.png)
4. Haga clic en **editar parámetros**, proporcione valores para cada uno de los parámetros obligatorios hello y haga clic en **Aceptar**.  Hola parámetros son como sigue:
   
   1. Nombre del sitio: Especifica el nombre de la aplicación de servicio de aplicaciones web de Hola y es usado tooconstruct Hola URL que va a usar la aplicación web de tooaccess hello (por ejemplo, si se especifica "mydemodocdbwebapp", dirección URL de Hola por el que tendrá acceso a aplicaciones web de hello será mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Especifica nombre Hola de toocreate de plan de hospedaje de servicio de aplicación.
   3. UBICACIÓN: Especifica Hola ubicación de Azure en qué toocreate hello web y base de datos de Azure Cosmos recursos de la aplicación.
   4. DATABASEACCOUNTNAME: Especifica nombre Hola de toocreate de cuenta de base de datos de Azure Cosmos Hola.   
      
      ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment4.png)
5. Elija un grupo de recursos existente o proporcionar un nombre toomake un nuevo grupo de recursos y elegir una ubicación para el grupo de recursos de Hola.

    ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment5.png)
6. Haga clic en **revisar los términos legales**, **compra**y, a continuación, haga clic en **crear** implementación de hello toobegin.  Seleccione **toodashboard Pin** por lo que es visible en la página principal del portal Azure implementación resultante Hola.
   ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment6.png)
7. Cuando finalice la implementación de hello, se abrirá la hoja de grupo de recursos de Hola.
   ![Captura de pantalla de hoja del grupo de recursos de Hola](./media/create-website/TemplateDeployment7.png)  
8. toouse Hola aplicación, simplemente vaya URL de la aplicación web toohello (en el ejemplo de Hola anterior, dirección URL de hello sería http://mydemodocdbwebapp.azurewebsites.net).  Verá Hola tras la aplicación web:
   
   ![Aplicación de tareas pendientes de ejemplo](./media/create-website/image2.png)
9. Continúe y cree un par de tareas en la aplicación web de hello y vuelva hoja del grupo de recursos de toohello Hola portal de Azure. Haga clic en recurso de cuenta de base de datos de Azure Cosmos hello en lista de recursos de hello y, a continuación, haga clic en **Explorer consulta**.
    ![Captura de pantalla de hello resumen lente con la aplicación web de hello resaltado](./media/create-website/TemplateDeployment8.png)  
10. Ejecutar consulta predeterminada de hello, "Seleccione * de c" e inspeccionar los resultados de Hola.  Tenga en cuenta que consultan Hola ha recuperado la representación JSON de Hola de elementos de lista de tareas de Hola que creó en el paso 7 anterior.  Cree tooexperiment gratuita con consultas; Por ejemplo, pruebe a ejecutar SELECT * FROM c c.isComplete WHERE = true tooreturn todos los elementos de lista de tareas que se han marcado como completados.
    
    ![Captura de pantalla de hojas de explorador de consulta y resultados de hello mostrando Hola resultados de consulta](./media/create-website/image5.png)
11. Sentirse tooexplore libre Hola experiencia del portal de base de datos de Azure Cosmos o modificar la aplicación de lista de tareas de ejemplo de Hola.  Cuando esté preparado, implementaremos otra plantilla.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Paso 3: Implementar hello cuenta de documento y ejemplo de aplicación web
Ahora implementaremos nuestra segunda plantilla.  Esta plantilla es útil tooshow cómo insertar información de conexión de base de datos de Azure Cosmos como punto de conexión de cuenta y la clave principal en una aplicación web como configuración de la aplicación o como una cadena de conexión personalizada. Por ejemplo, quizás tiene su propia aplicación web que se desee toodeploy con una cuenta de base de datos de Azure Cosmos y tiene información de conexión de hello rellena automáticamente durante la implementación.

> [!TIP]
> plantilla de Hello no valida que el nombre de la aplicación hello y nombre de cuenta de base de datos de Azure Cosmos especificado a continuación son un) válidos y b) disponibles.  Se recomienda encarecidamente que compruebe la disponibilidad Hola de hello los nombres que planear la implementación de Hola de toosupply toosubmitting anterior.
> 
> 

1. Hola [Portal de Azure](https://portal.azure.com), haga clic en nuevo y busque "Implementación de plantilla".
    ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment1.png)
2. Seleccione el elemento de plantilla de implementación de Hola y haga clic en **crear** ![captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment2.png)
3. Haga clic en **Editar plantilla**, pegue contenido de Hola Hola DocDBWebSite.json del archivo de plantilla y haga clic en **guardar**.
   ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment3.png)
4. Haga clic en **editar parámetros**, proporcione valores para cada uno de los parámetros obligatorios hello y haga clic en **Aceptar**.  Hola parámetros son como sigue:
   
   1. Nombre del sitio: Especifica el nombre de la aplicación de servicio de aplicaciones web de Hola y es usado tooconstruct Hola URL que va a usar la aplicación web de tooaccess hello (por ejemplo, si se especifica "mydemodocdbwebapp", dirección URL de Hola por el que tendrá acceso a aplicaciones web de hello será mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Especifica nombre Hola de toocreate de plan de hospedaje de servicio de aplicación.
   3. UBICACIÓN: Especifica Hola ubicación de Azure en qué toocreate hello web y base de datos de Azure Cosmos recursos de la aplicación.
   4. DATABASEACCOUNTNAME: Especifica nombre Hola de toocreate de cuenta de base de datos de Azure Cosmos Hola.   
      
      ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment4.png)
5. Elija un grupo de recursos existente o proporcionar un nombre toomake un nuevo grupo de recursos y elegir una ubicación para el grupo de recursos de Hola.

    ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment5.png)
6. Haga clic en **revisar los términos legales**, **compra**y, a continuación, haga clic en **crear** implementación de hello toobegin.  Seleccione **toodashboard Pin** por lo que es visible en la página principal del portal Azure implementación resultante Hola.
   ![Captura de pantalla de implementación de plantilla de hello interfaz de usuario](./media/create-website/TemplateDeployment6.png)
7. Cuando finalice la implementación de hello, se abrirá la hoja de grupo de recursos de Hola.
   ![Captura de pantalla de hoja del grupo de recursos de Hola](./media/create-website/TemplateDeployment7.png)  
8. Haga clic en recurso de aplicación Web de hello en lista de recursos de hello y, a continuación, haga clic en **configuración de la aplicación** ![captura de pantalla de grupo de recursos de Hola](./media/create-website/TemplateDeployment9.png)  
9. Tenga en cuenta que están presentes para punto de conexión de base de datos de Azure Cosmos hello y cada una de las claves maestras de base de datos de Azure Cosmos Hola configuración de la aplicación.

    ![Captura de pantalla de configuración de la aplicación](./media/create-website/TemplateDeployment10.png)  
10. Sentirse toocontinue libre explorar Hola Portal de Azure, o seguir uno de nuestra base de datos de Azure Cosmos [ejemplos](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate su propia aplicación de base de datos de Azure Cosmos.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Pasos siguientes
¡Enhorabuena! Ha implementado Azure Cosmos DB, una aplicación web de App Service y una aplicación web de ejemplo mediante plantillas de Azure Resource Manager.

* Haga clic en toolearn más información acerca de la base de datos de Azure Cosmos [aquí](http://azure.com/docdb).
* toolearn más información acerca de las aplicaciones Web de servicio de aplicación de Azure, haga clic en [aquí](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn más acerca de las plantillas de Azure Resource Manager, haga clic en [aquí](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)
* Para una toohello guía consulte cambio de toohello portal antiguo nuevo portal de hello: [Hola de referencia para navegar por el Portal clásico de Azure](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=523751), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

