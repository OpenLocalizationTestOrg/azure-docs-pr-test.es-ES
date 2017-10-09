---
title: las operaciones de proveedor del Administrador de recursos aaaAzure | Documentos de Microsoft
description: Detalles de Hola operaciones disponibles en proveedores de recursos de Microsoft Azure Resource Manager Hola
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Operaciones del proveedor de recursos de Azure Resource Manager

Este documento enumeran las operaciones de hello disponibles para cada proveedor de recursos de Microsoft Azure Resource Manager. Se pueden usar en funciones personalizadas tooprovide granular Control de acceso basado en roles (RBAC) permisos tooresources en Azure. Tenga en cuenta que esta no es una lista exhaustiva y que se pueden agregar o eliminar operaciones a medida que se actualiza cada proveedor. Las cadenas de operación seguir el formato de Hola de `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Para obtener una lista completa y actual use `Get-AzureRmProviderOperation` (en PowerShell) o `azure provider operations show` (en CLI de Azure) operaciones toolist de proveedores de recursos de Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Operación | Descripción |
|---|---|
|/configuration/action|Actualiza la configuración del inquilino.|
|/services/action|Actualiza una instancia de servicio en el inquilino de Hola.|
|/configuration/write|Crea una configuración de inquilino.|
|/configuration/read|Lee la configuración de inquilinos de Hola.|
|/services/write|Crea una instancia de servicio en el inquilino de Hola.|
|/services/read|Lee las instancias de servicio de hello en el inquilino de Hola.|
|/services/delete|Elimina una instancia de servicio en el inquilino de Hola.|
|/services/servicemembers/action|Crea una instancia de miembro de servicio en el servicio de Hola.|
|/services/servicemembers/read|Lee la instancia de miembro de servicio de hello en el servicio de Hola.|
|/services/servicemembers/delete|Elimina una instancia de miembro de servicio en el servicio de Hola.|
|/services/servicemembers/alerts/read|Lee las alertas de Hola para un miembro de servicio.|
|/services/alerts/read|Lee las alertas de Hola para un servicio.|
|/services/alerts/read|Lee las alertas de Hola para un servicio.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Operación | Descripción |
|---|---|
|/generateRecommendations/action|Genera recomendaciones|
|/suppressions/action|Crea o actualiza supresiones|
|/register/action|Registra la suscripción Hola Hola Microsoft Advisor|
|/generateRecommendations/read|Obtiene el estado de las recomendaciones generadas|
|/recommendations/read|Lee las recomendaciones|
|/suppressions/read|Obtiene las supresiones|
|/suppressions/delete|Elimina las supresiones|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Operación | Descripción |
|---|---|
|/servers/read|Recupera la información de Hola de hello especifica Analysis Server.|
|/servers/write|Crea o actualiza Hola especifica Analysis Server.|
|/servers/delete|Eliminaciones Hola Analysis Server.|
|/servers/suspend/action|Suspende Hola Analysis Server.|
|/servers/resume/action|Hola de currículos Analysis Server.|
|/servers/checkNameAvailability<br>/action|Comprueba que el nombre dado de la instancia de Analysis Server es válido y no está en uso.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Operación | Descripción |
|---|---|
|/checkNameAvailability/action|Comprueba si el nombre del servicio proporcionado está disponible|
|/register/action|Registra la suscripción para el proveedor de recursos de Microsoft.ApiManagement|
|/unregister/action|Anula el registro de la suscripción para el proveedor de recursos de Microsoft.ApiManagement|
|/service/write|Crea una nueva instancia del servicio API Management|
|/service/read|Lee los metadatos de una instancia del servicio API Management|
|/service/delete|Elimina una instancia del servicio API Management|
|/service/updatehostname/action|Configura, actualiza o elimina los nombres de dominio personalizado de un servicio API Management|
|/service/uploadcertificate/action|Carga el certificado SSL de un servicio API Management|
|/service/backup/action|Copia de seguridad contenedor especificado de toohello de servicio de administración de API en un usuario proporciona la cuenta de almacenamiento|
|/service/restore/action|Restaurar el servicio de administración de API de contenedor especificado de hello en un cuenta de almacenamiento de proporcionado por el usuario|
|/service/managedeployments/action|Cambia SKU y unidades, y agrega o quita las implementaciones regionales del servicio API Management|
|/service/getssotoken/action|Obtiene el token SSO que puede ser toologin usado en el portal de heredado de servicio de administración de API como administrador|
|/service/applynetworkconfigurationupdates/action|Los recursos de Microsoft.ApiManagement de Hola de actualizaciones que se ejecutan en red Virtual toopick actualizan configuración de red.|
|/service/operationresults/read|Obtiene el estado actual de una operación de larga duración|
|/service/networkStatus/read|Obtiene el estado de acceso de red de Hola de recursos.|
|/service/loggers/read|Obtiene una lista de registradores o los detalles de uno de ellos|
|/service/loggers/write|Agrega un nuevo registrador o actualiza los detalles de los registradores existentes|
|/service/loggers/delete|Quita un registrador existente|
|/service/users/read|Obtiene una lista de usuarios registrados o los detalles de la cuenta de un usuario|
|/service/users/write|Registra un nuevo usuario o actualiza los detalles de la cuenta de un usuario existente|
|/service/users/delete|Quita una cuenta de usuario|
|/service/users/generateSsoUrl/action|Genera la dirección URL de SSO. dirección URL de Hello puede ser usado tooaccess del portal de administración|
|/service/users/subscriptions/read|Obtiene una lista de suscripciones de usuario|
|/service/users/keys/read|Obtiene una lista de claves de usuario|
|/service/users/groups/read|Obtiene una lista de grupos de usuario|
|/service/tenant/operationResults/read|Obtiene una lista de resultados de operaciones o el resultado de una operación específica|
|/service/tenant/policy/read|Obtener la configuración de directiva para el inquilino de Hola|
|/service/tenant/policy/write|Establecer configuración de directiva para el inquilino de Hola|
|/service/tenant/policy/delete|Quitar la configuración de directiva para el inquilino de Hola|
|/service/tenant/configuration/save/action|Crea la confirmación con toohello de bifurcación especificada en el repositorio de hello para la instantánea configuración|
|/service/tenant/configuration/deploy/action|Ejecuta una tarea de implementación tooapply cambios de configuración de toohello de bifurcación de Hola git especificado en la base de datos.|
|/service/tenant/configuration/validate/action|Valida los cambios desde la bifurcación de hello git especificado|
|/service/tenant/configuration/operationResults/read|Obtiene una lista de resultados de operaciones o el resultado de una operación específica|
|/service/tenant/configuration/syncState/read|Obtiene el estado de la última sincronización de git|
|/service/tenant/access/read|Obtiene detalles de la información de acceso del inquilino|
|/service/tenant/access/write|Actualiza los detalles de la información de acceso del inquilino|
|/service/tenant/access/regeneratePrimaryKey/action|Regenera la clave de acceso principal|
|/service/tenant/access/regenerateSecondaryKey/action|Regenera la clave de acceso secundaria|
|/service/identityProviders/read|Obtiene una lista de proveedores de identidades o detalles del proveedor de identidades|
|/service/identityProviders/write|Crea un nuevo proveedor de identidades o actualiza los detalles de un proveedor ya existente|
|/service/identityProviders/delete|Elimina el proveedor de identidades existente|
|/service/subscriptions/read|Obtiene una lista de suscripciones de productos o detalles de una suscripción de producto|
|/service/subscriptions/write|Suscribirse a un producto existente de tooan de usuario existente o actualizar los detalles de la suscripción existente. Esta operación puede ser usado toorenew suscripción|
|/service/subscriptions/delete|Elimina la suscripción. Esta operación puede ser usado toodelete suscripción|
|/service/subscriptions/regeneratePrimaryKey/action|Regenera la clave principal de suscripción|
|/service/subscriptions/regenerateSecondaryKey/action|Regenera la clave secundaria de suscripción|
|/service/backends/read|Obtiene una lista de back-ends o detalles de un back-end|
|/service/backends/write|Agregar un nuevo back-end o actualiza los detalles de un back-end ya existente|
|/service/backends/delete|Elimina un backend existente|
|/service/apis/read|Obtiene una lista de todas las API registradas o detalles de una API|
|/service/apis/write|Crea una nueva API o actualiza los detalles de una API ya existente|
|/service/apis/delete|Elimina una API ya existente|
|/service/apis/policy/read|Obtiene los detalles de configuración de directivas de una API|
|/service/apis/policy/write|Establece los detalles de configuración de directivas de una API|
|/service/apis/policy/delete|Elimina la configuración de directivas de la API|
|/service/apis/operations/read|Obtiene una lista de las operaciones de API existentes o detalles de una operación de API|
|/service/apis/operations/write|Crea una nueva operación de API o actualiza una operación de API ya existente|
|/service/apis/operations/delete|Elimina una operación de API ya existente|
|/service/apis/operations/policy/read|Obtiene los detalles de configuración de directivas de una operación|
|/service/apis/operations/policy/write|Establece los detalles de configuración de directivas de una operación|
|/service/apis/operations/policy/delete|Elimina la configuración de directivas de una operación|
|/service/products/read|Obtiene una lista de productos o detalles de un producto|
|/service/products/write|Crea un nuevo producto o actualiza los detalles de un producto existente|
|/service/products/delete|Elimina un producto ya existente|
|/service/products/subscriptions/read|Obtiene una lista de suscripciones de productos|
|/service/products/apis/read|Obtención de una lista de las API de agregado tooexisting producto|
|/service/products/apis/write|Agregar producto de tooexisting API existente|
|/service/products/apis/delete|Elimina una API existente de un producto que ya existe|
|/service/products/policy/read|Obtiene la configuración de directivas de un producto ya existente|
|/service/products/policy/write|Establece la configuración de directivas de un producto ya existente|
|/service/products/policy/delete|Elimina la configuración de directivas de un producto ya existente|
|/service/products/groups/read|Obtiene una lista de grupos de desarrolladores asociados con el producto|
|/service/products/groups/write|Asocia un grupo de desarrolladores ya existente con un producto que ya existe|
|/service/products/groups/delete|Elimina la asociación de un grupo de desarrolladores ya existente con un producto que ya existe|
|/service/openidConnectProviders/read|Obtiene una lista de proveedores de OpenID Connect o detalles del proveedor de OpenID Connect|
|/service/openidConnectProviders/write|Crea un nuevo proveedor de OpenID Connect o actualiza los detalles de un proveedor de OpenID Connect ya existente|
|/service/openidConnectProviders/delete|Elimina un proveedor de OpenID Connect ya existente|
|/service/certificates/read|Obtiene una lista de certificados o detalles de un certificado|
|/service/certificates/write|Agrega un nuevo certificado|
|/service/certificates/delete|Elimina un certificado existente|
|/service/properties/read|Obtiene una lista de todas las propiedades o detalles de una propiedad especificada|
|/service/properties/write|Crea una nueva propiedad o actualiza el valor de una propiedad especificada|
|/service/properties/delete|Elimina una propiedad ya existente|
|/service/groups/read|Obtiene una lista de grupos o detalles de un grupo|
|/service/groups/write|Crea un nuevo grupo o actualiza los detalles de un grupo ya existente|
|/service/groups/delete|Elimina un grupo ya existente|
|/service/groups/users/read|Obtiene una lista de los usuarios del grupo|
|/service/groups/users/write|Agregar grupo de tooexisting de usuario existente|
|/service/groups/users/delete|Elimina un usuario existente de un grupo que ya existe|
|/service/authorizationServers/read|Obtiene una lista de servidores de autorización o detalles de un servidor de autorización|
|/service/authorizationServers/write|Crea un nuevo servidor de autorización o actualiza los detalles de un servidor de autorización ya existente|
|/service/authorizationServers/delete|Quita un servidor de autorización ya existente|
|/service/reports/bySubscription/read|Obtiene un informe agregado por la suscripción.|
|/service/reports/byRequest/read|Obtiene solicitudes de datos de informes|
|/service/reports/byOperation/read|Obtiene un informe agregado por las operaciones|
|/service/reports/byGeo/read|Obtiene un informe agregado por región geográfica|
|/service/reports/byUser/read|Obtiene un informe agregado por los desarrolladores.|
|/service/reports/byTime/read|Obtiene un informe agregado por períodos de tiempo|
|/service/reports/byApi/read|Obtiene un informe agregado por las API|
|/service/reports/byProduct/read|Obtiene un informe agregado por productos.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Operación | Descripción |
|---|---|
|/appidentities/Read|Devuelve Hola recursos (sitio web) registrado con hello puerta de enlace.|
|/appidentities/Write|Crea una nueva identidad de aplicación.|
|/appidentities/Delete|Elimina una identidad de aplicación ya existente.|
|/deploymenttemplates/listMetadata/Action|Muestra los metadatos de la interfaz de usuario asociado con hello paquete API App.|
|/deploymenttemplates/generate/Action|Devuelve una o varias instancias de API App tooprovision de plantilla de implementación.|
|/gateways/Read|Instancia de puerta de enlace de hello devuelve.|
|/gateways/Write|Crea una nueva puerta de enlace o actualiza una ya existente.|
|/gateways/Delete|Elimina una instancia existente de la puerta de enlace.|
|/gateways/listLoginUris/Action|Rellena un almacén de tokens y devuelve los identificadores URI de inicio de sesión de OAuth.|
|/gateways/listKeys/Action|Devuelve los secretos de la puerta de enlace.|
|/gateways/tokens/Write|Crea un nuevo Zumo Token con el nombre especificado de Hola.|
|/gateways/registrations/Read|Devuelve Hola recursos (sitio web) registrado con hello puerta de enlace.|
|/gateways/registrations/Write|Registra un recurso (sitio web) con hello puerta de enlace.|
|/gateways/registrations/Delete|Anula el registro de un recurso (sitio web) de hello puerta de enlace.|
|/apiapps/Read|Devuelve Hola instancia API App.|
|/apiapps/Write|Crea una nueva aplicación de API o actualiza una ya existente.|
|/apiapps/Delete|Elimina una instancia existente de la aplicación de API.|
|/apiapps/listStatus/Action|Devuelve el estado de la aplicación de API.|
|/apiapps/listKeys/Action|Devuelve los secretos de la aplicación de API.|
|/apiapps/apidefinitions/Read|Devuelve la definición de API de la aplicación de API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Operación | Descripción |
|---|---|
|/elevateAccess/action|Concede Hola llamador acceso de administrador de acceso de usuario en el ámbito del inquilino de Hola|
|/classicAdministrators/read|Lee los administradores de hello para la suscripción de Hola.|
|/classicAdministrators/write|Agregar o modificar administrador tooa suscripción.|
|/classicAdministrators/delete|Quita el Administrador de Hola de suscripción de Hola.|
|/locks/read|Obtiene bloqueos en hello especifican ámbito.|
|/locks/write|Agregar bloqueos en hello especificada ámbito.|
|/locks/delete|Eliminar bloqueos en hello especifican ámbito.|
|/policyAssignments/read|Obtiene información sobre una asignación de directiva.|
|/policyAssignments/write|Crear una directiva de asignación en hello especifica el ámbito.|
|/policyAssignments/delete|Eliminar una asignación de directiva en hello especifica ámbito.|
|/permissions/read|Enumera todos los permisos de hello tiene el llamador de hello en un ámbito determinado.|
|/roleDefinitions/read|Obtiene información sobre una definición de roles.|
|/roleDefinitions/write|Crea o actualiza una definición de roles personalizada con permisos especificados y ámbitos asignables.|
|/roleDefinitions/delete|Eliminar Hola especifica la definición de rol personalizada.|
|/providerOperations/read|Obtiene operaciones para todos los proveedores de recursos que pueden usarse en definiciones de roles.|
|/policyDefinitions/read|Obtiene información sobre una definición de directiva.|
|/policyDefinitions/write|Crea una definición de directiva personalizada.|
|/policyDefinitions/delete|Elimina una definición de directiva.|
|/roleAssignments/read|Obtiene información sobre una asignación de roles.|
|/roleAssignments/write|Crear una función de asignación en hello especifica el ámbito.|
|/roleAssignments/delete|Eliminar una asignación de roles en hello especifica ámbito.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Operación | Descripción |
|---|---|
|/automationAccounts/read|Obtiene una cuenta de Azure Automation|
|/automationAccounts/write|Crea o actualiza una cuenta de Azure Automation|
|/automationAccounts/delete|Elimina una cuenta de Azure Automation|
|/automationAccounts/configurations/readContent/action|Obtiene contenidos de DSC de Automatización de Azure|
|/automationAccounts/hybridRunbookWorkerGroups/read|Lee los recursos de Hybrid Runbook Worker|
|/automationAccounts/hybridRunbookWorkerGroups/delete|Elimina los recursos de Hybrid Runbook Worker|
|/automationAccounts/jobSchedules/read|Obtiene una programación de trabajos de Azure Automation|
|/automationAccounts/jobSchedules/write|Crea una programación de trabajos de Azure Automation|
|/automationAccounts/jobSchedules/delete|Elimina una programación de trabajos de Azure Automation|
|/automationAccounts/connectionTypes/read|Obtiene un recurso de tipo de conexión de Azure Automation|
|/automationAccounts/connectionTypes/write|Crea un recurso de tipo de conexión de Azure Automation|
|/automationAccounts/connectionTypes/delete|Elimina un recurso de tipo de conexión de Azure Automation|
|/automationAccounts/modules/read|Obtiene un módulo de Azure Automation|
|/automationAccounts/modules/write|Crea o actualiza un módulo de Azure Automation|
|/automationAccounts/modules/delete|Elimina un módulo de Azure Automation|
|/automationAccounts/credentials/read|Obtiene un recurso de credencial de Azure Automation|
|/automationAccounts/credentials/write|Crea o actualiza un recurso de credencial de Azure Automation|
|/automationAccounts/credentials/delete|Elimina un recurso de credencial de Azure Automation|
|/automationAccounts/certificates/read|Obtiene un recurso de credencial de Azure Automation|
|/automationAccounts/certificates/write|Crea o actualiza un recurso de certificado de Azure Automation|
|/automationAccounts/certificates/delete|Elimina un recurso de certificado de Azure Automation|
|/automationAccounts/schedules/read|Obtiene un recurso de programación de Azure Automation|
|/automationAccounts/schedules/write|Crea o actualiza un recurso de programación de Azure Automation|
|/automationAccounts/schedules/delete|Elimina un recurso de programación de Azure Automation|
|/automationAccounts/jobs/read|Obtiene un trabajo de Azure Automation|
|/automationAccounts/jobs/write|Crea un trabajo de Azure Automation|
|/automationAccounts/jobs/stop/action|Detiene un trabajo de Azure Automation|
|/automationAccounts/jobs/suspend/action|Suspende un trabajo de Azure Automation|
|/automationAccounts/jobs/resume/action|Reanuda un trabajo de Azure Automation|
|/automationAccounts/jobs/runbookContent/action|Obtiene el contenido de Hola de runbook de automatización de Azure de hello en tiempo de Hola Hola ejecución de trabajo|
|/automationAccounts/jobs/output/action|Obtiene el resultado de hello de un trabajo|
|/automationAccounts/jobs/read|Obtiene un trabajo de Azure Automation|
|/automationAccounts/jobs/write|Crea un trabajo de Azure Automation|
|/automationAccounts/jobs/stop/action|Detiene un trabajo de Azure Automation|
|/automationAccounts/jobs/suspend/action|Suspende un trabajo de Azure Automation|
|/automationAccounts/jobs/resume/action|Reanuda un trabajo de Azure Automation|
|/automationAccounts/jobs/streams/read|Obtiene un flujo de trabajos de Azure Automation|
|/automationAccounts/connections/read|Obtiene un recurso de conexión de Azure Automation|
|/automationAccounts/connections/write|Crea o actualiza un recurso de conexión de Azure Automation|
|/automationAccounts/connections/delete|Elimina un recurso de conexión de Azure Automation|
|/automationAccounts/variables/read|Lee un recurso de variable en Azure Automation|
|/automationAccounts/variables/write|Crea o actualiza un recurso de variable de Azure Automation|
|/automationAccounts/variables/delete|Elimina un recurso de variable de Azure Automation|
|/automationAccounts/runbooks/readContent/action|Obtiene el contenido de Hola de un runbook de automatización de Azure|
|/automationAccounts/runbooks/read|Obtiene un runbook de Azure Automation|
|/automationAccounts/runbooks/write|Crea o actualiza un runbook de Azure Automation|
|/automationAccounts/runbooks/delete|Elimina un runbook de Azure Automation|
|/automationAccounts/runbooks/draft/readContent/action|Obtiene el contenido de Hola de un borrador de runbook de automatización de Azure|
|/automationAccounts/runbooks/draft/writeContent/action|Crea contenido de Hola de un borrador de runbook de automatización de Azure|
|/automationAccounts/runbooks/draft/read|Obtiene un borrador de runbook de Azure Automation|
|/automationAccounts/runbooks/draft/publish/action|Publica un borrador de runbook de Azure Automation|
|/automationAccounts/runbooks/draft/undoEdit/action|Deshacer borrador de runbook de automatización de Azure de ediciones tooan|
|/automationAccounts/runbooks/draft/testJob/read|Obtiene un trabajo de prueba del borrador de runbook de Azure Automation|
|/automationAccounts/runbooks/draft/testJob/write|Crea un trabajo de prueba del borrador de runbook de Azure Automation|
|/automationAccounts/runbooks/draft/testJob/stop/action|Detiene un trabajo de prueba del borrador de runbook de Azure Automation|
|/automationAccounts/runbooks/draft/testJob/suspend/action|Suspende un trabajo de prueba del borrador de runbook de Azure Automation|
|/automationAccounts/runbooks/draft/testJob/resume/action|Reanuda un trabajo de prueba del borrador de runbook de Azure Automation|
|/automationAccounts/webhooks/read|Lee un webhook de Azure Automation|
|/automationAccounts/webhooks/write|Crea o actualiza un webhook de Azure Automation|
|/automationAccounts/webhooks/delete|Elimina un webhook de Azure Automation |
|/automationAccounts/webhooks/generateUri/action|Genera un identificador URI para un webhook de Azure Automation|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Este proveedor no es un proveedor de ARM completo y no proporciona ninguna operación de ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Operación | Descripción |
|---|---|
|/register/action|Registra Hola suscripción para el proveedor de recursos de proceso por lotes de Hola y permite la creación de hello de las cuentas de lote|
|/batchAccounts/write|Crea una nueva cuenta de Batch o actualiza una cuenta de Batch ya existente|
|/batchAccounts/read|Enumera las cuentas por lotes u obtiene las propiedades de Hola de una cuenta de lote|
|/batchAccounts/delete|Elimina una cuenta de Batch|
|/batchAccounts/listkeys/action|Enumera las claves de acceso de una cuenta de Batch|
|/batchAccounts/regeneratekeys/action|Regenera las claves de acceso de una cuenta de Batch|
|/batchAccounts/syncAutoStorageKeys/action|Sincroniza las teclas de acceso de cuenta de almacenamiento automático de hello configuradas para una cuenta de lote|
|/batchAccounts/applications/read|Obtiene las propiedades de Hola de una aplicación o enumera las aplicaciones|
|/batchAccounts/applications/write|Crea una nueva aplicación o actualiza una aplicación ya existente|
|/batchAccounts/applications/delete|Elimina una aplicación|
|/batchAccounts/applications/versions/read|Obtiene las propiedades de Hola de un paquete de aplicación|
|/batchAccounts/applications/versions/write|Crea un nuevo paquete de aplicación o actualiza uno ya existente|
|/batchAccounts/applications/versions/activate/action|Activa un paquete de aplicación|
|/batchAccounts/applications/versions/delete|Elimina un paquete de aplicación|
|/locations/quotas/read|Obtiene las cuotas de lote de hello especificado suscripción en la región de Azure especificada Hola|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Operación | Descripción |
|---|---|
|/invoices/read|Enumera las facturas disponibles|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Operación | Descripción |
|---|---|
|/mapApis/Read|Lee una operación|
|/mapApis/Write|Escribe una operación|
|/mapApis/Delete|Elimina una operación|
|/mapApis/regenerateKey/action|Vuelve a generar Hola clave|
|/mapApis/listSecrets/action|Lista Hola secretos|
|/mapApis/listSingleSignOnToken/action|Hola lectura único inicio de sesión en autorización Token para recursos|
|/Operations/read|Descripción de operación de Hola.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Operación | Descripción |
|---|---|
|/checknameavailability/action|Comprueba si un nombre está disponible para su uso con una nueva instancia de Redis Cache|
|/register/action|Registra el proveedor de recursos de hello 'Microsoft.Cache' con una suscripción|
|/unregister/action|Anula el registro de proveedor de recursos de hello 'Microsoft.Cache' con una suscripción|
|/redis/write|Modificar configuración de portal de administración de Hola y la configuración de caché en Redis Hola|
|/redis/read|Ver la configuración y la configuración de caché en Redis hello en el portal de administración de Hola|
|/redis/delete|Delete Hola toda la caché Redis|
|/redis/listKeys/action|Valor de las teclas de acceso de caché en Redis en el portal de administración de Hola Hola de vista|
|/redis/regenerateKey/action|Cambiar el valor de las teclas de acceso de caché en Redis en el portal de administración de Hola Hola|
|/redis/import/action|Importa datos de un formato especificado desde varios blobs en Redis|
|/redis/export/action|Exportar blobs de almacenamiento de datos de Redis tooprefixed en formato especificado.|
|/redis/forceReboot/action|Fuerza el reinicio de una instancia de memoria caché, posiblemente con pérdida de datos.|
|/redis/stop/action|Detiene una instancia de la memoria caché.|
|/redis/start/action|Inicia una instancia de la memoria caché.|
|/redis/metricDefinitions/read|Obtiene las métricas de hello disponibles para una caché en Redis|
|/redis/firewallRules/read|Obtener las reglas de firewall de hello IP de una caché en Redis|
|/redis/firewallRules/write|Editar reglas de firewall de hello IP de una caché en Redis|
|/redis/firewallRules/delete|Elimina las reglas de firewall IP de una instancia de Redis Cache|
|/redis/listUpgradeNotifications/read|Lista Hola últimas notificaciones de actualización para el inquilino de la caché de Hola.|
|/redis/linkedservers/read|Obtiene los servidores vinculados asociados con una instancia de Redis Cache.|
|/redis/linkedservers/write|Agregar servidor vinculado tooa caché en Redis|
|/redis/linkedservers/delete|Elimina un servidor vinculado de una instancia de Redis Cache|
|/redis/patchSchedules/read|Obtiene la programación de una caché en Redis de revisión de Hola|
|/redis/patchSchedules/write|Modificar Hola programación de una caché en Redis de aplicación de revisiones|
|/redis/patchSchedules/delete|Eliminar la programación de revisión de Hola de una caché en Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Operación | Descripción |
|---|---|
|/provisionGlobalAppServicePrincipalInUserTenant/Action|Aprovisiona una entidad de servicio para entidad de aplicación de servicio|
|/validateCertificateRegistrationInformation/Action|Valida un objeto de compra de certificado sin enviarlo|
|/register/action|Registrar el proveedor de recursos de Microsoft Certificates hello para la suscripción de Hola|
|/certificateOrders/Write|Agrega un nuevo certificateOrder o actualiza uno existente|
|/certificateOrders/Delete|Elimina un AppServiceCertificate existente|
|/certificateOrders/Read|Obtener lista de Hola de CertificateOrders|
|/certificateOrders/reissue/Action|Vuelve a emitir un certificateorder existente|
|/certificateOrders/renew/Action|Renueva un certificateorder existente|
|/certificateOrders/retrieveCertificateActions/Action|Recuperar la lista de Hola de acciones de certificado|
|/certificateOrders/retrieveEmailHistory/Action|Recupera el historial de correos electrónicos del certificado|
|/certificateOrders/resendEmail/Action|Vuelve a enviar el correo electrónico de certificado|
|/certificateOrders/verifyDomainOwnership/Action|Comprobar la propiedad del dominio|
|/certificateOrders/resendRequestEmails/Action|Solicitud de reenvío envía por correo electrónico tooanother dirección de correo electrónico|
|/certificateOrders/resendRequestEmails/Action|Recupera el sello del sitio de un certificado emitido de App Service|
|/certificateOrders/certificates/Write|Agrega un nuevo certificado o actualiza uno existente|
|/certificateOrders/certificates/Delete|Elimina un certificado existente|
|/certificateOrders/certificates/Read|Obtener lista de Hola de certificados|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| Operación | Descripción |
|---|---|
|/register/action|Registrar tooClassic proceso|
|/checkDomainNameAvailability/action|Hola comprueba la disponibilidad de un nombre de dominio determinado.|
|/moveSubscriptionResources/action|Mover a otra suscripción de todos los recursos clásicos tooa.|
|/validateSubscriptionMoveAvailability/action|Validar la disponibilidad de la suscripción de hello para la operación de movimiento clásico.|
|/operatingSystemFamilies/read|Enumera Hola familias del sistema operativo invitado disponibles en Microsoft Azure y también muestra las versiones de sistema operativo Hola disponibles para cada f
|/capabilities/read|Muestra las capacidades de Hola|
|/operatingSystems/read|Enumera las versiones de hello del sistema operativo de Hola que están actualmente disponibles en Microsoft Azure.|
|/resourceTypes/skus/read|Obtiene la lista de Sku de Hola para tipos de recursos admitidos.|
|/domainNames/read|Devolver nombres de dominio de Hola para los recursos.|
|/domainNames/write|Agregar o modificar los nombres de dominio de Hola para los recursos.|
|/domainNames/delete|Quitar nombres de dominio de Hola para los recursos.|
|/domainNames/swap/action|Intercambia Hola ranura de producción de toohello de ranura de ensayo.|
|/domainNames/serviceCertificates/read|Devuelve Hola certificados de servicio usados.|
|/domainNames/serviceCertificates/write|Agregar o modificar los certificados de servicio Hola usados.|
|/domainNames/serviceCertificates/delete|Eliminar certificados de servicio de hello usados.|
|/domainNames/serviceCertificates/operationStatuses/read|Lee el estado de la operación de Hola para certificados de servicio de nombres de dominio de Hola.|
|/domainNames/capabilities/read|Muestra las capacidades de nombre de dominio Hola|
|/domainNames/extensions/read|Devuelve Hola extensiones de nombre de dominio.|
|/domainNames/extensions/write|Agregar extensiones de nombre de dominio de Hola.|
|/domainNames/extensions/delete|Quitar extensiones de nombre de dominio de Hola.|
|/domainNames/extensions/operationStatuses/read|Lee el estado de la operación de Hola para extensiones de nombres de dominio de Hola.|
|/domainNames/active/write|Establece el nombre de dominio de active Hola.|
|/domainNames/slots/read|Muestra las ranuras de implementación de Hola.|
|/domainNames/slots/write|Crea o actualiza la implementación de Hola.|
|/domainNames/slots/delete|Elimina una ranura de implementación concreta.|
|/domainNames/slots/start/action|Inicia una ranura de implementación.|
|/domainNames/slots/stop/action|Suspende la ranura de implementación de Hola.|
|/domainNames/slots/operationStatuses/read|Lee el estado de la operación de Hola para las ranuras de nombres de dominio de Hola.|
|/domainNames/slots/roles/read|Obtener ranura de implementación de hello rol Hola.|
|/domainNames/slots/roles/extensionReferences/read|Devuelve Hola referencia de extensión de rol de ranura de implementación de Hola.|
|/domainNames/slots/roles/extensionReferences/write|Agregar o modificar la referencia de extensión de Hola de rol de ranura de implementación de Hola.|
|/domainNames/slots/roles/extensionReferences/delete|Quite la referencia de extensión de Hola de rol de ranura de implementación de Hola.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/read|Lee el estado de la operación de Hola para referencias de extensión de roles de ranuras nombres de dominio de Hola.|
|/domainNames/slots/roles/roleInstances/read|Obtiene la instancia de rol de Hola.|
|/domainNames/slots/roles/roleInstances/restart/action|Reinicia las instancias de rol.|
|/domainNames/slots/roles/roleInstances/reimage/action|Instancia de rol de reimages Hola.|
|/domainNames/slots/roles/roleInstances/operationStatuses/read|Lee el estado de la operación de Hola para instancias de rol de roles de ranuras nombres de dominio de Hola.|
|/domainNames/slots/state/start/write|Cambios Hola toostopped de estado de ranura de implementación.|
|/domainNames/slots/state/stop/write|Cambios Hola toostarted de estado de ranura de implementación.|
|/domainNames/slots/upgradeDomain/write|Recorrer dominio de actualización Hola.|
|/domainNames/internalLoadBalancers/read|Obtiene los equilibradores de carga internos de Hola.|
|/domainNames/internalLoadBalancers/write|Crea un nuevo equilibrio de carga interno.|
|/domainNames/internalLoadBalancers/delete|Quita un nuevo equilibrio de carga interno.|
|/domainNames/internalLoadBalancers/operationStatuses/read|Lee el estado de la operación de Hola de equilibradores de carga internos de nombres de dominio de Hola.|
|/domainNames/loadBalancedEndpointSets/read|Muestra los conjuntos de extremos con equilibrio de carga de Hola|
|/domainNames/loadBalancedEndpointSets/operationStatuses/read|Lee el estado de la operación de Hola de conjuntos de extremos con equilibrio de carga de nombres de dominio de Hola.|
|/domainNames/availabilitySets/read|Mostrar hello conjunto de disponibilidad de recursos de Hola.|
|/quotas/read|Obtener la cuota de hello para la suscripción de Hola.|
|/virtualMachines/read|Recupera una lista de máquinas virtuales.|
|/virtualMachines/write|Agrega o modifica máquinas virtuales.|
|/virtualMachines/delete|Quita máquinas virtuales.|
|/virtualMachines/start/action|Inicie la máquina virtual de Hola.|
|/virtualMachines/redeploy/action|Vuelve a implementar máquina virtual de Hola.|
|/virtualMachines/restart/action|Reinicia las máquinas virtuales.|
|/virtualMachines/stop/action|Se detiene Hola máquina virtual.|
|/virtualMachines/shutdown/action|Apagar la máquina virtual Hola.|
|/virtualMachines/attachDisk/action|Asocia una máquina virtual de datos disco tooa.|
|/virtualMachines/detachDisk/action|Desconecta un disco de datos de una máquina virtual.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/action|Descarga el archivo RDP de hello para la máquina virtual.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/read|Obtiene el grupo de seguridad de red Hola asociado con la interfaz de red de Hola.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/write|Agrega un grupo de seguridad de red asociado con la interfaz de red de Hola.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/delete|Elimina el grupo de seguridad de red de hello asociado con la interfaz de red de Hola.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/operationStatuses/read|Lee el estado de la operación de Hola para las máquinas virtuales de hello asociados a grupos de seguridad de red.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/read|Obtiene las definiciones de las métricas de Hola.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/read|Obtiene la configuración de diagnósticos de Hola.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/write|Agrega o modifica la configuración de diagnóstico.|
|/virtualMachines/metrics/read|Obtiene las métricas de Hola.|
|/virtualMachines/operationStatuses/read|Lee el estado de la operación de Hola para las máquinas virtuales de Hola.|
|/virtualMachines/extensions/read|Obtiene la extensión de máquina virtual de Hola.|
|/virtualMachines/extensions/write|Coloca la extensión de máquina virtual de Hola.|
|/virtualMachines/extensions/operationStatuses/read|Lee el estado de la operación de Hola para las extensiones de máquinas virtuales de Hola.|
|/virtualMachines/asyncOperations/read|Obtiene las operaciones asincrónicas posibles de Hola|
|/virtualMachines/disks/read|Recupera la lista de discos de datos|
|/virtualMachines/associatedNetworkSecurityGroups/read|Obtiene el grupo de seguridad de red de hello asociado a la máquina virtual de Hola.|
|/virtualMachines/associatedNetworkSecurityGroups/write|Agrega un grupo de seguridad de red asociado a la máquina virtual de Hola.|
|/virtualMachines/associatedNetworkSecurityGroups/delete|Elimina el grupo de seguridad de red de hello asociado con la máquina virtual de Hola.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/read|Lee el estado de la operación de Hola para las máquinas virtuales de hello asociados a grupos de seguridad de red.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Operación | Descripción |
|---|---|
|/register/action|Registrar tooClassic red|
|/gatewaySupportedDevices/read|Recupera la lista de Hola de dispositivos compatibles.|
|/reservedIps/read|Obtiene Hola direcciones IP reservadas|
|/reservedIps/write|Agregar una nueva IP reservada|
|/reservedIps/delete|Elimina una IP reservada.|
|/reservedIps/link/action|Vincula una IP reservada|
|/reservedIps/join/action|Une una IP reservada|
|/reservedIps/operationStatuses/read|Lee el estado de la operación de Hola para direcciones IP reservada de Hola.|
|/virtualNetworks/read|Obtener la red virtual de Hola.|
|/virtualNetworks/write|Agrega una nueva red virtual.|
|/virtualNetworks/delete|Elimina la red virtual de Hola.|
|/virtualNetworks/peer/action|Empareja una red virtual con otra red virtual.|
|/virtualNetworks/join/action|Una red virtual de Hola.|
|/virtualNetworks/checkIPAddressAvailability/action|Comprueba la disponibilidad de Hola de una dirección IP determinada en una red virtual.|
|/virtualNetworks/capabilities/read|Muestra las capacidades de Hola|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/read|Obtiene el grupo de seguridad de red de hello asociado a la subred de Hola.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/write|Agrega un grupo de seguridad de red asociado a la subred de Hola.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/delete|Elimina el grupo de seguridad de red de hello asociado a la subred de Hola.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/operationStatuses/read|Lee el estado de la operación de hello para el grupo de seguridad de red de hello red virtual subred asociado.|
|/virtualNetworks/operationStatuses/read|Lee el estado de la operación de Hola para redes virtuales Hola.|
|/virtualNetworks/gateways/read|Obtiene las puertas de enlace de red virtual de Hola.|
|/virtualNetworks/gateways/write|Agrega una puerta de enlace de red virtual.|
|/virtualNetworks/gateways/delete|Elimina la puerta de enlace de red virtual de Hola.|
|/virtualNetworks/gateways/startDiagnostics/action|Inicia el diagnóstico de puerta de enlace de red virtual de Hola.|
|/virtualNetworks/gateways/stopDiagnostics/action|Se detiene Hola diagnóstico de puerta de enlace de red virtual de Hola.|
|/virtualNetworks/gateways/downloadDiagnostics/action|Descargas de diagnóstico de puerta de enlace de Hola.|
|/virtualNetworks/gateways/listCircuitServiceKey/action|Recupera la clave de servicio del circuito de Hola.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/action|Descarga el script de configuración de dispositivo de Hola.|
|/virtualNetworks/gateways/listPackage/action|Paquete de puerta de enlace de red virtual de Hola de listas.|
|/virtualNetworks/gateways/operationStatuses/read|Lee el estado de la operación de Hola para puertas de enlace de hello redes virtuales.|
|/virtualNetworks/gateways/packages/read|Obtiene el paquete de puerta de enlace de red virtual de Hola.|
|/virtualNetworks/gateways/connections/read|Recupera la lista de Hola de conexiones.|
|/virtualNetworks/gateways/connections/connect/action|Se conecta a una conexión de puerta de enlace de sitio toosite.|
|/virtualNetworks/gateways/connections/disconnect/action|Desconecta una conexión de puerta de enlace de sitio toosite.|
|/virtualNetworks/gateways/connections/test/action|Comprueba una conexión de puerta de enlace de sitio toosite.|
|/virtualNetworks/gateways/clientRevokedCertificates/read|Hola de lectura revoca certificados de cliente.|
|/virtualNetworks/gateways/clientRevokedCertificates/write|Revoca un certificado de cliente.|
|/virtualNetworks/gateways/clientRevokedCertificates/delete|Anula la revocación de un certificado de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/read|Buscar Hola certificados raíz de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/write|Carga un nuevo certificado raíz de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/delete|Elimina el certificado de cliente de puerta de enlace de red virtual de Hola.|
|/virtualNetworks/gateways/clientRootCertificates/download/action|Descarga el certificado con huella digital.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/action|Paquete de certificado de puerta de enlace de red virtual de listas Hola.|
|/networkSecurityGroups/read|Obtiene el grupo de seguridad de red de Hola.|
|/networkSecurityGroups/write|Agrega un nuevo grupo de seguridad de red.|
|/networkSecurityGroups/delete|Elimina el grupo de seguridad de red de Hola.|
|/networkSecurityGroups/operationStatuses/read|Lee el estado de la operación de hello para el grupo de seguridad de red de Hola.|
|/networkSecurityGroups/securityRules/read|Obtiene la regla de seguridad de Hola.|
|/networkSecurityGroups/securityRules/write|Agrega o actualiza una regla de seguridad.|
|/networkSecurityGroups/securityRules/delete|Elimina la regla de seguridad de Hola.|
|/networkSecurityGroups/securityRules/operationStatuses/read|Lee el estado de la operación de Hola para reglas de seguridad del grupo de seguridad de red de Hola.|
|/quotas/read|Obtener la cuota de hello para la suscripción de Hola.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Operación | Descripción |
|---|---|
|/register/action|Registrar tooClassic almacenamiento|
|/checkStorageAccountAvailability/action|Comprueba la disponibilidad de Hola de una cuenta de almacenamiento.|
|/capabilities/read|Muestra las capacidades de Hola|
|/publicImages/read|Obtiene la imagen de máquina virtual pública Hola.|
|/images/read|Imagen de hello devuelve.|
|/storageAccounts/read|Devolver cuenta de almacenamiento de hello con hello dado cuenta.|
|/storageAccounts/write|Agrega una nueva cuenta de almacenamiento.|
|/storageAccounts/delete|Eliminar cuenta de almacenamiento de Hola.|
|/storageAccounts/listKeys/action|Enumera las teclas de acceso de Hola Hola las cuentas de almacenamiento.|
|/storageAccounts/regenerateKey/action|Vuelve a generar claves de acceso existentes de Hola Hola cuenta de almacenamiento.|
|/storageAccounts/operationStatuses/read|Lee el estado de la operación de hello para el recurso de Hola.|
|/storageAccounts/images/read|Devuelve Hola imagen de la cuenta de almacenamiento.|
|/storageAccounts/images/delete|Elimina una imagen determinada de la cuenta de almacenamiento.|
|/storageAccounts/disks/read|Devuelve Hola disco de la cuenta de almacenamiento.|
|/storageAccounts/disks/write|Agrega un disco de cuenta de almacenamiento.|
|/storageAccounts/disks/delete|Elimina un disco de cuenta de almacenamiento determinado.|
|/storageAccounts/disks/operationStatuses/read|Lee el estado de la operación de hello para el recurso de Hola.|
|/storageAccounts/osImages/read|Devuelve Hola imagen de sistema operativo de cuenta de almacenamiento.|
|/storageAccounts/osImages/delete|Elimina una imagen del sistema operativo de la cuenta de almacenamiento.|
|/storageAccounts/services/read|Obtener servicios disponibles de Hola.|
|/storageAccounts/services/metricDefinitions/read|Obtiene las definiciones de las métricas de Hola.|
|/storageAccounts/services/metrics/read|Obtiene las métricas de Hola.|
|/storageAccounts/services/diagnosticSettings/read|Obtiene la configuración de diagnósticos de Hola.|
|/storageAccounts/services/diagnosticSettings/write|Agrega o modifica la configuración de diagnóstico.|
|/disks/read|Devuelve Hola disco de la cuenta de almacenamiento.|
|/osImages/read|Imagen de sistema operativo de hello devuelve.|
|/quotas/read|Obtener la cuota de hello para la suscripción de Hola.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Operación | Descripción |
|---|---|
|/accounts/read|Lee las cuentas de la API.|
|/accounts/write|Escribe las cuentas de la API.|
|/accounts/delete|Elimina las cuentas de la API|
|/accounts/listKeys/action|Enumera las claves|
|/accounts/regenerateKey/action|Regenera una clave|
|/accounts/skus/read|Lee las SKU disponibles para un recurso existente.|
|/accounts/usages/read|Obtener el uso de cuota de Hola para un recurso existente.|
|/Operations/read|Descripción de operación de Hola.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Operación | Descripción |
|---|---|
|/RateCard/read|Devuelve la oferta datos, los metadatos de recurso y medidor y las tasas de hello suscripción concreta.|
|/UsageAggregates/read|Recupera el consumo de Microsoft Azure por parte de una suscripción. resultado de Hello contiene agregados de datos de uso, suscripción y recursos relacionados con la información en un intervalo de tiempo determinado.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción con el proveedor de recursos de Microsoft.Compute|
|/restorePointCollections/read|Obtener propiedades de Hola de una colección de puntos de restauración|
|/restorePointCollections/write|Crea una nueva colección de puntos de restauración o actualiza una ya existente|
|/restorePointCollections/delete|Colección de puntos de restauración de eliminaciones hello y puntos de restauración independiente|
|/restorePointCollections/restorePoints/read|Obtener propiedades de Hola de un punto de restauración|
|/restorePointCollections/restorePoints/write|Crea un nuevo punto de restauración|
|/restorePointCollections/restorePoints/delete|Elimina el punto de restauración de Hola|
|/restorePointCollections/restorePoints/retrieveSasUris/action|Obtener propiedades de Hola de un punto de restauración junto con el URI de SAS de blob|
|/virtualMachineScaleSets/read|Obtener propiedades de Hola de un conjunto de escalas de máquina virtual|
|/virtualMachineScaleSets/write|Crea un nuevo conjunto de escalado de máquinas virtuales o actualiza uno ya existente|
|/virtualMachineScaleSets/delete|Elimina el conjunto de escalas de máquina virtual de Hola|
|/virtualMachineScaleSets/start/action|Inicia Hola instancias de conjunto de escalas de máquina virtual de Hola|
|/virtualMachineScaleSets/powerOff/action|Desconecta de instancias de Hola de conjunto de escalas de máquina virtual de Hola|
|/virtualMachineScaleSets/restart/action|Reinicia las instancias de Hola de conjunto de escalas de máquina virtual de Hola|
|/virtualMachineScaleSets/deallocate/action|Desconecta y recursos de proceso de Hola de versiones para las instancias de Hola de conjunto de escalas de máquina virtual de Hola |
|/virtualMachineScaleSets/manualUpgrade/action|Actualiza manualmente el modelo de toolatest de instancias de conjunto de escalas de máquina virtual de Hola|
|/virtualMachineScaleSets/scale/action|Reduce o escala horizontalmente el recuento de instancias de un conjunto de escalado de máquinas virtuales ya existente|
|/virtualMachineScaleSets/instanceView/read|Obtiene la vista de instancia de Hola de conjunto de escalas de máquina virtual de Hola|
|/virtualMachineScaleSets/skus/read|Listas de Hola SKU válidas de un conjunto de escala de máquina virtual existente|
|/virtualMachineScaleSets/virtualMachines/read|Recupera las propiedades de Hola de una máquina Virtual en un conjunto de escala de VM.|
|/virtualMachineScaleSets/virtualMachines/delete|Elimina una máquina virtual específica de un conjunto de escalado de máquinas virtuales.|
|/virtualMachineScaleSets/virtualMachines/start/action|Inicia una instancia de máquina virtual en un conjunto de escalado de máquinas virtuales.|
|/virtualMachineScaleSets/virtualMachines/powerOff/action|Apaga una instancia de máquina virtual en un conjunto de escalado de máquinas virtuales.|
|/virtualMachineScaleSets/virtualMachines/restart/action|Reinicia una instancia de máquina virtual en un conjunto de escalado de máquinas virtuales.|
|/virtualMachineScaleSets/virtualMachines/deallocate/action|Desconecta y recursos de proceso de Hola de versiones para una máquina Virtual en un conjunto de escala de la máquina virtual.|
|/virtualMachineScaleSets/virtualMachines/instanceView/read|Recupera la vista de instancia de Hola de una máquina Virtual en un conjunto de escala de la máquina virtual.|
|/images/read|Obtener propiedades de Hola de hello imagen|
|/images/write|Crea una nueva imagen o actualiza una ya existente|
|/images/delete|Elimina la imagen de Hola|
|/operations/read|Enumera las operaciones disponibles en el proveedor de recursos de Microsoft.Compute|
|/disks/read|Obtener propiedades de Hola de un disco|
|/disks/write|Crea un nuevo disco o actualiza uno ya existente|
|/disks/delete|Eliminaciones Hola disco|
|/disks/beginGetAccess/action|Obtener Hola URI de SAS de hello disco de acceso de blob|
|/disks/endGetAccess/action|Revocar Hola URI de SAS de hello disco|
|/snapshots/read|Obtener propiedades de Hola de una instantánea|
|/snapshots/write|Crea una nueva instantánea o actualiza una ya existente|
|/snapshots/delete|Elimina una instantánea|
|/availabilitySets/read|Obtener propiedades de Hola de un conjunto de disponibilidad|
|/availabilitySets/write|Crea un nuevo conjunto de disponibilidad o actualiza uno ya existente|
|/availabilitySets/delete|Elimina el conjunto de disponibilidad de Hola|
|/availabilitySets/vmSizes/read|Enumerar los tamaños disponibles para crear o actualizar una máquina virtual en el conjunto de disponibilidad de Hola|
|/virtualMachines/read|Obtener propiedades de Hola de una máquina virtual|
|/virtualMachines/write|Crea una nueva máquina virtual o actualiza una ya existente|
|/virtualMachines/delete|Elimina la máquina virtual de Hola|
|/virtualMachines/start/action|Hola inicia la máquina virtual|
|/virtualMachines/powerOff/action|Desconecta de la máquina virtual de Hola. Tenga en cuenta que la máquina virtual Hola continuará toobe facturada.|
|/virtualMachines/redeploy/action|Vuelve a implementar la máquina virtual|
|/virtualMachines/restart/action|Reinicia la máquina virtual de Hola|
|/virtualMachines/deallocate/action|Desconecta de la máquina virtual de Hola y Hola de versiones de recursos de proceso|
|/virtualMachines/generalize/action|Establece tooGeneralized de estado de máquina virtual de Hola y prepara la máquina virtual de hello para la captura|
|/virtualMachines/capture/action|Captura de máquina virtual de hello mediante la copia de los discos duros virtuales y genera una plantilla que puede ser usado toocreate las máquinas virtuales similares|
|/virtualMachines/convertToManagedDisks/action|Convierte los discos de blob en función de Hola de discos de la máquina virtual toomanaged Hola|
|/virtualMachines/vmSizes/read|Enumera los tamaños disponibles se puede actualizar la máquina virtual de Hola a|
|/virtualMachines/instanceView/read|Obtiene Hola estado en tiempo de ejecución detallado de la máquina virtual de Hola y sus recursos|
|/virtualMachines/extensions/read|Obtener propiedades de Hola de una extensión de máquina virtual|
|/virtualMachines/extensions/write|Crea una nueva extensión de máquina virtual o actualiza una ya existente|
|/virtualMachines/extensions/delete|Elimina la extensión de máquina virtual de Hola|
|/locations/vmSizes/read|Enumera los tamaños disponibles de máquina virtual en una ubicación|
|/locations/usages/read|Obtiene los límites de servicio y las cantidades de uso actual de recursos de proceso de la suscripción de hello en una ubicación|
|/locations/operations/read|Obtiene el estado de saludo de una operación asincrónica|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de registro de contenedor de Hola y permite la creación de hello de los registros de contenedor.|
|/checknameavailability/read|Comprueba que el nombre del registro es válido y que no está en uso.|
|/registries/read|Devuelve la lista de los registros de contenedor de Hola u obtiene Hola propiedades de registro de hello contenedor especificado.|
|/registries/write|Crea un registro de contenedor con Hola parámetros especificados o actualizar las propiedades de Hola o etiquetas para el registro de hello contenedor especificado.|
|/registries/delete|Elimina un registro de contenedor existente.|
|/registries/listCredentials/action|Enumera las credenciales de inicio de sesión de hello para el registro de hello contenedor especificado.|
|/registries/regenerateCredential/action|Vuelve a generar credenciales de inicio de sesión de hello para el registro de hello contenedor especificado.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Operación | Descripción |
|---|---|
|/containerServices/subscriptions/read|Get Hola servicios de contenedor especificados según la suscripción|
|/containerServices/resourceGroups/read|Get Hola servicios de contenedor especificados en función del grupo de recursos|
|/containerServices/resourceGroups/ContainerServiceName/read|Hola obtiene especifica el servicio de contenedor.|
|/containerServices/resourceGroups/ContainerServiceName/write|Coloca u Hola actualizaciones especificado servicio de contenedor.|
|/containerServices/resourceGroups/ContainerServiceName/delete|Hola eliminaciones especifica el servicio de contenedor|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Operación | Descripción |
|---|---|
|/updateCommunicationPreference/action|Actualiza las preferencias de comunicación|
|/listCommunicationPreference/action|Enumera las preferencias de comunicación|
|/applications/read|Lee una operación|
|/applications/write|Escribe una operación|
|/applications/write|Escribe una operación|
|/applications/delete|Elimina una operación|
|/applications/listSecrets/action|Enumera secretos|
|/applications/listSingleSignOnToken/action|Lee tokens de inicio de sesión único|
|/operations/read|operaciones de lectura|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Operación | Descripción |
|---|---|
|/hubs/read|Lee todos los concentradores de Azure Customer Insights|
|/hubs/write|Crea o actualiza todos los concentradores de Azure Customer Insights|
|/hubs/delete|Elimina todos los concentradores de Azure Customer Insights|
|/hubs/providers/Microsoft.Insights/metricDefinitions/read|Obtiene las métricas disponibles de hello para el recurso|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/read|Obtiene la configuración de diagnóstico de hello para el recurso de Hola|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/write|Crea o actualiza la configuración de diagnóstico de hello para el recurso de Hola|
|/hubs/providers/Microsoft.Insights/logDefinitions/read|Obtiene los registros disponibles de Hola para recursos|
|/hubs/authorizationPolicies/read|Lee todas las directivas de firma de acceso compartido de Azure Customer Insights|
|/hubs/authorizationPolicies/write|Crea o actualiza todas las directivas de firma de acceso compartido de Azure Customer Insights|
|/hubs/authorizationPolicies/delete|Elimina todas las directivas de firma de acceso compartido de Azure Customer Insights|
|/hubs/authorizationPolicies/regeneratePrimaryKey/action|Regenera la clave principal de la directiva de firma de acceso compartido de Azure Customer Insights|
|/hubs/authorizationPolicies/regenerateSecondaryKey/action|Regenera la clave secundaria de la directiva de firma de acceso compartido de Azure Customer Insights|
|/hubs/profiles/read|Lee todos los perfiles de Azure Customer Insights|
|/hubs/profiles/write|Escribe todos los perfiles de Azure Customer Insights|
|/hubs/kpi/read|Lee todos los indicadores clave de rendimiento de Azure Customer Insights|
|/hubs/kpi/write|Crea o actualiza todos los indicadores clave de rendimiento de Azure Customer Insights|
|/hubs/kpi/delete|Elimina todos los indicadores clave de rendimiento de Azure Customer Insights|
|/hubs/views/read|Lee todas vistas de aplicación de Azure Customer Insights|
|/hubs/views/write|Crea o actualiza todas las vistas de aplicación de Azure Customer Insights|
|/hubs/views/delete|Elimina todas las vistas de aplicación de Azure Customer Insights|
|/hubs/interactions/read|Lee todas las interacciones de Azure Customer Insights|
|/hubs/interactions/write|Crea o actualiza todas las interacciones de Azure Customer Insights|
|/hubs/roleAssignments/read|Lee todas las asignaciones de control de acceso basado en rol de Azure Customer Insights|
|/hubs/roleAssignments/write|Crea o actualiza todas las asignaciones de control de acceso basado en rol de Azure Customer Insights|
|/hubs/roleAssignments/delete|Elimina todas las asignaciones de control de acceso basado en rol de Azure Customer Insights|
|/hubs/connectors/read|Lee todos los conectores de Azure Customer Insights|
|/hubs/connectors/write|Crea o actualiza todos los conectores de Azure Customer Insights|
|/hubs/connectors/delete|Elimina todos los conectores de Azure Customer Insights|
|/hubs/connectors/mappings/read|Lee todas las asignaciones de conectores de Azure Customer Insights|
|/hubs/connectors/mappings/write|Crea o actualiza todas las asignaciones de conectores de Azure Customer Insights|
|/hubs/connectors/mappings/delete|Elimina todas las asignaciones de conectores de Azure Customer Insights|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Operación | Descripción |
|---|---|
|/checkNameAvailability/action|Comprueba la disponibilidad del nombre del catálogo del inquilino.|
|/catalogs/read|Obtiene las propiedades de los catálogos de la suscripción o grupo de recursos.|
|/catalogs/write|Crea etiquetas Hola de catálogo o las actualizaciones y las propiedades de catálogo de Hola.|
|/catalogs/delete|Elimina el catálogo de Hola.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Operación | Descripción |
|---|---|
|/datafactories/read|Lee datos de Data Factory.|
|/datafactories/write|Crea o actualiza una instancia de Data Factory|
|/datafactories/delete|Elimina una instancia de Data Factory.|
|/datafactories/datapipelines/read|Lee la canalización.|
|/datafactories/datapipelines/delete|Elimina la canalización.|
|/datafactories/datapipelines/pause/action|Pausa la canalización.|
|/datafactories/datapipelines/resume/action|Reanuda la canalización.|
|/datafactories/datapipelines/update/action|Actualiza la canalización.|
|/datafactories/datapipelines/write|Crea o actualiza la canalización|
|/datafactories/linkedServices/read|Lee un servicio vinculado.|
|/datafactories/linkedServices/delete|Elimina un servicio vinculado.|
|/datafactories/linkedServices/write|Crea o actualiza un servicio vinculado|
|/datafactories/tables/read|Lee una tabla.|
|/datafactories/tables/delete|Elimina una tabla.|
|/datafactories/tables/write|Crea o actualiza una tabla|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Operación | Descripción |
|---|---|
|/accounts/read|Obtener información acerca de hello DataLakeAnalytics cuenta.|
|/accounts/write|Crear o actualizar la cuenta de hello DataLakeAnalytics.|
|/accounts/delete|Eliminar cuenta de hello DataLakeAnalytics.|
|/accounts/firewallRules/read|Obtiene información acerca de una regla de firewall.|
|/accounts/firewallRules/write|Crea o actualiza una regla de firewall.|
|/accounts/firewallRules/delete|Elimina una regla de firewall.|
|/accounts/storageAccounts/read|Obtener la cuenta de almacenamiento vinculada hello DataLakeAnalytics cuenta.|
|/accounts/storageAccounts/write|Vincular un toohello de cuenta DataLakeAnalytics cuenta de almacenamiento.|
|/accounts/storageAccounts/delete|Desvincular una cuenta de almacenamiento de hello DataLakeAnalytics cuenta.|
|/accounts/storageAccounts/Containers/read|Obtener contenedores en hello cuenta de almacenamiento|
|/accounts/storageAccounts/Containers/listSasTokens/action|Lista de Tokens de SAS para el contenedor de almacenamiento de Hola|
|/accounts/dataLakeStoreAccounts/read|Obtener cuenta DataLakeStore vinculada hello DataLakeAnalytics cuenta.|
|/accounts/dataLakeStoreAccounts/write|Vincular un toohello de cuenta DataLakeStore DataLakeAnalytics cuenta.|
|/accounts/dataLakeStoreAccounts/delete|Desvincular una cuenta de DataLakeStore de hello DataLakeAnalytics cuenta.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Operación | Descripción |
|---|---|
|/accounts/read|Obtiene información acerca de una cuenta de DataLakeStore existente.|
|/accounts/write|Crea una nueva cuenta de DataLakeStore o actualiza una cuenta de DataLakeStore existente.|
|/accounts/delete|Elimina una cuenta de DataLakeStore existente.|
|/accounts/firewallRules/read|Obtiene información acerca de una regla de firewall.|
|/accounts/firewallRules/write|Crea o actualiza una regla de firewall.|
|/accounts/firewallRules/delete|Elimina una regla de firewall.|
|/accounts/trustedIdProviders/read|Obtiene información acerca de un proveedor de identidades de confianza.|
|/accounts/trustedIdProviders/write|Crea o actualiza un proveedor de identidades de confianza.|
|/accounts/trustedIdProviders/delete|Elimina un proveedor de identidades de confianza.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Operación | Descripción |
|---|---|
|/register/action|Registrar la suscripción de Hola Hola el centro de IOT recursos proveedor y permite hello para la creación de recursos el centro de IOT|
|/checkNameAvailability/Action|Comprueba si el nombre de la instancia de IotHub está disponible|
|/usages/Read|Obtiene los detalles de uso de la suscripción para este proveedor.|
|/operations/Read|Obtiene todas las operaciones de ResourceProvider|
|/iotHubs/Read|Obtiene los recursos de hello el centro de IOT|
|/iotHubs/Write|Crea o actualiza los recursos de IotHub|
|/iotHubs/Delete|Elimina los recursos de IotHub|
|/iotHubs/listkeys/Action|Obtiene todas las claves de IotHub|
|/iotHubs/exportDevices/Action|Exporta los dispositivos|
|/iotHubs/importDevices/Action|Importa los dispositivos|
|/IotHubs/metricDefinitions/read|Obtiene las métricas disponibles de Hola para hello servicio el centro de IOT|
|/iotHubs/iotHubKeys/listkeys/Action|Obtener IotHub Key para el nombre proporcionado de Hola|
|/iotHubs/iotHubStats/Read|Obtiene las estadísticas de IotHub|
|/iotHubs/quotaMetrics/Read|Obtiene las métricas de cuota|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Crea un grupo de consumidores de EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Obtiene los grupos de consumidores de EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Delete|Elimina los grupos de consumidores de EventHub|
|/iotHubs/routing/routes/$testall/Action|Prueba un mensaje en todas las rutas existentes|
|/iotHubs/routing/routes/$testnew/Action|Prueba un mensaje en una ruta proporcionada de pruebas|
|/IotHubs/diagnosticSettings/read|Obtiene la configuración de diagnóstico de hello para el recurso de Hola|
|/IotHubs/diagnosticSettings/write|Crea o actualiza la configuración de diagnóstico de hello para el recurso de Hola|
|/iotHubs/skus/Read|Obtiene SKU válidas de IotHub|
|/iotHubs/jobs/Read|Obtiene detalles de los trabajos enviados en una determinada instancia de IotHub|
|/iotHubs/routingEndpointsHealth/Read|Obtiene el mantenimiento de Hola de todos los extremos de enrutamientos para el que un centro de IOT|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Operación | Descripción |
|---|---|
|/Subscription/register/action|Registra la suscripción de Hola|
|/labs/delete|Elimina laboratorios.|
|/labs/read|Lee laboratorios.|
|/labs/write|Agrega o modifica laboratorios.|
|/labs/ListVhds/action|Enumera las imágenes de disco disponibles para la creación de imágenes personalizadas.|
|/labs/GenerateUploadUri/action|Generar un URI para cargar imágenes de disco personalizada tooa laboratorio.|
|/labs/CreateEnvironment/action|Crea máquinas virtuales en un laboratorio.|
|/labs/ClaimAnyVm/action|Notificación de una máquina virtual claimable aleatoria en laboratorio Hola.|
|/labs/ExportResourceUsage/action|Exportaciones Hola uso de recursos de laboratorio en una cuenta de almacenamiento|
|/labs/users/delete|Elimina perfiles de usuario.|
|/labs/users/read|Lee perfiles de usuario.|
|/labs/users/write|Agrega o modifica perfiles de usuario.|
|/labs/users/secrets/delete|Elimina secretos.|
|/labs/users/secrets/read|Lee secretos.|
|/labs/users/secrets/write|Agrega o modifica secretos.|
|/labs/users/environments/delete|Elimina entornos.|
|/labs/users/environments/read|Lee entornos.|
|/labs/users/environments/write|Agrega o modifica entornos.|
|/labs/users/disks/delete|Elimina discos.|
|/labs/users/disks/read|Lee discos.|
|/labs/users/disks/write|Agrega o modifica discos.|
|/labs/users/disks/Attach/action|Adjuntar y crear la concesión de Hola de máquina virtual de hello disco toohello.|
|/labs/users/disks/Detach/action|Separar y concesión de Hola de salto del disco de hello adjunta toohello virtual machine.|
|/labs/customImages/delete|Elimina imágenes personalizadas.|
|/labs/customImages/read|Lee imágenes personalizadas.|
|/labs/customImages/write|Agrega o modifica imágenes personalizadas.|
|/labs/serviceRunners/delete|Elimina ejecutores del servicio.|
|/labs/serviceRunners/read|Lee ejecutores del servicio.|
|/labs/serviceRunners/write|Agrega o modifica ejecutores del servicio.|
|/labs/artifactSources/delete|Elimina orígenes de artefacto.|
|/labs/artifactSources/read|Lee orígenes de artefacto.|
|/labs/artifactSources/write|Agrega o modifica orígenes de artefacto.|
|/labs/artifactSources/artifacts/read|Lee artefactos.|
|/labs/artifactSources/artifacts/GenerateArmTemplate/action|Genera una plantilla de ARM para hello dado artefacto, carga la cuenta de almacenamiento de hello requerido archivos tooa y valida artefacto Hola generado.|
|/labs/artifactSources/armTemplates/read|Lee las plantillas de Azure Resource Manager.|
|/labs/costs/read|Lee los costos.|
|/labs/costs/write|Agrega o modifica costos.|
|/labs/virtualNetworks/delete|Elimina redes virtuales.|
|/labs/virtualNetworks/read|Lee redes virtuales.|
|/labs/virtualNetworks/write|Agrega o modifica redes virtuales.|
|/labs/formulas/delete|Elimina fórmulas.|
|/labs/formulas/read|Lee fórmulas.|
|/labs/formulas/write|Agrega o modifica fórmulas.|
|/labs/schedules/delete|Elimina programaciones.|
|/labs/schedules/read|Lee programaciones.|
|/labs/schedules/write|Agrega o modifica programaciones.|
|/labs/schedules/Execute/action|Ejecuta una programación.|
|/labs/schedules/ListApplicable/action|Enumera todas las programaciones aplicables|
|/labs/galleryImages/read|Lee imágenes de la galería.|
|/labs/policySets/EvaluatePolicies/action|Evalúa la directiva de laboratorio.|
|/labs/policySets/policies/delete|Elimina directivas.|
|/labs/policySets/policies/read|Lee directivas.|
|/labs/policySets/policies/write|Agrega o modifica directivas.|
|/labs/virtualMachines/delete|Elimina máquinas virtuales.|
|/labs/virtualMachines/read|Lee máquinas virtuales.|
|/labs/virtualMachines/write|Agrega o modifica máquinas virtuales.|
|/labs/virtualMachines/Start/action|Inicia una máquina virtual.|
|/labs/virtualMachines/Stop/action|Detención de una máquina virtual|
|/labs/virtualMachines/ApplyArtifacts/action|Aplicar máquina toovirtual de artefactos.|
|/labs/virtualMachines/AddDataDisk/action|Conectar una máquina de toovirtual del disco de datos nueva o existente.|
|/labs/virtualMachines/DetachDataDisk/action|Desconectar el disco especificado de hello de la máquina virtual de Hola.|
|/labs/virtualMachines/Claim/action|Toma la propiedad de una máquina virtual existente|
|/labs/virtualMachines/ListApplicableSchedules/action|Enumera todas las programaciones aplicables|
|/labs/virtualMachines/schedules/delete|Elimina programaciones.|
|/labs/virtualMachines/schedules/read|Lee programaciones.|
|/labs/virtualMachines/schedules/write|Agrega o modifica programaciones.|
|/labs/virtualMachines/schedules/Execute/action|Ejecuta una programación.|
|/labs/notificationChannels/delete|Elimina notificationchannels.|
|/labs/notificationChannels/read|Lee notificationchannels.|
|/labs/notificationChannels/write|Agrega o modifica notificationchannels.|
|/labs/notificationChannels/Notify/action|Enviar el canal de notificación tooprovided.|
|/schedules/delete|Elimina programaciones.|
|/schedules/read|Lee programaciones.|
|/schedules/write|Agrega o modifica programaciones.|
|/schedules/Execute/action|Ejecuta una programación.|
|/schedules/Retarget/action|Actualiza un identificador de recurso de destino de la programación.|
|/locations/operations/read|Lee operaciones.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Operación | Descripción |
|---|---|
|/databaseAccountNames/read|Comprueba la disponibilidad del nombre.|
|/databaseAccounts/read|Lee una cuenta de base de datos.|
|/databaseAccounts/write|Actualiza una cuenta de base de datos.|
|/databaseAccounts/listKeys/action|Enumera las claves de una cuenta de base de datos|
|/databaseAccounts/regenerateKey/action|Rota las claves de una cuenta de base de datos|
|/databaseAccounts/listConnectionStrings/action|Obtener cadenas de conexión de Hola para una cuenta de base de datos|
|/databaseAccounts/changeResourceGroup/action|Cambia el grupo de recursos de una cuenta de base de datos|
|/databaseAccounts/failoverPriorityChange/action|Cambia las prioridades de conmutación por error de las regiones de una cuenta de base de datos. Se trata de operación de conmutación por error manual de tooperform usado|
|/databaseAccounts/delete|Elimina las cuentas de base de datos de Hola.|
|/databaseAccounts/metricDefinitions/read|Lee las definiciones de las métricas de cuenta de base de datos de Hola.|
|/databaseAccounts/metrics/read|Lee las métricas de cuenta de base de datos de Hola.|
|/databaseAccounts/usages/read|Lee los usos de cuenta de base de datos de Hola.|
|/databaseAccounts/databases/collections/metricDefinitions/read|Lee colección Hola definiciones de métrica.|
|/databaseAccounts/databases/collections/metrics/read|Lee las métricas de colección de Hola.|
|/databaseAccounts/databases/collections/usages/read|Lee los usos de la colección de Hola.|
|/databaseAccounts/databases/metricDefinitions/read|Lee las definiciones de métrica de base de datos de Hola|
|/databaseAccounts/databases/metrics/read|Lee las métricas de base de datos de Hola.|
|/databaseAccounts/databases/usages/read|Lee los usos de la base de datos de Hola.|
|/databaseAccounts/readonlykeys/read|Lee cuenta de base de datos de hello las claves de solo lectura.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Operación | Descripción |
|---|---|
|/generateSsoRequest/Action|Genera una solicitud para iniciar sesión en el centro de control de dominios.|
|/validateDomainRegistrationInformation/Action|Valida un objeto de compra de dominio sin enviarlo|
|/checkDomainAvailability/Action|Comprueba si un dominio está disponible para su compra|
|/listDomainRecommendations/Action|Recuperar las recomendaciones de dominio de lista Hola según palabras clave|
|/register/action|Registrar el proveedor de recursos de Microsoft Domains hello para la suscripción de Hola|
|/domains/Read|Obtener lista de Hola de dominios|
|/domains/Write|Agrega un nuevo dominio o actualiza uno existente|
|/domains/Delete|Elimina un dominio ya existente.|
|/domains/operationresults/Read|Obtiene una operación de dominio|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Operación | Descripción |
|---|---|
|/lcsprojects/read|Mostrar los proyectos de servicios de ciclo de vida de Microsoft Dynamics que pertenecen el usuario tooa|
|/lcsprojects/write|Crear y actualizar los proyectos de servicios de ciclo de vida de Microsoft Dynamics pertenecen toohello usuario. Propiedades de nombre y una descripción de hello sola se pueden actualizar. no se puede actualizar suscripción de Hola y ubicación asociada con el proyecto de hello después de la creación|
|/lcsprojects/delete|Eliminar proyectos de servicios de ciclo de vida de Microsoft Dynamics que pertenecen el usuario toohello|
|/lcsprojects/clouddeployments/read|Mostrar las implementaciones de Microsoft Dynamics AX 2012 R3 evaluación en un proyecto de servicios de ciclo de vida de Microsoft Dynamics que pertenece el usuario tooa|
|/lcsprojects/clouddeployments/write|Crear implementación de Microsoft Dynamics AX 2012 R3 evaluación en un proyecto de servicios de ciclo de vida de Microsoft Dynamics que pertenece el usuario tooa. Las implementaciones se pueden administrar desde el portal de administración de Azure|
|/lcsprojects/connectors/read|Leer los conectores que pertenecen el proyecto de servicios de ciclo de vida de Microsoft Dynamics tooa|
|/lcsprojects/connectors/write|Crear y actualizar los conectores que pertenecen el proyecto de servicios de ciclo de vida de Microsoft Dynamics tooa|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Operación | Descripción |
|---|---|
|/checkNameAvailability/action|Comprueba la disponibilidad del espacio de nombres en una suscripción dada.|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de EventHub de Hola y permite la creación de hello de recursos de EventHub|
|/namespaces/write|Crea un recurso de espacio de nombres y actualiza sus propiedades. Etiquetas y el estado del programa Hola Namespace son propiedades de Hola que se pueden actualizar.|
|/namespaces/read|Obtener lista de Hola de descripción del recurso Namespace|
|/namespaces/Delete|Elimina el recurso del espacio de nombres|
|/namespaces/metricDefinitions/read|Obtiene una lista de descripciones de recursos de métricas del espacio de nombres|
|/namespaces/authorizationRules/read|Obtener lista de Hola de descripción de las reglas de autorización de espacios de nombres.|
|/namespaces/authorizationRules/write|Crea reglas de autorización en el nivel del espacio de nombres y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/authorizationRules/delete|Elimina la regla de autorización del espacio de nombres. Hola regla de autorización de Namespace predeterminada no se puede eliminar. |
|/namespaces/authorizationRules/listkeys/action|Obtener la cadena de conexión de hello toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Volver a generar Hola principal o secundario clave toohello recursos|
|/namespaces/eventhubs/write|Crea o actualiza propiedades de EventHub.|
|/namespaces/eventhubs/read|Obtiene una lista de descripciones de recursos de EventHub|
|/namespaces/eventhubs/Delete|Operación toodelete recursos de EventHub|
|/namespaces/eventHubs/consumergroups/write|Crea o actualiza las propiedades de ConsumerGroup.|
|/namespaces/eventHubs/consumergroups/read|Obtiene una lista de descripciones de recursos de ConsumerGroup|
|/namespaces/eventHubs/consumergroups/Delete|Operación toodelete ConsumerGroup recursos|
|/namespaces/eventhubs/authorizationRules/read| Obtener lista de hello EventHub de reglas de autorización|
|/namespaces/eventhubs/authorizationRules/write|Crea reglas de autorización de EventHub y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/eventhubs/authorizationRules/delete|Operación toodelete las reglas de autorización de EventHub|
|/namespaces/eventhubs/authorizationRules/listkeys/action|Obtener tooEventHub de cadena de conexión de Hola|
|/namespaces/eventhubs/authorizationRules/regenerateKeys/action|Volver a generar Hola principal o secundario clave toohello recursos|
|/namespaces/diagnosticSettings/read|Obtiene una lista de descripciones de recursos de configuración de diagnósticos del espacio de nombres|
|/namespaces/diagnosticSettings/write|Obtiene una lista de descripciones de recursos de configuración de diagnósticos del espacio de nombres|
|/namespaces/logDefinitions/read|Obtiene una lista de descripciones de recursos de registros del espacio de nombres|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Operación | Descripción |
|---|---|
|/providers/features/read|Obtiene la característica de Hola de una suscripción en un proveedor de recursos determinado.|
|/providers/features/register/action|Característica de Hola para una suscripción se registra en un proveedor de recursos determinado.|
|/features/read|Obtiene las características de Hola de una suscripción.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Operación | Descripción |
|---|---|
|/clusters/write|Crea o actualiza un clúster de HDInsight|
|/clusters/read|Obtiene detalles sobre el clúster de HDInsight|
|/clusters/delete|Elimina un clúster de HDInsight|
|/clusters/changerdpsetting/action|Cambia la configuración de RDP de un clúster de HDInsight|
|/clusters/configurations/action|Actualiza la configuración de un clúster de HDInsight|
|/clusters/configurations/read|Obtiene las configuraciones de un clúster de HDInsight|
|/clusters/roles/resize/action|Cambia el tamaño de un clúster de HDInsight|
|/locations/capabilities/read|Obtiene las funcionalidades de la suscripción|
|/locations/checkNameAvailability/read|Comprueba la disponibilidad del nombre|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de importación y exportación de Hola y permite la creación de hello de trabajos de importación y exportación.|
|/jobs/write|Crea un trabajo con Hola parámetros especificados o actualizar las propiedades de Hola o etiquetas para el trabajo especificado Hola.|
|/jobs/read|Obtiene propiedades de hello para el trabajo especificado de Hola o devuelve la lista de Hola de trabajos.|
|/jobs/listBitLockerKeys/action|Obtiene las claves de BitLocker de hello para el trabajo especificado Hola.|
|/jobs/delete|Elimina un trabajo existente.|
|/locations/read|Obtiene las propiedades de Hola de hello ubicación o devuelve Hola lista especificada de ubicaciones.|

## <a name="microsoftinsights"></a>Microsoft.Insights

| Operación | Descripción |
|---|---|
|/Register/Action|Registrar proveedor de información de microsoft de Hola|
|/AlertRules/Write|Escribir la configuración de regla de alerta de tooan|
|/AlertRules/Delete|Elimina una configuración de regla de alerta|
|/AlertRules/Read|Lee una configuración de regla de alerta|
|/AlertRules/Activated/Action|Regla de alerta activada|
|/AlertRules/Resolved/Action|Regla de alerta resuelta|
|/AlertRules/Throttled/Action|Se limita la regla de alerta|
|/AlertRules/Incidents/Read|Lee una configuración de incidentes de regla de alerta|
|/MetricDefinitions/Read|Lee definiciones de métricas|
|/eventtypes/values/Read|Lee valores de tipo de evento de administración|
|/eventtypes/digestevents/Read|Lee un resumen de tipos de evento de administración|
|/Metrics/Read|Lee métricas|
|/LogProfiles/Write|Escribir la configuración de perfil de registro de tooa|
|/LogProfiles/Delete|Elimina la configuración de perfiles de registro|
|/LogProfiles/Read|Lee perfiles de registro|
|/AutoscaleSettings/Write|Escribir la configuración de escalado automático tooan|
|/AutoscaleSettings/Delete|Elimina una configuración de opciones de escalado automático|
|/AutoscaleSettings/Read|Lee una configuración de opciones de escalado automático|
|/AutoscaleSettings/Scaleup/Action|Operación de escalado vertical de autoescala|
|/AutoscaleSettings/Scaledown/Action|Operación de reducción vertical de autoescala|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Lee definiciones de métricas|
|/ActivityLogAlerts/Activated/Action|Hola desencadenada alerta de registro de actividad|
|/DiagnosticSettings/Write|Configuración de opciones de toodiagnostic de escritura|
|/DiagnosticSettings/Delete|Elimina la configuración de opciones de diagnóstico|
|/DiagnosticSettings/Read|Lee una opción de configuración de diagnóstico|
|/LogDefinitions/Read|Lee definiciones de registro|
|/ExtendedDiagnosticSettings/Write|Escribir la configuración de opciones de diagnóstico de tooextended|
|/ExtendedDiagnosticSettings/Delete|Elimina la configuración de opciones de diagnóstico extendida|
|/ExtendedDiagnosticSettings/Read|Lee una configuración de opciones de diagnóstico extendida|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Operación | Descripción |
|---|---|
|/register/action|Registra una suscripción|
|/checkNameAvailability/read|Comprueba que un nombre de almacén de claves es válido y que no está en uso|
|/vaults/read|Hola ver las propiedades de un almacén de claves|
|/vaults/write|Crear una nueva clave Hola de almacén o actualización de propiedades de un almacén de claves existente|
|/vaults/delete|Elimina un almacén de claves|
|/vaults/deploy/action|Permite obtener acceso a toosecrets en un almacén de claves al implementar recursos de Azure|
|/vaults/secrets/read|Ver las propiedades de un secreto, pero no su valor Hola|
|/vaults/secrets/write|Cree un nuevo valor de hello secreto o actualización de un secreto existente|
|/vaults/accessPolicies/write|Actualizar una directiva de acceso existente mediante combinación o reemplazar, o agregar un nuevo almacén de tooa de directiva de acceso.|
|/deletedVaults/read|Ver propiedades de Hola de soft eliminan almacenes de claves|
|/locations/operationResults/read|Resultado de hello la comprobación de una operación de larga ejecución|
|/locations/deletedVaults/read|Ver las propiedades de un almacén de claves eliminada suave Hola|
|/locations/deletedVaults/purge/action|Purga un almacén de claves eliminado temporalmente|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Operación | Descripción |
|---|---|
|/workflows/read|Lee el flujo de trabajo de Hola.|
|/workflows/write|Crea o actualiza el flujo de trabajo de Hola.|
|/workflows/delete|Elimina el flujo de trabajo de Hola.|
|/workflows/run/action|Inicia una ejecución de flujo de trabajo de Hola.|
|/workflows/disable/action|Deshabilita el flujo de trabajo de Hola.|
|/workflows/enable/action|Permite el flujo de trabajo de Hola.|
|/workflows/validate/action|Valida el flujo de trabajo de Hola.|
|/workflows/move/action|Mueve el flujo de trabajo de su Id. de suscripción, el grupo de recursos o Id. de suscripción diferente de tooa de nombre, grupo de recursos existente, o nombre.|
|/workflows/listSwagger/action|Obtiene el flujo de trabajo de hello las definiciones de swagger.|
|/workflows/regenerateAccessKey/action|Vuelve a generar secretos de clave de acceso de Hola.|
|/workflows/listCallbackUrl/action|Obtiene la dirección URL de devolución de llamada de hello para el flujo de trabajo.|
|/workflows/versions/read|Lee la versión de flujo de trabajo de Hola.|
|/workflows/versions/triggers/listCallbackUrl/action|Obtiene la dirección URL de devolución de llamada de hello para el desencadenador.|
|/workflows/runs/read|Lee el flujo de trabajo de hello ejecutar.|
|/workflows/runs/cancel/action|Cancela la ejecución de Hola de un flujo de trabajo.|
|/workflows/runs/actions/read|Lee el flujo de trabajo de hello ejecutar acción.|
|/workflows/runs/operations/read|Lee el estado de la operación de ejecución de flujo de trabajo de Hola.|
|/workflows/triggers/read|Lee el desencadenador de Hola.|
|/workflows/triggers/run/action|Ejecuta el desencadenador de Hola.|
|/workflows/triggers/listCallbackUrl/action|Obtiene la dirección URL de devolución de llamada de hello para el desencadenador.|
|/workflows/triggers/histories/read|Lee los historiales de desencadenador de Hola.|
|/workflows/triggers/histories/resubmit/action|Vuelve a enviar el desencadenador de flujo de trabajo de Hola.|
|/workflows/accessKeys/read|Lee la clave de acceso de Hola.|
|/workflows/accessKeys/write|Crea o actualiza la clave de acceso de Hola.|
|/workflows/accessKeys/delete|Elimina la clave de acceso de Hola.|
|/workflows/accessKeys/list/action|Enumera los secretos de clave de acceso de Hola.|
|/workflows/accessKeys/regenerate/action|Vuelve a generar secretos de clave de acceso de Hola.|
|/locations/workflows/validate/action|Valida el flujo de trabajo de Hola.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de servicio web de aprendizaje de automático de Hola y permite la creación de hello de servicios web.|
|/webServices/action|Crea propiedades del servicio web regional las regiones admitidas|
|/commitmentPlans/read|Lee todos los planes de compromiso de Machine Learning|
|/commitmentPlans/write|Crea o actualiza todos los planes de compromiso de Machine Learning|
|/commitmentPlans/delete|Elimina todos los planes de compromiso de Machine Learning|
|/commitmentPlans/join/action|Combina todos los planes de compromiso de Machine Learning|
|/commitmentPlans/commitmentAssociations/read|Lee todas las asociaciones de planes de compromiso de Machine Learning|
|/commitmentPlans/commitmentAssociations/move/action|Mueve todas las asociaciones de planes de compromiso de Machine Learning|
|/Workspaces/read|Lee todas las áreas de trabajo de Machine Learning|
|/Workspaces/write|Crea o actualiza todas las áreas de trabajo de Machine Learning|
|/Workspaces/delete|Elimina todas las áreas de trabajo de Machine Learning|
|/Workspaces/listworkspacekeys/action|Enumera las claves de un área de trabajo de Machine Learning|
|/Workspaces/resyncstoragekeys/action|Vuelve a sincronizar las claves de la cuenta de almacenamiento configurada para un área de trabajo de Machine Learning|
|/webServices/read|Lee todos los servicios web Machine Learning|
|/webServices/write|Crea o actualiza todos los servicios web Machine Learning|
|/webServices/delete|Elimina todos los servicios web Machine Learning|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Operación | Descripción |
|---|---|
|/agreements/offers/plans/read|Devuelve un acuerdo para un elemento determinado de Marketplace|
|/agreements/offers/plans/sign/action|Firma un acuerdo para un elemento determinado de Marketplace|
|/agreements/offers/plans/cancel/action|Cancela un acuerdo para un elemento determinado de Marketplace|

## <a name="microsoftmedia"></a>Microsoft.Media

| Operación | Descripción |
|---|---|
|/mediaservices/read||
|/mediaservices/write||
|/mediaservices/delete||
|/mediaservices/regenerateKey/action||
|/mediaservices/listKeys/action||
|/mediaservices/syncStorageKeys/action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de Hola|
|/unregister/action|Anula el registro de suscripción de Hola|
|/checkTrafficManagerNameAvailability/action|Comprueba la disponibilidad de Hola de un nombre DNS de Traffic Manager relativo.|
|/dnszones/read|Obtener la zona DNS de hello, en formato JSON. propiedades de la zona de Hello incluyen etiquetas, etag, numberOfRecordSets y maxNumberOfRecordSets. Tenga en cuenta que este comando no recupera conjuntos de registros de hello contenidos en la zona de Hola.|
|/dnszones/write|Crea o actualiza una zona DNS en un grupo de recursos.  Etiquetas de hello tooupdate usado en un recurso de zona DNS. Tenga en cuenta que este comando no puede ser un conjuntos de registros usado en toocreate o actualización en la zona de Hola.|
|/dnszones/delete|Eliminar la zona DNS de hello, en formato JSON. propiedades de la zona de Hello incluyen etiquetas, etag, numberOfRecordSets y maxNumberOfRecordSets.|
|/dnszones/MX/read|Obtener el conjunto de registros de Hola de tipo 'MX' en formato JSON. conjunto de registros de Hello contiene una lista de registros, así como Hola TTL, tags y etag.|
|/dnszones/MX/write|Crea o actualiza un conjunto de registros del tipo "MX" dentro de una zona DNS. registros de Hello especificados reemplazarán Hola actuales en el conjunto de registros de Hola.|
|/dnszones/MX/delete|Quite el conjunto de registros de Hola de nombre dado y tipo 'MX' de una zona DNS.|
|/dnszones/NS/read|Obtiene el conjunto de registros de DNS del tipo NS|
|/dnszones/NS/write|Crea o actualiza el conjunto de registros de DNS del tipo NS|
|/dnszones/NS/delete|Elimina el conjunto de registros de DNS de Hola de tipo NS|
|/dnszones/AAAA/read|Obtener el conjunto de registros de Hola de tipo 'AAAA', en formato JSON. conjunto de registros de Hello contiene una lista de registros, así como Hola TTL, tags y etag.|
|/dnszones/AAAA/write|Crea o actualiza un conjunto de registros del tipo "AAAA" dentro de una zona DNS. registros de Hello especificados reemplazarán Hola actuales en el conjunto de registros de Hola.|
|/dnszones/AAAA/delete|Elimine el conjunto de registros de Hola de nombre dado y de tipo 'AAAA' de una zona DNS.|
|/dnszones/CNAME/read|Obtener el conjunto de registros de Hola de tipo 'CNAME' en formato JSON. conjunto de registros de Hello contiene Hola TTL, tags y etag.|
|/dnszones/CNAME/write|Crea o actualiza un conjunto de registros del tipo "CNAME" dentro de una zona DNS. registros de Hello especificados reemplazarán Hola actuales en el conjunto de registros de Hola.|
|/dnszones/CNAME/delete|Quite el conjunto de registros de Hola de nombre dado y tipo 'CNAME' de una zona DNS.|
|/dnszones/SOA/read|Obtiene el conjunto de registros de DNS del tipo SOA|
|/dnszones/SOA/write|Crea o actualiza el conjunto de registros de DNS del tipo SOA|
|/dnszones/SRV/read|Obtener el conjunto de registros de Hola de tipo 'SRV' en formato JSON. conjunto de registros de Hello contiene una lista de registros, así como Hola TTL, tags y etag.|
|/dnszones/SRV/write|Crea o actualiza el conjunto de registros del tipo SRV|
|/dnszones/SRV/delete|Quitar el conjunto de registros de Hola de nombre dado y tipo 'SRV' de una zona DNS.|
|/dnszones/PTR/read|Obtener el conjunto de registros de Hola de tipo 'PTR' en formato JSON. conjunto de registros de Hello contiene una lista de registros, así como Hola TTL, tags y etag.|
|/dnszones/PTR/write|Crea o actualiza un conjunto de registros del tipo "PTR" dentro de una zona DNS. registros de Hello especificados reemplazarán Hola actuales en el conjunto de registros de Hola.|
|/dnszones/PTR/delete|Quitar el conjunto de registros de Hola de nombre dado y tipo 'PTR' de una zona DNS.|
|/dnszones/A/read|Obtener el conjunto de registros de Hola de tipo 'A', en formato JSON. conjunto de registros de Hello contiene una lista de registros, así como Hola TTL, tags y etag.|
|/dnszones/A/write|Crea o actualiza un conjunto de registros del tipo "A" dentro de una zona DNS. registros de Hello especificados reemplazarán Hola actuales en el conjunto de registros de Hola.|
|/dnszones/A/delete|Elimine el conjunto de registros de Hola de nombre dado y de tipo 'A' de una zona DNS.|
|/dnszones/TXT/read|Obtener el conjunto de registros de Hola de tipo 'TXT' en formato JSON. conjunto de registros de Hello contiene una lista de registros, así como Hola TTL, tags y etag.|
|/dnszones/TXT/write|Crea o actualiza un conjunto de registros del tipo "TXT" dentro de una zona DNS. registros de Hello especificados reemplazarán Hola actuales en el conjunto de registros de Hola.|
|/dnszones/TXT/delete|Elimine el conjunto de registros de Hola de nombre dado y de tipo 'TXT' de una zona DNS.|
|/dnszones/recordsets/read|Obtiene los conjuntos de registros de DNS entre los tipos|
|/networkInterfaces/read|Obtiene una definición de interfaz de red. |
|/networkInterfaces/write|Crea una interfaz de red o actualiza una interfaz de red existente. |
|/networkInterfaces/join/action|Se une a una interfaz de red de máquina Virtual tooa|
|/networkInterfaces/delete|Elimina una interfaz de red|
|/networkInterfaces/effectiveRouteTable/action|Obtener tabla de rutas configuradas en la interfaz de red de Vm de Hola|
|/networkInterfaces/effectiveNetworkSecurityGroups/action|Obtener hello en red interfaz de configurado grupos de seguridad de red virtual|
|/networkInterfaces/loadBalancers/read|Obtiene todos los equilibradores de carga de Hola Hola de interfaz de red forma parte de|
|/networkInterfaces/ipconfigurations/read|Obtiene una definición de configuración de dirección IP de la interfaz de red. |
|/publicIPAddresses/read|Obtiene una definición de la dirección ip pública.|
|/publicIPAddresses/write|Crea una dirección Ip pública o actualiza una que ya existe. |
|/publicIPAddresses/delete|Elimina una dirección IP pública.|
|/publicIPAddresses/join/action|Se une a una dirección IP pública|
|/routeFilters/read|Obtiene una definición de filtro de rutas|
|/routeFilters/join/action|Se une a un filtro de ruta|
|/routeFilters/delete|Elimina una definición de filtro de rutas|
|/routeFilters/write|Crea un filtro de rutas o actualiza uno que ya existe|
|/routeFilters/rules/read|Obtiene una definición de regla de filtro de rutas|
|/routeFilters/rules/write|Crea una regla de filtro de rutas o actualiza una que ya existe|
|/routeFilters/rules/delete|Elimina una definición de regla de filtro de rutas|
|/networkWatchers/read|Obtener la definición de Monitor de red de Hola|
|/networkWatchers/write|Crea una instancia de Network Watcher o actualiza una que ya existe|
|/networkWatchers/delete|Elimina una instancia de Network Watcher|
|/networkWatchers/configureFlowLog/action|Configura el registro de flujos para un recurso de destino.|
|/networkWatchers/ipFlowVerify/action|Devuelve si los paquetes de saludo se permitirá o denegará tooor de un destino determinado.|
|/networkWatchers/nextHop/action|Para un destino especificado y la dirección IP de destino, devolver el tipo de próximo salto hello y esperar a continuación la dirección IP.|
|/networkWatchers/queryFlowLogStatus/action|Obtiene el estado de saludo del flujo de registro en un recurso.|
|/networkWatchers/queryTroubleshootResult/action|Obtiene Hola resultado de hello que ya se ejecutó o está ejecutando la solución de problemas de funcionamiento de la solución de problemas.|
|/networkWatchers/securityGroupView/action|Ver Hola configurado y reglas del grupo de seguridad de red eficaz aplicadas en una máquina virtual.|
|/networkWatchers/topology/action|Obtiene una vista de nivel de red de los recursos y sus relaciones en un grupo de recursos.|
|/networkWatchers/troubleshoot/action|Inicia la solución de problemas en un recurso de redes de Azure.|
|/networkWatchers/packetCaptures/queryStatus/action|Obtiene información acerca de las propiedades y el estado de un recurso de captura de paquetes.|
|/networkWatchers/packetCaptures/stop/action|Detener Hola ejecutando la sesión de captura de paquetes.|
|/networkWatchers/packetCaptures/read|Obtener la definición de captura de paquetes de Hola|
|/networkWatchers/packetCaptures/write|Crea una captura de paquetes|
|/networkWatchers/packetCaptures/delete|Elimina una captura de paquetes|
|/loadBalancers/read|Obtiene una definición del equilibrador de carga|
|/loadBalancers/write|Crea un equilibrador de carga o actualiza uno que ya existe|
|/loadBalancers/delete|Elimina un equilibrador de carga|
|/loadBalancers/networkInterfaces/read|Obtiene las referencias de interfaces de red de hello tooall en un equilibrador de carga|
|/loadBalancers/loadBalancingRules/read|Obtiene una definición de regla de equilibrado de carga del equilibrador de carga|
|/loadBalancers/backendAddressPools/read|Obtiene una definición de grupo de direcciones de back-end del equilibrador de carga|
|/loadBalancers/backendAddressPools/join/action|Se une a un grupo de direcciones de back-end del equilibrador de carga|
|/loadBalancers/inboundNatPools/read|Obtiene una definición de conjuntos NAT de entrada del equilibrador de carga|
|/loadBalancers/inboundNatPools/join/action|Se une a conjuntos NAT de entrada del equilibrador de carga|
|/loadBalancers/inboundNatRules/read|Obtiene una definición de reglas NAT de entrada del equilibrador de carga|
|/loadBalancers/inboundNatRules/write|Crea una regla NAT de entrada del equilibrador de carga o actualiza una que ya existe|
|/loadBalancers/inboundNatRules/delete|Elimina una regla NAT de entrada del equilibrador de carga|
|/loadBalancers/inboundNatRules/join/action|Se une a una regla NAT de entrada del equilibrador de carga|
|/loadBalancers/outboundNatRules/read|Obtiene una definición de reglas NAT de salida del equilibrador de carga|
|/loadBalancers/probes/read|Obtiene un sondeo del equilibrador de carga|
|/loadBalancers/virtualMachines/read|Obtiene referencias tooall Hola máquinas en un equilibrador de carga|
|/loadBalancers/frontendIPConfigurations/read|Obtiene una definición de configuración de dirección IP de front-end del equilibrador de carga|
|/trafficManagerGeographicHierarchies/read|Obtiene Hola Traffic Manager geográfico jerarquía que contiene áreas que se pueden usar con hello método de enrutamiento de tráfico geográfica|
|/bgpServiceCommunities/read|Obtiene las comunidades de servicio de BGP|
|/applicationGatewayAvailableWafRuleSets/read|Obtiene los conjuntos de reglas WAF disponibles en Application Gateway|
|/virtualNetworks/read|Obtener la definición de red virtual de Hola|
|/virtualNetworks/write|Crea una red virtual o actualiza una que ya existe|
|/virtualNetworks/delete|Elimina una red virtual|
|/virtualNetworks/peer/action|Empareja una red virtual con otra red virtual|
|/virtualNetworks/virtualNetworkPeerings/read|Obtiene una definición de emparejamiento de redes virtuales|
|/virtualNetworks/virtualNetworkPeerings/write|Crea un emparejamiento de redes virtuales o actualiza uno que ya existe|
|/virtualNetworks/virtualNetworkPeerings/delete|Elimina un emparejamiento de redes virtuales|
|/virtualNetworks/subnets/read|Obtiene una definición de subred de red virtual|
|/virtualNetworks/subnets/write|Crea una subred de red virtual o actualiza una que ya existe|
|/virtualNetworks/subnets/delete|Elimina una subred de red virtual|
|/virtualNetworks/subnets/join/action|Se une a una red virtual|
|/virtualNetworks/subnets/joinViaServiceTunnel/action|Se une a recursos como cuenta de almacenamiento o SQL tooa servicio activado el túnel subred la base de datos.|
|/virtualNetworks/subnets/virtualMachines/read|Obtiene referencias máquinas virtuales de tooall hello en una subred de red virtual|
|/virtualNetworks/checkIpAddressAvailability/read|Compruebe si la dirección Ip está disponible en la red virtual especificado de Hola|
|/virtualNetworks/virtualMachines/read|Obtiene referencias máquinas virtuales de tooall hello en una red virtual|
|/expressRouteServiceProviders/read|Obtiene los proveedores de servicios de ExpressRoute|
|/dnsoperationresults/read|Obtiene los resultados de una operación DNS|
|/localnetworkgateways/read|Obtiene LocalNetworkGateway|
|/localnetworkgateways/write|Crea o actualiza una LocalNetworkGateway existente|
|/localnetworkgateways/delete|Elimina LocalNetworkGateway|
|/trafficManagerProfiles/read|Obtiene la configuración de perfil de Traffic Manager de Hola. Esto incluye la configuración DNS, configuración de enrutamiento de tráfico, configuración de supervisión de extremo y lista de Hola de extremos enrutados por este perfil de Traffic Manager.|
|/trafficManagerProfiles/write|Crear un perfil de Traffic Manager, o modificar la configuración de Hola de un perfil de Traffic Manager existente Esto incluye la habilitación o deshabilitación de un perfil y la modificación de la configuración de DNS, la de enrutamiento de tráfico o la de supervisión de puntos de conexión. Los extremos enrutados por perfil de Traffic Manager Hola pueden agregar, quitar, habilitados o deshabilitados.|
|/trafficManagerProfiles/delete|Eliminar perfil de Traffic Manager Hola. Se perderán todos los valores asociados con el perfil de Traffic Manager de Hola y Hola perfil ya no se puede usar tooroute tráfico.|
|/dnsoperationstatuses/read|Obtiene el estado de una operación DNS |
|/operations/read|Obtiene las operaciones disponibles|
|/expressRouteCircuits/read|Obtiene un ExpressRouteCircuit|
|/expressRouteCircuits/write|Crea o actualiza un ExpressRouteCircuit existente|
|/expressRouteCircuits/delete|Elimina un ExpressRouteCircuit|
|/expressRouteCircuits/stats/read|Obtiene un estado de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/read|Obtiene un emparejamiento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/write|Crea o actualiza un emparejamiento de ExpressRouteCircuit existente|
|/expressRouteCircuits/peerings/delete|Elimina un emparejamiento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/arpTables/action|Obtiene un ArpTable de emparejamiento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/routeTables/action|Obtiene un RouteTable de emparejamiento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/<br>routeTablesSummary/action|Obtiene un resumen de RouteTable de emparejamiento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/stats/read|Obtiene estadísticas de emparejamiento de ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/read|Obtiene una autorización de ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/write|Crea o actualiza una autorización de ExpressRouteCircuit existente|
|/expressRouteCircuits/authorizations/delete|Elimina una autorización de ExpressRouteCircuit|
|/connections/read|Obtiene VirtualNetworkGatewayConnection|
|/connections/write|Crea o actualiza una VirtualNetworkGatewayConnection existente|
|/connections/delete|Elimina VirtualNetworkGatewayConnection|
|/connections/sharedKey/read|Obtiene el valor de SharedKey de VirtualNetworkGatewayConnection|
|/connections/sharedKey/write|Crea o actualiza una SharedKey de VirtualNetworkGatewayConnection existente|
|/networkSecurityGroups/read|Obtiene una definición de grupo de seguridad de red|
|/networkSecurityGroups/write|Crea un grupo de seguridad de red o actualiza uno que ya existe|
|/networkSecurityGroups/delete|Elimina un grupo de seguridad de red|
|/networkSecurityGroups/join/action|Se une a un grupo de seguridad de red|
|/networkSecurityGroups/defaultSecurityRules/read|Obtiene una definición de regla de seguridad predeterminada|
|/networkSecurityGroups/securityRules/read|Obtiene una definición de regla de seguridad|
|/networkSecurityGroups/securityRules/write|Crea una regla de seguridad o actualiza una que ya existe|
|/networkSecurityGroups/securityRules/delete|Elimina una regla de seguridad|
|/applicationGateways/read|Obtiene una instancia de Application Gateway|
|/applicationGateways/write|Crea una instancia de Application Gateway o actualiza una que ya existe|
|/applicationGateways/delete|Elimina una instancia de Application Gateway|
|/applicationGateways/backendhealth/action|Obtiene el estado de back-end de una instancia de Application Gateway|
|/applicationGateways/start/action|Inicia una instancia de Application Gateway|
|/applicationGateways/stop/action|Detiene una instancia de Application Gateway|
|/applicationGateways/backendAddressPools/join/action|Se une a un grupo de direcciones de back-end de Application Gateway|
|/routeTables/read|Obtiene una definición de tabla de rutas|
|/routeTables/write|Crea una tabla de rutas o actualiza una que ya existe|
|/routeTables/delete|Elimina una definición de tabla de rutas|
|/routeTables/join/action|Se une a una tabla de rutas|
|/routeTables/routes/read|Obtiene una definición de rutas|
|/routeTables/routes/write|Crea una ruta o actualiza una que ya existe|
|/routeTables/routes/delete|Elimina una definición de rutas|
|/locations/operationResults/read|Obtiene el resultado de una operación POST o DELETE asincrónica|
|/locations/checkDnsNameAvailability/read|Comprueba si la etiqueta dns está disponible en hello ubicación especificada|
|/locations/usages/read|Obtiene las métricas de uso de recursos de Hola|
|/locations/operations/read|Obtiene el recurso de operaciones que representa el estado de una operación asincrónica|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de Notificationhubs de Hola y permite la creación de hello de espacios de nombres y NotificationHubs|
|/CheckNamespaceAvailability/action|Comprueba si o no un nombre de recurso Namespace determinado está disponible dentro de hello servicio NotificationHub.|
|/Namespaces/write|Crea un recurso de espacio de nombres y actualiza sus propiedades. Etiquetas y el estado del programa Hola Namespace son propiedades de Hola que se pueden actualizar.|
|/Namespaces/read|Obtener lista de Hola de descripción del recurso Namespace|
|/Namespaces/Delete|Elimina el recurso del espacio de nombres|
|/Namespaces/authorizationRules/action|Obtener lista de Hola de descripción de las reglas de autorización de espacios de nombres.|
|/Namespaces/CheckNotificationHubAvailability/action|Comprueba si un nombre de NotificationHub determinado está disponible dentro de un espacio de nombres.|
|/Namespaces/authorizationRules/write|Crea reglas de autorización en el nivel del espacio de nombres y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/Namespaces/authorizationRules/read|Obtener lista de Hola de descripción de las reglas de autorización de espacios de nombres.|
|/Namespaces/authorizationRules/delete|Elimina la regla de autorización del espacio de nombres. Hola regla de autorización de Namespace predeterminada no se puede eliminar. |
|/Namespaces/authorizationRules/listkeys/action|Obtener la cadena de conexión de hello toohello Namespace|
|/Namespaces/authorizationRules/regenerateKeys/action|Vuelve a generar Namespace autorización regla regenerar principal/clave secundaria, especifique Hola clave que necesita toobe|
|/Namespaces/NotificationHubs/write|Crea un Centro de notificaciones y actualiza sus propiedades. Sus propiedades incluyen principalmente las credenciales PNS. Reglas de autorización y TTL|
|/Namespaces/NotificationHubs/read|Obtiene una lista de descripciones de recursos del Centro de notificaciones|
|/Namespaces/NotificationHubs/Delete|Elimina un recurso del Centro de notificaciones|
|/Namespaces/NotificationHubs/authorizationRules/action|Obtener lista de Hola de reglas de autorización del centro de notificaciones|
|/Namespaces/NotificationHubs/pnsCredentials/action|Obtiene todas las credenciales PNS del Centro de notificaciones. Esto incluye las credenciales WNS, MPNS, APNS, GCM y Baidu|
|/Namespaces/NotificationHubs/debugSend/action|Envía una notificación de inserción de prueba.|
|/Namespaces/NotificationHubs/metricDefinitions/read|Obtiene una lista de descripciones de recursos de métricas del espacio de nombres|
|/Namespaces/NotificationHubs/<br>authorizationRules/write|Crea reglas de autorización del Centro de notificaciones y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/Namespaces/NotificationHubs/<br>authorizationRules/read|Obtener lista de Hola de reglas de autorización del centro de notificaciones|
|/Namespaces/NotificationHubs/<br>authorizationRules/delete|Elimina las reglas de autorización del Centro de notificaciones|
|/Namespaces/NotificationHubs/<br>authorizationRules/listkeys/action|Obtener la cadena de conexión de hello toohello centro de notificaciones|
|/Namespaces/NotificationHubs/<br>authorizationRules/regenerateKeys/action|Vuelve a generar notificación concentrador autorización regla regenerar principal/clave secundaria, especifique Hola clave que necesita toobe|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Operación | Descripción |
|---|---|
|/register/action|Registrar un proveedor de recursos de tooa de suscripción.|
|/linkTargets/read|Enumera las cuentas existentes que no están asociadas a una suscripción de Azure. toolink esta área de trabajo de tooa de suscripción de Azure, use un identificador de cliente devuelto por esta operación en la propiedad de Id. de cliente hello de hello operación Crear área de trabajo.|
|/workspaces/write|Crea una nueva área de trabajo o el área de trabajo existente de vínculos tooan proporcionando Hola Id. de cliente desde el área de trabajo existente de Hola.|
|/workspaces/read|Obtiene un área de trabajo existente|
|/workspaces/delete|Elimina un área de trabajo. Si se vinculó el área de trabajo de hello tooan área de trabajo existente en el momento de creación, a continuación, Hola estaba vinculado toois no elimina del área de trabajo.|
|/workspaces/generateregistrationcertificate/action|Genera el certificado de registro para el área de trabajo de Hola. Este certificado es el área de trabajo de tooconnect usa Microsoft System Center Operation Manager toohello.|
|/workspaces/sharedKeys/action|Recupera claves Hola compartido para el área de trabajo de Hola. Estas claves son tooconnect usa visión operativa de Microsoft agentes toohello área de trabajo.|
|/workspaces/search/action|Ejecuta una consulta de búsqueda|
|/workspaces/datasources/read|Obtiene los orígenes de datos en un área de trabajo.|
|/workspaces/datasources/write|Crea o actualiza los orígenes de datos en un área de trabajo.|
|/workspaces/datasources/delete|Elimina los orígenes de datos en un área de trabajo.|
|/workspaces/managementGroups/read|Obtiene los nombres de Hola y metadatos para el área de trabajo toothis conectado grupos de administración de System Center Operations Manager.|
|/workspaces/schema/read|Obtiene el esquema de búsqueda de hello para el área de trabajo de Hola.  Esquema de la búsqueda incluye Hola expuesta campos y sus tipos.|
|/workspaces/usages/read|Obtiene los datos de uso para un área de trabajo incluida Hola cantidad de datos leídos por área de trabajo de Hola.|
|/workspaces/intelligencepacks/read|Enumera todos los módulos de inteligencia que están visibles para un área de trabajo determinado y también muestra si el módulo de hello está habilitado o deshabilitado para esa área de trabajo.|
|/workspaces/intelligencepacks/enable/action|Habilita un Intelligence Pack para un área de trabajo determinado.|
|/workspaces/intelligencepacks/disable/action|Deshabilita un Intelligence Pack para un área de trabajo determinado.|
|/workspaces/sharedKeys/read|Recupera claves Hola compartido para el área de trabajo de Hola. Estas claves son tooconnect usa visión operativa de Microsoft agentes toohello área de trabajo.|
|/workspaces/savedSearches/read|Obtiene una consulta de búsqueda guardada|
|/workspaces/savedSearches/write|Crea una consulta de búsqueda guardada|
|/workspaces/savedSearches/delete|Elimina una consulta de búsqueda guardada|
|/workspaces/storageinsightconfigs/write|Crea una nueva configuración de almacenamiento. Estas configuraciones son datos de uso toopull desde una ubicación de una cuenta de almacenamiento existente.|
|/workspaces/storageinsightconfigs/read|Obtiene una configuración de almacenamiento.|
|/workspaces/storageinsightconfigs/delete|Elimina una configuración de almacenamiento. Esto detendrá visión operativa de Microsoft pueda leer los datos de cuenta de almacenamiento de Hola.|
|/workspaces/configurationScopes/read|Obtiene el ámbito de configuración|
|/workspaces/configurationScopes/write|Establece el ámbito de configuración|
|/workspaces/configurationScopes/delete|Elimina el ámbito de configuración|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Operación | Descripción |
|---|---|
|/register/action|Registrar un proveedor de recursos de tooa de suscripción.|
|/solutions/write|Crea una nueva solución OMS|
|/solutions/read|Obtiene una solución OMS ya existente|
|/solutions/delete|Elimina una solución OMS ya existente|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Operación | Descripción |
|---|---|
|/Vaults/backupJobsExport/action|Exporta trabajos|
|/Vaults/write|La operación Create Vault crea un recurso de Azure del tipo "almacén"|
|/Vaults/read|Hola operación obtener almacén Obtiene un objeto que representa el recurso de Azure del tipo "almacén" hello|
|/Vaults/delete|Hola eliminar almacén operación eliminaciones Hola especifica el recurso de Azure del tipo "almacén"|
|/Vaults/refreshContainers/read|Actualiza la lista de contenedores de Hola|
|/Vaults/backupJobsExport/operationResults/read|Hola devuelve resultados de la operación de trabajo de exportación.|
|/Vaults/backupOperationResults/read|Devuelve el resultado de la operación de Backup para el almacén de Recovery Services.|
|/Vaults/monitoringAlerts/read|Obtiene las alertas de hello para el almacén de servicios de recuperación de Hola.|
|/Vaults/monitoringAlerts/{uniqueAlertId}/read|Obtiene los detalles de Hola de alerta de Hola.|
|/Vaults/backupSecurityPIN/read|Devuelve la información del PIN de seguridad del almacén de Recovery Services.|
|/vaults/replicationEvents/read|Lee todos los eventos|
|/Vaults/backupProtectableItems/read|Devuelve una lista de todos los elementos que se pueden proteger.|
|/vaults/replicationFabrics/read|Lee todos los tejidos|
|/vaults/replicationFabrics/write|Crea o actualiza todos los tejidos|
|/vaults/replicationFabrics/remove/action|Quita el tejido|
|/vaults/replicationFabrics/checkConsistency/action|Comprobaciones de coherencia de hello tejido|
|/vaults/replicationFabrics/delete|Elimina todos los tejidos|
|/vaults/replicationFabrics/renewcertificate/action||
|/vaults/replicationFabrics/deployProcessServerImage/action|Implementa la imagen del servidor de proceso|
|/vaults/replicationFabrics/reassociateGateway/action|Vuelve a asociar la puerta de enlace|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>read|Lee todos los proveedores de Recovery Services|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>remove/action|Quita los proveedores de Recovery Services|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>delete|Elimina todos los proveedores de Recovery Services|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>refreshProvider/action|Actualiza el proveedor|
|/vaults/replicationFabrics/replicationStorageClassifications/read|Lee todas las clasificaciones de almacenamiento|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/read|Lee todas las asignaciones de clasificaciones de almacenamiento|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/write|Crea o actualiza todas las asignaciones de clasificaciones de almacenamiento|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/delete|Elimina todas las asignaciones de clasificaciones de almacenamiento|
|/vaults/replicationFabrics/replicationvCenters/read|Lee todos los trabajos|
|/vaults/replicationFabrics/replicationvCenters/write|Crea o actualiza todos los trabajos|
|/vaults/replicationFabrics/replicationvCenters/delete|Elimina todos los trabajos|
|/vaults/replicationFabrics/replicationNetworks/read|Lee todas las redes|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/read|Lee todas las asignaciones de redes|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/write|Crea o actualiza todas las asignaciones de redes|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/delete|Elimina todas las asignaciones de redes|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>read|Lee todos los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>discoverProtectableItem/action|Detecta los elementos que se pueden proteger|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>write|Crea o actualiza todos los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>remove/action|Elimina los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>switchprotection/action|Cambia los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectableItems/read|Lee todos los elementos que se pueden proteger|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/read|Lee todas las asignaciones de los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/write|Crea o actualiza todas las asignaciones de los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/remove/action|Quita las asignaciones de los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/delete|Elimina todas las asignaciones de los contenedores de protección|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/read|Lee todos los elementos protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/write|Crea o actualiza todos los elementos protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/delete|Elimina todos los elementos protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/remove/action|Quita los elementos protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/plannedFailover/action|Conmutación por error planeada|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/unplannedFailover/action|Conmutación por error|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailover/action|Test Failover|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailoverCleanup/action|Prueba la limpieza de la conmutación por error|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/failoverCommit/action|Confirma la conmutación por error|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/reProtect/action|Vuelva a proteger el elemento protegido|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/updateMobilityService/action|Actualiza Mobility Service|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/repairReplication/action|Repara una replicación|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/applyRecoveryPoint/action|Aplica un punto de recuperación|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/recoveryPoints/read|Lee los puntos de recuperación de todas las replicaciones|
|/vaults/replicationPolicies/read|Lee todas las directivas|
|/vaults/replicationPolicies/write|Crea o actualiza todas las directivas|
|/vaults/replicationPolicies/delete|Elimina todas las directivas|
|/vaults/replicationRecoveryPlans/read|Lee todos los planes de recuperación|
|/vaults/replicationRecoveryPlans/write|Crea o actualiza todos los planes de recuperación|
|/vaults/replicationRecoveryPlans/delete|Elimina todos los planes de recuperación|
|/vaults/replicationRecoveryPlans/plannedFailover/action|Plan de recuperación de conmutación por error planeado|
|/vaults/replicationRecoveryPlans/unplannedFailover/action|Plan de recuperación de conmutación por error|
|/vaults/replicationRecoveryPlans/testFailover/action|Prueba el plan de recuperación de conmutación por error|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/action|Prueba el plan de recuperación de limpieza de la conmutación por error|
|/vaults/replicationRecoveryPlans/failoverCommit/action|Plan de recuperación de confirmación de la conmutación por error|
|/vaults/replicationRecoveryPlans/reProtect/action|Vuelve a proteger el plan de recuperación|
|/Vaults/extendedInformation/read|¿Hola operación obtener información ampliada obtiene información ampliada de un objeto que representa el recurso de Azure del tipo hello? almacén?|
|/Vaults/extendedInformation/write|¿Hola operación obtener información ampliada obtiene información ampliada de un objeto que representa el recurso de Azure del tipo hello? almacén?|
|/Vaults/extendedInformation/delete|¿Hola operación obtener información ampliada obtiene información ampliada de un objeto que representa el recurso de Azure del tipo hello? almacén?|
|/Vaults/backupManagementMetaData/read|Devuelve los metadatos de administración de Backup para el almacén de Recovery Services.|
|/Vaults/backupProtectionContainers/read|Devuelve todos los contenedores que pertenecen toohello suscripción|
|/Vaults/backupFabrics/operationResults/read|Devuelve el estado de operación de Hola|
|/Vaults/backupFabrics/protectionContainers/read|Devuelve todos los contenedores registrados|
|/Vaults/backupFabrics/protectionContainers/<br>operationResults/read|Obtiene los resultados de la operación realizada en el contenedor de protección.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/read|Devuelve un objeto detalles de hello elemento protegido|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/write|Crea un elemento protegido de copia de seguridad|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/delete|Elimina los elementos protegidos|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/backup/action|Hace una copia de seguridad del elemento protegido.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationResults/read|Obtiene el resultado de la operación realizada en los elementos protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationStatus/read|Devuelve el estado de Hola de operación realizada en elementos protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/read|Obtiene los puntos de recuperación de los elementos protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>restore/action|Restaura los puntos de recuperación de los elementos protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>provisionInstantItemRecovery/action|Aprovisiona una recuperación de elementos instantánea para los elementos protegidos|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>revokeInstantItemRecovery/action|Revoca la recuperación de elementos instantánea para los elementos protegidos|
|/Vaults/usages/read|Devuelve los detalles de uso de un almacén de Recovery Services.|
|/vaults/usages/read|Lee todos los usos de almacén|
|/Vaults/certificates/write|Hola operación actualizar certificado de recursos actualiza el certificado de credencial de recursos o almacenes de Hola.|
|/Vaults/tokenInfo/read|Devuelve la información del token del almacén de Recovery Services.|
|/vaults/replicationAlertSettings/read|Lee la configuración de todas las alertas|
|/vaults/replicationAlertSettings/write|Crea o actualiza la configuración de todas las alertas|
|/Vaults/backupOperations/read|Devuelve el estado de la operación de Backup para el almacén de Recovery Services.|
|/Vaults/storageConfig/read|Devuelve la configuración de almacenamiento del almacén de Recovery Services.|
|/Vaults/storageConfig/write|Actualiza la configuración de almacenamiento del almacén de Recovery Services.|
|/Vaults/backupUsageSummaries/read|Devuelve resúmenes de los elementos y servidores protegidos para un almacén de Recovery Services.|
|/Vaults/backupProtectedItems/read|Devuelve una lista Hola de todos los elementos protegidos.|
|/Vaults/backupconfig/vaultconfig/read|Devuelve la configuración del almacén de Recovery Services.|
|/Vaults/backupconfig/vaultconfig/write|Actualiza la configuración del almacén de Recovery Services.|
|/Vaults/registeredIdentities/write|Hola operación registrar contenedor de servicios puede ser utilizado tooregister un contenedor con el servicio de recuperación.|
|/Vaults/registeredIdentities/read|Hola obtener contenedores se puede utilizar la operación obtener contenedores de hello registrados para un recurso.|
|/Vaults/registeredIdentities/delete|Hola operación anular el registro del contenedor puede ser usado toounregister un contenedor.|
|/Vaults/registeredIdentities/operationResults/read|Hola operación obtener resultados de operación se pueden usar para obtener estado de la operación de Hola y forma asincrónica como resultado de hello envió operación|
|/vaults/replicationJobs/read|Lee todos los trabajos|
|/vaults/replicationJobs/cancel/action|Cancela un trabajo|
|/vaults/replicationJobs/restart/action|Reinicia un trabajo|
|/vaults/replicationJobs/resume/action|Reanuda un trabajo|
|/Vaults/backupPolicies/read|Devuelve todas las directivas de protección|
|/Vaults/backupPolicies/write|Crea una directiva de protección|
|/Vaults/backupPolicies/delete|Elimina una directiva de protección|
|/Vaults/backupPolicies/operationResults/read|Obtiene los resultados de la operación de directiva.|
|/Vaults/backupPolicies/operationStatus/read|Obtiene el estado de la operación de directiva.|
|/Vaults/vaultTokens/read|Hola operación Token de almacén puede ser usado tooget de Token de almacén para las operaciones de nivel de back-end del almacén.|
|/Vaults/monitoringConfigurations/notificationConfiguration/read|Obtiene la configuración de notificación de almacén de servicios de recuperación de Hola.|
|/Vaults/backupJobs/read|Devuelve todos los objetos de trabajo|
|/Vaults/backupJobs/cancel/action|Hola Cancelar trabajo|
|/Vaults/backupJobs/operationResults/read|Hola devuelve resultados de la operación de trabajo.|
|/locations/allocateStamp/action|AllocateStamp es una operación interna que el servicio usa|
|/locations/allocatedStamp/read|GetAllocatedStamp es una operación interna que el servicio usa|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Operación | Descripción |
|---|---|
|/checkNamespaceAvailability/action|Comprueba la disponibilidad del espacio de nombres en una suscripción dada.|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de retransmisión de Hola y permite la creación de hello de recursos de retransmisión|
|/namespaces/write|Crea un recurso de espacio de nombres y actualiza sus propiedades. Etiquetas y el estado del programa Hola Namespace son propiedades de Hola que se pueden actualizar.|
|/namespaces/read|Obtener lista de Hola de descripción del recurso Namespace|
|/namespaces/Delete|Elimina el recurso del espacio de nombres|
|/namespaces/authorizationRules/write|Crea reglas de autorización en el nivel del espacio de nombres y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/authorizationRules/delete|Elimina la regla de autorización del espacio de nombres. Hola regla de autorización de Namespace predeterminada no se puede eliminar. |
|/namespaces/authorizationRules/listkeys/action|Obtener la cadena de conexión de hello toohello Namespace|
|/namespaces/HybridConnections/write|Crea o actualiza las propiedades de HybridConnection.|
|/namespaces/HybridConnections/read|Obtiene una lista de descripciones de recursos de HybridConnection|
|/namespaces/HybridConnections/Delete|Operación toodelete HybridConnection recursos|
|/namespaces/HybridConnections/authorizationRules/write|Crea reglas de autorización de HybridConnection y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/HybridConnections/authorizationRules/delete|Operación toodelete HybridConnection las reglas de autorización|
|/namespaces/HybridConnections/authorizationRules/listkeys/action|Obtener tooHybridConnection de cadena de conexión de Hola|
|/namespaces/WcfRelays/write|Crea o actualiza las propiedades de WcfRelay.|
|/namespaces/WcfRelays/read|Obtiene una lista de descripciones de recursos de WcfRelay|
|/namespaces/WcfRelays/Delete|Operación toodelete WcfRelay recursos|
|/namespaces/WcfRelays/authorizationRules/write|Crea reglas de autorización de WcfRelay y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/WcfRelays/authorizationRules/delete|Operación toodelete WcfRelay las reglas de autorización|
|/namespaces/WcfRelays/authorizationRules/listkeys/action|Obtener tooWcfRelay de cadena de conexión de Hola|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Operación | Descripción |
|---|---|
|/AvailabilityStatuses/read|Estado de disponibilidad de hello obtiene para todos los recursos de hello especifica ámbito|
|/AvailabilityStatuses/current/read|Estado de disponibilidad de hello obtiene para hello recurso específico|

## <a name="microsoftresources"></a>Microsoft.Resources

| Operación | Descripción |
|---|---|
|/checkResourceName/action|Compruebe el nombre de recurso de hello validez.|
|/providers/read|Obtener lista de Hola de proveedores.|
|/subscriptions/read|Obtiene la lista de Hola de suscripciones.|
|/subscriptions/operationresults/read|Obtener suscripción Hola resultados de la operación.|
|/subscriptions/providers/read|Obtiene o enumera los proveedores de recursos.|
|/subscriptions/tagNames/read|Obtiene o enumera las etiquetas de suscripción.|
|/subscriptions/tagNames/write|Agrega una etiqueta de suscripción.|
|/subscriptions/tagNames/delete|Elimina una etiqueta de suscripción.|
|/subscriptions/tagNames/tagValues/read|Obtiene o enumera los valores de las etiquetas de suscripción.|
|/subscriptions/tagNames/tagValues/write|Agrega un valor de etiqueta de suscripción.|
|/subscriptions/tagNames/tagValues/delete|Elimina el valor de una etiqueta de suscripción.|
|/subscriptions/resources/read|Obtiene recursos de una suscripción.|
|/subscriptions/resourceGroups/read|Obtiene o enumera los grupos de recursos.|
|/subscriptions/resourceGroups/write|Crea o actualiza un grupo de recursos.|
|/subscriptions/resourceGroups/delete|Elimina un grupo de recursos y todos sus recursos.|
|/subscriptions/resourceGroups/moveResources/action|Mueve los recursos de tooanother de grupo de recursos.|
|/subscriptions/resourceGroups/validateMoveResources/action|Valida el traslado de recursos de tooanother de grupo de recursos.|
|/subscriptions/resourcegroups/resources/read|Obtiene los recursos de Hola Hola para grupo de recursos.|
|/subscriptions/resourcegroups/deployments/read|Obtiene o enumera implementaciones.|
|/subscriptions/resourcegroups/deployments/write|Crea o actualiza una implementación.|
|/subscriptions/resourcegroups/deployments/operationstatuses/read|Obtiene o enumera los estados de la operación de implementación.|
|/subscriptions/resourcegroups/deployments/operations/read|Obtiene o enumera las operaciones de implementación.|
|/subscriptions/locations/read|Obtiene la lista de Hola de ubicaciones admitidas.|
|/links/read|Obtiene o enumera los vínculos de recursos.|
|/links/write|Crea o actualiza un vínculo de recursos.|
|/links/delete|Elimina un vínculo de recursos.|
|/tenants/read|Obtiene la lista de Hola de inquilinos.|
|/resources/read|Obtener lista de Hola de recursos en función de los filtros.|
|/deployments/read|Obtiene o enumera implementaciones.|
|/deployments/write|Crea o actualiza una implementación.|
|/deployments/delete|Elimina una implementación.|
|/deployments/cancel/action|Cancela una implementación.|
|/deployments/validate/action|Valida una implementación.|
|/deployments/operations/read|Obtiene o enumera las operaciones de implementación.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Operación | Descripción |
|---|---|
|/jobcollections/read|Obtiene una colección de trabajos|
|/jobcollections/write|Crea o actualiza una colección de trabajos.|
|/jobcollections/delete|Elimina una colección de trabajos.|
|/jobcollections/enable/action|Habilita una colección de trabajos.|
|/jobcollections/disable/action|Deshabilita una colección de trabajos.|
|/jobcollections/jobs/read|Obtiene un trabajo.|
|/jobcollections/jobs/write|Crea o actualiza el trabajo.|
|/jobcollections/jobs/delete|Elimina el trabajo.|
|/jobcollections/jobs/run/action|Ejecuta el trabajo.|
|/jobcollections/jobs/generateLogicAppDefinition/action|Genera una definición de Logic Apps basada en un trabajo de Scheduler.|
|/jobcollections/jobs/jobhistories/read|Obtiene el historial de trabajos.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de búsqueda de Hola y permite la creación de hello de servicios de búsqueda.|
|/checkNameAvailability/action|Comprueba la disponibilidad del nombre del servicio Hola.|
|/searchServices/write|Crea o actualiza el servicio de búsqueda de Hola.|
|/searchServices/read|Lee el servicio de búsqueda de Hola.|
|/searchServices/delete|Elimina el servicio de búsqueda de Hola.|
|/searchServices/start/action|Inicia el servicio de búsqueda de Hola.|
|/searchServices/stop/action|Detiene el servicio de búsqueda de Hola.|
|/searchServices/listAdminKeys/action|Lee las claves de administración de Hola.|
|/searchServices/regenerateAdminKey/action|Vuelve a generar clave de administración de Hola.|
|/searchServices/createQueryKey/action|Crea la clave de consulta de Hola.|
|/searchServices/queryKey/read|Lee las claves de consulta de Hola.|
|/searchServices/queryKey/delete|Elimina la clave de consulta de Hola.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Operación | Descripción |
|---|---|
|/jitNetworkAccessPolicies/read|Obtiene las directivas de acceso de red de just-in-time de Hola|
|/jitNetworkAccessPolicies/write|Crea una nueva directiva just-in-time de acceso de red o actualiza una que ya existe|
|/jitNetworkAccessPolicies/initiate/action|Inicia una directiva de acceso de red just-in-time|
|/securitySolutionsReferenceData/read|Obtiene los datos de referencia de las soluciones de seguridad Hola|
|/securityStatuses/read|Obtiene los Estados de mantenimiento de seguridad de Hola para recursos de Azure|
|/webApplicationFirewalls/read|Obtiene los firewalls de aplicación web de Hola|
|/webApplicationFirewalls/write|Crea un nuevo firewall de aplicaciones web o actualiza uno que ya existe|
|/webApplicationFirewalls/delete|Elimina un firewall de aplicaciones web|
|/securitySolutions/read|Obtiene las soluciones de seguridad Hola|
|/securitySolutions/write|Crea una nueva solución de seguridad o actualiza una ya existente|
|/securitySolutions/delete|Elimina una solución de seguridad|
|/tasks/read|Obtiene todas las recomendaciones de seguridad disponibles|
|/tasks/dismiss/action|Descarta una recomendación de seguridad|
|/tasks/activate/action|Activa una recomendación de seguridad|
|/policies/read|Obtiene la directiva de seguridad de Hola|
|/policies/write|Hola de las actualizaciones de directiva de seguridad|
|/applicationWhitelistings/read|Obtiene Hola aplicación whitelistings|
|/applicationWhitelistings/write|Crea una nueva lista de permitidos de la aplicación o actualiza una ya existente|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Operación | Descripción |
|---|---|
|/subscriptions/write|Crea o actualiza una suscripción|
|/gateways/write|Crea o actualiza una puerta de enlace|
|/gateways/delete|Elimina una puerta de enlace|
|/gateways/read|Obtiene una puerta de enlace|
|/gateways/regenerateprofile/action|Vuelve a generar perfiles de la puerta de enlace de Hola|
|/gateways/upgradetolatest/action|Versión más reciente de actualizaciones Hola puerta de enlace toohello|
|/nodes/write|Crea o actualiza un nodo|
|/nodes/delete|Elimina un nodo|
|/nodes/read|Obtiene un nodo|
|/sessions/write|Crea o actualiza una sesión|
|/sessions/read|Obtiene una sesión|
|/sessions/delete|Elimina una sesión|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Operación | Descripción |
|---|---|
|/checkNameAvailability/action|Comprueba la disponibilidad del espacio de nombres en una suscripción dada.|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de bus de servicio de Hola y permite la creación de hello de recursos de ServiceBus|
|/namespaces/write|Crea un recurso de espacio de nombres y actualiza sus propiedades. Etiquetas y el estado del programa Hola Namespace son propiedades de Hola que se pueden actualizar.|
|/namespaces/read|Obtener lista de Hola de descripción del recurso Namespace|
|/namespaces/Delete|Elimina el recurso del espacio de nombres|
|/namespaces/metricDefinitions/read|Obtiene una lista de descripciones de recursos de métricas del espacio de nombres|
|/namespaces/authorizationRules/write|Crea reglas de autorización en el nivel del espacio de nombres y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/authorizationRules/read|Obtener lista de Hola de descripción de las reglas de autorización de espacios de nombres.|
|/namespaces/authorizationRules/delete|Elimina la regla de autorización del espacio de nombres. Hola regla de autorización de Namespace predeterminada no se puede eliminar. |
|/namespaces/authorizationRules/listkeys/action|Obtener la cadena de conexión de hello toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Volver a generar Hola principal o secundario clave toohello recursos|
|/namespaces/diagnosticSettings/read|Obtiene una lista de descripciones de recursos de configuración de diagnósticos del espacio de nombres|
|/namespaces/diagnosticSettings/write|Obtiene una lista de descripciones de recursos de configuración de diagnósticos del espacio de nombres|
|/namespaces/queues/write|Crea o actualiza las propiedades de Queue.|
|/namespaces/queues/read|Obtiene una lista de descripciones de recursos de Queue|
|/namespaces/queues/Delete|Operación toodelete recurso de cola|
|/namespaces/queues/authorizationRules/write|Crea reglas de autorización de Queue y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/queues/authorizationRules/read| Obtener lista de Hola de reglas de autorización de cola|
|/namespaces/queues/authorizationRules/delete|Operación toodelete las reglas de autorización de cola|
|/namespaces/queues/authorizationRules/listkeys/action|Obtener tooQueue de cadena de conexión de Hola|
|/namespaces/queues/authorizationRules/regenerateKeys/action|Volver a generar Hola principal o secundario clave toohello recursos|
|/namespaces/logDefinitions/read|Obtiene una lista de descripciones de recursos de registros del espacio de nombres|
|/namespaces/topics/write|Crea o actualiza las propiedades de tema.|
|/namespaces/topics/read|Obtiene una lista de descripciones de recursos de tema|
|/namespaces/topics/Delete|Operación toodelete recursos de tema|
|/namespaces/topics/authorizationRules/write|Crea reglas de autorización de temas y actualiza sus propiedades. Derechos de acceso de las reglas de autorización de Hello, Hola principales y claves secundarias se pueden actualizar.|
|/namespaces/topics/authorizationRules/read| Obtener lista de Hola de reglas de autorización de tema|
|/namespaces/topics/authorizationRules/delete|Operación toodelete las reglas de autorización de tema|
|/namespaces/topics/authorizationRules/listkeys/action|Obtener tooTopic de cadena de conexión de Hola|
|/namespaces/topics/authorizationRules/regenerateKeys/action|Volver a generar Hola principal o secundario clave toohello recursos|
|/namespaces/topics/subscriptions/write|Crear o actualizar las propiedades de TopicSubscription.|
|/namespaces/topics/subscriptions/read|Obtiene una lista de descripciones de recursos de TopicSubscription|
|/namespaces/topics/subscriptions/Delete|Operación toodelete TopicSubscription recursos|
|/namespaces/topics/subscriptions/rules/write|Crea o actualiza las propiedades de reglas.|
|/namespaces/topics/subscriptions/rules/read|Obtiene una lista de descripciones de recursos de reglas|
|/namespaces/topics/subscriptions/rules/Delete|Operación toodelete recursos de la regla|

## <a name="microsoftsql"></a>Microsoft.Sql

| Operación | Descripción |
|---|---|
|/servers/read|Devuelve una lista de servidores de un grupo de recursos en una suscripción|
|/servers/write|Crea un servidor nuevo o modifica las propiedades del servidor existente en un grupo de recursos de una suscripción|
|/servers/delete|Elimina un servidor y todas las bases de datos y grupos elásticos que contiene|
|/servers/import/action|Crear una nueva base de datos en el servidor de hello e implementar el esquema y los datos de un paquete DacPac|
|/servers/upgrade/action|Habilitar la nueva funcionalidad disponible en la versión más reciente de Hola de servidor y especifique el mapa de conversión de edición de las bases de datos|
|/servers/VulnerabilityAssessmentScans/action|Ejecuta un análisis del servidor de evaluación de vulnerabilidad|
|/servers/operationResults/read|Se utiliza la operación tootrack progreso de actualización del servidor de toohigher de versión inferior|
|/servers/operationResults/delete|Anula la actualización de la versión del servidor en curso|
|/servers/securityAlertPolicies/read|Recuperar los detalles de la directiva de detección de amenazas Hola servidor configurado en un servidor determinado|
|/servers/securityAlertPolicies/write|Hola servidor amenaza para la detección de un servidor determinado de cambios|
|/servers/securityAlertPolicies/operationResults/read|Recuperar resultados de servidor hello operación de establecimiento de directiva de detección de amenazas|
|/servers/administrators/read|Recupera los detalles del administrador del servidor|
|/servers/administrators/write|Crea o actualiza el administrador del servidor|
|/servers/administrators/delete|Eliminar el administrador del servidor del servidor de Hola|
|/servers/recoverableDatabases/read|Esta operación se usa para la recuperación ante desastres en vivo de la base de datos toorestore base de datos conocidos toolast buena copia de seguridad del punto de. Devuelve información acerca de la copia de seguridad buena Hola última pero realmente no restaura base de datos de Hola.|
|/servers/serviceObjectives/read|Recupera la lista de objetivos de nivel de servicio (también conocida como niveles de rendimiento) disponible en un servidor determinado|
|/servers/firewallRules/read|Recupera los detalles de regla de firewall del servidor|
|/servers/firewallRules/write|Crear o actualizar regla de firewall que controla el intervalo de direcciones IP permitida tooconnect toohello server|
|/servers/firewallRules/delete|Eliminar regla de firewall del servidor de Hola|
|/servers/administratorOperationResults/read|Recupera los resultados de la operación del administrador del servidor|
|/servers/recommendedElasticPools/read|Recuperar la recomendación para la base de datos elástica grupos tooreduce costo o mejorar el rendimiento en comparación con la utilización de recursos de historica|
|/servers/recommendedElasticPools/metrics/read|Recupera las métricas para los grupos de bases de datos elásticas recomendados para un servidor determinado|
|/servers/recommendedElasticPools/databases/read|Recupera bases de datos que deben agregarse a grupos de bases de datos elásticas recomendados para un servidor determinado|
|/servers/elasticPools/read|Recupera los detalles del grupo de bases de datos elásticas de un servidor determinado|
|/servers/elasticPools/write|Crea un nuevo grupo de bases de datos elásticas o cambia las propiedades de uno que ya existe|
|/servers/elasticPools/delete|Elimina un grupo de bases de datos elásticas que ya existe|
|/servers/elasticPools/operationResults/read|Recupera los detalles de una operación de un grupo de bases de datos elásticas determinado|
|/servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions/read|Devuelve los tipos de métricas que están disponibles para grupos de bases de datos elásticas|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/read|Obtiene la configuración de diagnóstico de hello para el recurso de Hola|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/write|Crea o actualiza la configuración de diagnóstico de hello para el recurso de Hola|
|/servers/elasticPools/metrics/read|Devuelve las métricas de utilización de recursos de un grupo de bases de datos elásticas|
|/servers/elasticPools/elasticPoolDatabaseActivity/read|Recupera las actividades y detalles de una determinada base de datos que forma parte del grupo de bases de datos elásticas|
|/servers/elasticPools/advisors/read|Devuelve una lista de asesores disponibles para el grupo elástico Hola|
|/servers/elasticPools/advisors/write|Actualiza el estado de ejecución automática de un asesor en el nivel del grupo elástico.|
|/servers/elasticPools/advisors/recommendedActions/read|Devuelve una lista de recomendaciones de advisor especificado para el grupo elástico Hola|
|/servers/elasticPools/advisors/recommendedActions/write|Aplicar Hola acción en el grupo elástico Hola recomendada|
|/servers/elasticPools/elasticPoolActivity/read|Recupera las actividades y detalles de un grupo de bases de datos elásticas determinado|
|/servers/elasticPools/databases/read|Recupera la lista y los detalles de las bases de datos que forman parte de un grupo de bases de datos elásticas de un servidor determinado|
|/servers/auditingPolicies/read|Recuperar detalles de tabla de servidor de hello predeterminada configurada en un servidor determinado de directiva de auditoría|
|/servers/auditingPolicies/write|La tabla de servidor predeterminada Hola auditoría para un servidor determinado de cambios|
|/servers/disasterRecoveryConfiguration/operationResults/read|Obtiene los resultados de la operación de configuración de recuperación ante desastres|
|/servers/advisors/read|Devuelve una lista de asesores disponibles para el servidor de Hola|
|/servers/advisors/write|Actualiza el estado de ejecución automática de un asesor en el nivel del servidor.|
|/servers/advisors/recommendedActions/read|Devuelve una lista de recomendaciones de advisor especificado para el servidor de Hola|
|/servers/advisors/recommendedActions/write|Aplicar Hola acción en el servidor de hello recomendada|
|/servers/usages/read|Devolver la cuota de DTU de servidor y consuption DTU actual por todas las bases de datos de servidor hello|
|/servers/elasticPoolEstimates/read|Devuelve una lista de las estimaciones de grupos elásticos ya creados para este servidor|
|/servers/elasticPoolEstimates/write|Crea una nueva estimación de grupos elásticos para la lista de bases de datos proporcionada|
|/servers/auditingSettings/read|Recuperar los detalles de blob de servidor hello configurado en un servidor determinado de directiva de auditoría|
|/servers/auditingSettings/write|Auditoría de cambio Hola server blob para un servidor determinado|
|/servers/auditingSettings/operationResults/read|Recuperar resultados de blob de servidor hello operación de establecimiento de directivas de auditoría|
|/servers/backupLongTermRetentionVaults/read|Esta operación es tooget usa un almacén de retención de copia de seguridad a largo plazo. Devuelve información acerca de hello almacén registrados toothis server.|
|/servers/backupLongTermRetentionVaults/write|Registra un almacén de retención de copia de seguridad a largo plazo|
|/servers/restorableDroppedDatabases/read|Recupera una lista de bases de datos que se han quitado de un servidor determinado que siguen estando dentro de la directiva de retención. Esta operación devuelve una lista de las bases de datos y sus metadatos asociados, como la fecha de eliminación.|
|/servers/databases/read|Devuelve una lista de servidores de un grupo de recursos en una suscripción|
|/servers/databases/write|Crea un servidor nuevo o modifica las propiedades del servidor existente en un grupo de recursos de una suscripción|
|/servers/databases/delete|Elimina un servidor y todas las bases de datos y grupos elásticos que contiene|
|/servers/databases/export/action|Crear una nueva base de datos en el servidor de hello e implementar el esquema y los datos de un paquete DacPac|
|/servers/databases/VulnerabilityAssessmentScans/action|Ejecuta un análisis de la base datos de evaluación de vulnerabilidad.|
|/servers/databases/pause/action|Pausa una base de datos de edición de DataWarehouse|
|/servers/databases/resume/action|Reanuda una base de datos de edición de DataWarehouse|
|/servers/databases/operationResults/read|Se utiliza la operación tootrack progreso de la operación de base de datos de ejecución prolongada, como escala.|
|/servers/databases/replicationLinks/read|Devuelve detalles acerca de los vínculos de replicación establecidos para una determinada base de datos|
|/servers/databases/replicationLinks/delete|Terminar la relación de replicación de hello forzosamente y con posible pérdida de datos|
|/servers/databases/replicationLinks/unlink/action|Finalizar la relación de replicación de hello forzosamente o después de sincronizar con el asociado de Hola|
|/servers/databases/replicationLinks/failover/action|Conmutación por error después de sincronizar todos los cambios de hello principal, esta base de datos se pasa en principal remoto de la relación de replicación de Hola Hola principal y realizar en una base de datos secundaria|
|/servers/databases/replicationLinks/forceFailoverAllowDataLoss/action|Conmutación por error inmediatamente con posible pérdida de datos, haciendo esta base de datos en remoto de Hola principal y realización de la relación de replicación de hello principal en una base de datos secundaria|
|/servers/databases/replicationLinks/updateReplicationMode/action|Actualiza el modo de replicación para el vínculo toosynchronous o el modo asincrónico|
|/servers/databases/replicationLinks/operationResults/read|Obtiene el estado de operaciones de larga duración en vínculos de replicación de la base de datos|
|/servers/databases/dataMaskingPolicies/read|Recuperar los detalles de directiva configurada en una base de datos de enmascaramiento de datos de Hola|
|/servers/databases/dataMaskingPolicies/write|Cambia la directiva de enmascaramiento de datos de una determinada base de datos|
|/servers/databases/dataMaskingPolicies/rules/read|Recuperar los detalles de regla de directiva configurada en una base de datos de enmascaramiento de datos de Hola|
|/servers/databases/dataMaskingPolicies/rules/write|Cambia la regla de directiva de enmascaramiento de datos de una determinada base de datos|
|/servers/databases/securityAlertPolicies/read|Recuperar los detalles de la directiva de detección de amenazas Hola configurado en una base de datos|
|/servers/databases/securityAlertPolicies/write|Cambiar la directiva de detección de amenazas de Hola de una base de datos|
|/servers/databases/providers/Microsoft.Insights/<br>metricDefinitions/read|Devuelve los tipos de métricas que están disponibles para grupos de bases de datos|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/read|Obtiene la configuración de diagnóstico de hello para el recurso de Hola|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/write|Crea o actualiza la configuración de diagnóstico de hello para el recurso de Hola|
|/servers/databases/providers/Microsoft.Insights/<br>logDefinitions/read|Obtiene los registros disponibles de Hola para las bases de datos|
|/servers/databases/topQueries/read|Devuelve estadísticas agregadas de tiempo de ejecución para la consulta seleccionada en el período de tiempo seleccionado|
|/servers/databases/topQueries/queryText/read|Devuelve el texto de Transact-SQL de hello para el Id. de la consulta seleccionada|
|/servers/databases/topQueries/statistics/read|Devuelve estadísticas agregadas de tiempo de ejecución para la consulta seleccionada en el período de tiempo seleccionado|
|/servers/databases/connectionPolicies/read|Recuperar detalles de directiva de conexión de hello configurado en una base de datos|
|/servers/databases/connectionPolicies/write|Cambia la directiva de conexión para una base de datos determinada|
|/servers/databases/metrics/read|Devuelve las métricas de utilización de recursos de base de datos|
|/servers/databases/auditRecords/read|Recuperar los registros de auditoría de blob de base de datos de Hola|
|/servers/databases/transparentDataEncryption/read|Recupera el estado y los detalles de la característica de seguridad de cifrado de datos transparente para una base de datos determinada|
|/servers/databases/transparentDataEncryption/write|Habilita o deshabilita el cifrado de datos transparente para una base de datos|
|/servers/databases/transparentDataEncryption/operationResults/read|Recupera el estado y los detalles de la característica de seguridad de cifrado de datos transparente para una base de datos determinada|
|/servers/databases/auditingPolicies/read|Recuperar detalles de directiva auditoría en la tabla de hello configurado en una base de datos|
|/servers/databases/auditingPolicies/write|Cambiar la directiva de auditoría de tabla de Hola para una base de datos|
|/servers/databases/dataWarehouseQueries/read|Devuelve información de consulta de distribución en almacenamiento de datos de hello para el Id. de la consulta seleccionada|
|/servers/databases/dataWarehouseQueries/<br>dataWarehouseQuerySteps/read|Hola devuelve distribuidas consultar la información de paso de consulta de almacén de datos para el Id. de paso seleccionado|
|/servers/databases/serviceTierAdvisors/read|Devolver sugerencias acerca de cómo ampliar la base de datos hacia arriba o hacia abajo en función del rendimiento de tooimprove de las estadísticas de ejecución de consulta o reducir los costos|
|/servers/databases/advisors/read|Devuelve una lista de los asesores de base de datos de Hola|
|/servers/databases/advisors/write|Actualiza el estado de ejecución automática de un asesor en el nivel de la base de datos.|
|/servers/databases/advisors/recommendedActions/read|Devuelve una lista de recomendaciones de advisor especificado para la base de datos de Hola|
|/servers/databases/advisors/recommendedActions/write|Aplicar Hola acción en la base de datos de hello recomendada|
|/servers/databases/usages/read|Devuelve el tamaño máximo de la base de datos que se puede alcanzar y el tamaño actual ocupado por los datos|
|/servers/databases/queryStore/read|Devuelve los valores actuales de configuración de almacén de consultas de base de datos de Hola|
|/servers/databases/queryStore/write|Actualiza la configuración de almacén de consultas de base de datos de Hola|
|/servers/databases/auditingSettings/read|Recuperar los detalles de directiva de auditoría de hello blob con un configurado en una base de datos|
|/servers/databases/auditingSettings/write|Cambiar la directiva de auditoría de blob de Hola para una base de datos|
|/servers/databases/schemas/tables/recommendedIndexes/read|Recupera la lista de recomendaciones de índice de una base de datos|
|/servers/databases/schemas/tables/recommendedIndexes/write|Aplica la recomendación de índice|
|/servers/databases/schemas/tables/columns/read|Recuperar la lista de columnas de una tabla|
|/servers/databases/missingindexes/read|Devolver sugerencias sobre toocreate de índices de base de datos, modificar o eliminar en el rendimiento de las consultas tooimprove orden|
|/servers/databases/missingindexes/write|Usa la recomendación de índice de base de datos en una base de datos determinada|
|/servers/databases/importExportOperationResults/read|Devuelve detalles sobre una operación de importación o exportación de base de datos desde un DacPac ubicado en la cuenta de almacenamiento|
|/servers/importExportOperationResults/read|Devolver la lista de hello con detalles de las operaciones de importación de base de datos de cuenta de almacenamiento en un servidor determinado|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Operación | Descripción |
|---|---|
|/register/action|Registra la suscripción de hello para el proveedor de recursos de almacenamiento de Hola y permite la creación de hello de cuentas de almacenamiento.|
|/checknameavailability/read|Comprueba que el nombre de la cuenta es válido y que no está en uso.|
|/storageAccounts/write|Crea una cuenta de almacenamiento con hello especificada parámetros o actualización Hola propiedades o etiquetas o agrega personalizado dominio para hello especifica la cuenta de almacenamiento.|
|/storageAccounts/delete|Agrega una cuenta de almacenamiento existente.|
|/storageAccounts/listkeys/action|Devuelve las teclas de acceso de Hola para hello especifican cuenta de almacenamiento.|
|/storageAccounts/regeneratekey/action|Vuelve a generar claves de acceso de Hola para hello especifican cuenta de almacenamiento.|
|/storageAccounts/read|Devuelve la lista de cuentas de almacenamiento de Hola u obtiene propiedades Hola Hola especifican cuenta de almacenamiento.|
|/storageAccounts/listAccountSas/action|Devuelve el token de SAS de cuenta de hello para hello especifica cuenta de almacenamiento.|
|/storageAccounts/listServiceSas/action|Token SAS del servicio de almacenamiento|
|/storageAccounts/services/diagnosticSettings/write|Crea o actualiza la configuración de diagnóstico de la cuenta de almacenamiento.|
|/skus/read|Listas de hello SKU compatibles con almacenamiento de Microsoft.|
|/usages/read|Devuelve Hola límite y recuento de utilización actual de Hola de recursos de hello especifica suscripción|
|/operations/read|Estado de Hola de sondeos de una operación asincrónica.|
|/locations/deleteVirtualNetworkOrSubnets/action|Notifica a Microsoft.Storage que se está eliminando una red virtual o subred|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Operación | Descripción |
|---|---|
|/managers/clearAlerts/action|Borrar todas las alertas de hello asociadas con el Administrador de dispositivos de Hola.|
|/managers/getActivationKey/action|Obtener la clave de activación para el Administrador de dispositivos de Hola.|
|/managers/regenerateActivationKey/action|Volver a generar la clave de activación para el Administrador de dispositivos de Hola.|
|/managers/regenarateRegistationCertificate/action|Volver a generar el certificado de registro para administradores de dispositivos de Hola.|
|/managers/getEncryptionKey/action|Obtener la clave de cifrado para el Administrador de dispositivos de Hola.|
|/managers/read|Muestra u obtiene Hola administradores de dispositivos|
|/managers/delete|Elimina los administradores de dispositivos de Hola|
|/managers/write|Crear o actualizar los administradores de dispositivos de Hola|
|/managers/configureDevice/action|Configura un dispositivo|
|/managers/listActivationKey/action|Obtiene la clave de activación de Hola de hello Administrador de dispositivos de StorSimple.|
|/managers/listPublicEncryptionKey/action|Enumera las claves de cifrado públicas de un administrador de dispositivos de StorSimple.|
|/managers/listPrivateEncryptionKey/action|Obtiene una clave de cifrado privada de un administrador de dispositivos de StorSimple.|
|/managers/provisionCloudAppliance/action|Crea una nueva aplicación en la nube.|
|/Managers/write|La operación Create Vault crea un recurso de Azure del tipo "almacén"|
|/Managers/read|Hola operación obtener almacén Obtiene un objeto que representa el recurso de Azure del tipo "almacén" hello|
|/Managers/delete|Hola eliminar almacén operación eliminaciones Hola especifica el recurso de Azure del tipo "almacén"|
|/managers/storageAccountCredentials/write|Crear o actualizar las credenciales de cuenta de almacenamiento de Hola|
|/managers/storageAccountCredentials/read|Obtiene las credenciales de cuenta de almacenamiento de Hola o enumera|
|/managers/storageAccountCredentials/delete|Elimina las credenciales de cuenta de almacenamiento de Hola|
|/managers/storageAccountCredentials/listAccessKey/action|Muestra las claves de acceso de las credenciales de la cuenta de almacenamiento|
|/managers/accessControlRecords/read|Obtiene los registros de Control de acceso de Hola o enumera|
|/managers/accessControlRecords/write|Crear o actualizar los registros de Control de acceso de Hola|
|/managers/accessControlRecords/delete|Elimina los registros de Control de acceso de Hola|
|/managers/metrics/read|Muestra u obtiene las métricas de Hola|
|/managers/bandwidthSettings/read|Lista de opciones de ancho de banda de hello (sólo serie 8000)|
|/managers/bandwidthSettings/write|Crea una nueva configuración de ancho de banda (solo serie 8000) o actualiza la que ya existe|
|/managers/bandwidthSettings/delete|Elimina una configuración de ancho de banda (solo serie 8000) que ya existe|
|/Managers/extendedInformation/read|¿Hola operación obtener información ampliada obtiene información ampliada de un objeto que representa el recurso de Azure del tipo hello? almacén?|
|/Managers/extendedInformation/write|¿Hola operación obtener información ampliada obtiene información ampliada de un objeto que representa el recurso de Azure del tipo hello? almacén?|
|/Managers/extendedInformation/delete|¿Hola operación obtener información ampliada obtiene información ampliada de un objeto que representa el recurso de Azure del tipo hello? almacén?|
|/managers/alerts/read|Obtiene las alertas de Hola o muestra|
|/managers/storageDomains/read|Muestra u obtiene Hola dominios de almacenamiento|
|/managers/storageDomains/write|Crear o actualizar los dominios de almacenamiento de Hola|
|/managers/storageDomains/delete|Elimina los dominios de almacenamiento de Hola|
|/managers/devices/scanForUpdates/action|Busca actualizaciones de un dispositivo.|
|/managers/devices/download/action|Descarga actualizaciones para un dispositivo.|
|/managers/devices/install/action|Instala actualizaciones en un dispositivo.|
|/managers/devices/read|Muestra u obtiene Hola dispositivos|
|/managers/devices/write|Crear o actualizar los dispositivos de Hola|
|/managers/devices/delete|Elimina los dispositivos de Hola|
|/managers/devices/deactivate/action|Desactiva un dispositivo.|
|/managers/devices/publishSupportPackage/action|Publica el paquete de soporte de un dispositivo para la solución de problemas del Soporte técnico de Microsoft.|
|/managers/devices/failover/action|Conmutación por error de dispositivo de Hola.|
|/managers/devices/sendTestAlertEmail/action|Enviar alertas por correo electrónico de prueba tooconfigured destinatarios de correo electrónico.|
|/managers/devices/installUpdates/action|Instala las actualizaciones en dispositivos de Hola|
|/managers/devices/listFailoverSets/action|Conmutación por error de lista Hola se establece en un dispositivo existente.|
|/managers/devices/listFailoverTargets/action|Lista de destinos de conmutación por error de dispositivos de Hola|
|/managers/devices/publicEncryptionKey/action|Clave de cifrado pública de la lista del Administrador de dispositivos de Hola|
|/managers/devices/hardwareComponentGroups/<br>read|Hola de lista grupos de componentes de Hardware|
|/managers/devices/hardwareComponentGroups/<br>changeControllerPowerState/action|Cambia el estado de energía del controlador de los grupos de componentes de hardware|
|/managers/devices/metrics/read|Muestra u obtiene las métricas de Hola|
|/managers/devices/chapSettings/write|Crear o actualizar la configuración de Chap Hola|
|/managers/devices/chapSettings/read|Muestra u Obtiene la configuración de Chap Hola|
|/managers/devices/chapSettings/delete|Elimina la configuración de Chap Hola|
|/managers/devices/backupScheduleGroups/read|Obtiene los grupos de programación de copia de seguridad de Hola o muestra|
|/managers/devices/backupScheduleGroups/write|Crear o actualizar los grupos de programación de copia de seguridad de Hola|
|/managers/devices/backupScheduleGroups/delete|Elimina los grupos de programación de copia de seguridad de Hola|
|/managers/devices/updateSummary/read|Muestra u obtiene Hola resumen de actualización|
|/managers/devices/migrationSourceConfigurations/<br>import/action|Importa las configuraciones de origen para la migración|
|/managers/devices/migrationSourceConfigurations/<br>startMigrationEstimate/action|Inicie una duración de trabajo tooestimate Hola Hola del proceso de migración.|
|/managers/devices/migrationSourceConfigurations/<br>startMigration/action|Inicia la migración mediante configuraciones de origen|
|/managers/devices/migrationSourceConfigurations/<br>confirmMigration/action|Confirma una migración correcta y la confirma.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationEstimate/action|Capturar el estado de hello para el trabajo de estimación de migración de Hola.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationStatus/action|Capturar el estado de hello para la migración de Hola.|
|/managers/devices/migrationSourceConfigurations/<br>fetchConfirmMigrationStatus/action|Hola Fetch confirme el estado de la migración.|
|/managers/devices/alertSettings/read|Enumera u obtiene la configuración de alertas de Hola|
|/managers/devices/alertSettings/write|Crear o actualizar la configuración de alerta de Hola|
|/managers/devices/networkSettings/read|Muestra o se obtiene la configuración de red de Hola|
|/managers/devices/networkSettings/write|Crea una nueva configuración de red o actualiza una que ya existe|
|/managers/devices/jobs/read|Muestra u obtiene Hola trabajos|
|/managers/devices/jobs/cancel/action|Cancela un trabajo de ejecución|
|/managers/devices/metricsDefinitions/read|Obtiene las definiciones de las métricas de Hola o muestra|
|/managers/devices/volumeContainers/write|Crea un nuevo contenedor de volumen (solo para la serie 8000) o actualiza uno que ya existe|
|/managers/devices/volumeContainers/read|Lista de contenedores de volúmenes de hello (sólo serie 8000)|
|/managers/devices/volumeContainers/delete|Elimina los contenedores de volumen existentes (solo para la serie 8000)|
|/managers/devices/volumeContainers/listEncryptionKeys/action|Enumera las claves de cifrado de los contenedores de volumen|
|/managers/devices/volumeContainers/rolloverEncryptionKey/action|Sustituye las claves de cifrado de los contenedores de volumen|
|/managers/devices/volumeContainers/metrics/read|Lista Hola métricas|
|/managers/devices/volumeContainers/volumes/read|Lista Hola volúmenes|
|/managers/devices/volumeContainers/volumes/write|Crea un nuevo volumen o actualiza uno que ya existe|
|/managers/devices/volumeContainers/volumes/delete|Elimina un volumen existente|
|/managers/devices/volumeContainers/volumes/metrics/read|Lista Hola métricas|
|/managers/devices/volumeContainers/volumes/metricsDefinitions/read|Hola lista definiciones de métricas|
|/managers/devices/volumeContainers/metricsDefinitions/read|Hola lista definiciones de métricas|
|/managers/devices/iscsiservers/read|Muestra u obtiene Hola iSCSI servidores|
|/managers/devices/iscsiservers/write|Crear o actualizar Hola iSCSI servidores|
|/managers/devices/iscsiservers/delete|Elimina Hola iSCSI servidores|
|/managers/devices/iscsiservers/backup/action|Realiza una copia de seguridad de un servidor iSCSI.|
|/managers/devices/iscsiservers/metrics/read|Muestra u obtiene las métricas de Hola|
|/managers/devices/iscsiservers/disks/read|Muestra u obtiene Hola discos|
|/managers/devices/iscsiservers/disks/write|Crear o actualizar discos Hola|
|/managers/devices/iscsiservers/disks/delete|Elimina los discos de Hola|
|/managers/devices/iscsiservers/disks/metrics/read|Muestra u obtiene las métricas de Hola|
|/managers/devices/iscsiservers/disks/metricsDefinitions/read|Obtiene las definiciones de las métricas de Hola o muestra|
|/managers/devices/iscsiservers/metricsDefinitions/read|Obtiene las definiciones de las métricas de Hola o muestra|
|/managers/devices/backups/read|Muestra u obtiene Hola de conjunto de copia|
|/managers/devices/backups/delete|Hola de eliminaciones de conjunto de copia|
|/managers/devices/backups/restore/action|Restaurar todos los volúmenes de Hola desde un conjunto de copia de seguridad.|
|/managers/devices/backups/elements/clone/action|Clona un recurso o volumen compartido mediante un elemento de copia de seguridad.|
|/managers/devices/backupPolicies/write|Crea una nueva directiva de copia de seguridad (solo serie 8000) o actualiza una que ya existe|
|/managers/devices/backupPolicies/read|Hola lista las directivas de copia de seguridad (sólo serie 8000)|
|/managers/devices/backupPolicies/delete|Elimina una directiva de copia de seguridad existente (solo serie 8000)|
|/managers/devices/backupPolicies/backup/action|Realizar copia de seguridad de todos los volúmenes de hello protegidos por la política de hello un toocreate de copia de seguridad manual a petición.|
|/managers/devices/backupPolicies/schedules/write|Crea una nueva programación o actualiza una que ya existe|
|/managers/devices/backupPolicies/schedules/read|Lista Hola programaciones|
|/managers/devices/backupPolicies/schedules/delete|Elimina una programación existente|
|/managers/devices/securitySettings/update/action|Actualizar la configuración de seguridad de Hola.|
|/managers/devices/securitySettings/read|Hola de lista Configuración de seguridad|
|/managers/devices/securitySettings/<br>syncRemoteManagementCertificate/action|Sincronizar el certificado de administración remota de Hola para un dispositivo.|
|/managers/devices/securitySettings/write|Crea una nueva configuración de seguridad o actualiza una que ya existe|
|/managers/devices/fileservers/read|Muestra u obtiene Hola File Servers|
|/managers/devices/fileservers/write|Crear o actualizar los servidores de archivos de Hola|
|/managers/devices/fileservers/delete|Elimina los servidores de archivos de Hola|
|/managers/devices/fileservers/backup/action|Realiza una copia de seguridad de un servidor de archivos.|
|/managers/devices/fileservers/metrics/read|Muestra u obtiene las métricas de Hola|
|/managers/devices/fileservers/shares/write|Crear o actualizar los recursos compartidos de Hola|
|/managers/devices/fileservers/shares/read|Muestra u obtiene los recursos compartidos de Hola|
|/managers/devices/fileservers/shares/delete|Elimina los recursos compartidos de Hola|
|/managers/devices/fileservers/shares/metrics/read|Muestra u obtiene las métricas de Hola|
|/managers/devices/fileservers/shares/metricsDefinitions/read|Obtiene las definiciones de las métricas de Hola o muestra|
|/managers/devices/fileservers/metricsDefinitions/read|Obtiene las definiciones de las métricas de Hola o muestra|
|/managers/devices/timeSettings/read|Muestra u Obtiene la configuración de tiempo de Hola|
|/managers/devices/timeSettings/write|Crea una nueva configuración de hora o actualiza una que ya existe|
|/Managers/certificates/write|Hola operación actualizar certificado de recursos actualiza el certificado de credencial de recursos o almacenes de Hola.|
|/managers/cloudApplianceConfigurations/read|Hola lista configuraciones admitidas de dispositivo en la nube|
|/managers/metricsDefinitions/read|Obtiene las definiciones de las métricas de Hola o muestra|
|/managers/encryptionSettings/read|Enumera u obtiene la configuración de cifrado de Hola|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Operación | Descripción |
|---|---|
|/streamingjobs/Start/action|Inicia el trabajo de Stream Analytics|
|/streamingjobs/Stop/action|Detiene el trabajo de Stream Analytics|
|/streamingjobs/Read|Lee el trabajo de Stream Analytics|
|/streamingjobs/Write|Escribe el trabajo de Stream Analytics|
|/streamingjobs/Delete|Elimina el trabajo de Stream Analytics|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/read|Obtiene las métricas disponibles de Hola para streamingjobs|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/read|Lee la configuración de diagnóstico.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/write|Escribe la configuración de diagnóstico.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/read|Obtiene los registros disponibles de Hola para streamingjobs|
|/streamingjobs/transformations/Read|Lee la transformación de trabajos de Stream Analytics|
|/streamingjobs/transformations/Write|Escribe la transformación de trabajos de Stream Analytics|
|/streamingjobs/transformations/Delete|Elimina la transformación de trabajos de Stream Analytics|
|/streamingjobs/inputs/Read|Lee la entrada del trabajo de Stream Analytics|
|/streamingjobs/inputs/Write|Escribe la entrada del trabajo de Stream Analytics|
|/streamingjobs/inputs/Delete|Elimina la entrada del trabajo de Stream Analytics|
|/streamingjobs/outputs/Read|Lee la salida del trabajo de Stream Analytics|
|/streamingjobs/outputs/Write|Escribe la salida del trabajo de Stream Analytics|
|/streamingjobs/outputs/Delete|Elimina la salida del trabajo de Stream Analytics|

## <a name="microsoftsupport"></a>Microsoft.Support

| Operación | Descripción |
|---|---|
|/register/action|Registra el proveedor de recursos tooSupport|
|/supportTickets/read|Obtiene los detalles de la incidencia de soporte técnico (incluido el estado, gravedad, detalles de contacto y las comunicaciones) u obtiene la lista de Hola de incidencias de soporte técnico a través de suscripciones.|
|/supportTickets/write|Crea o actualiza una incidencia de soporte técnico. Puede crear una incidencia de soporte técnico para problemas relacionados con cuestiones técnicas, de facturación, cuotas o de administración de suscripciones. Puede actualizar la gravedad, los detalles de contacto y las comunicaciones de las incidencias de soporte técnico existentes.|

## <a name="microsoftweb"></a>Microsoft.Web

| Operación | Descripción |
|---|---|
|/unregister/action|Anular el registro del proveedor de recursos de Microsoft.Web para la suscripción de Hola.|
|/validate/action|Valida.|
|/register/action|Registrar proveedor de recursos de Microsoft.Web para la suscripción de Hola.|
|/hostingEnvironments/Read|Obtener propiedades de Hola de un entorno de servicio de aplicaciones|
|/hostingEnvironments/Write|Crea un nuevo entorno de App Service o actualiza uno que ya existe|
|/hostingEnvironments/Delete|Elimina un entorno de App Service|
|/hostingEnvironments/reboot/Action|Reinicia todas las máquinas de un entorno de App Service|
|/hostingenvironments/resume/action|Reanuda los entornos de hospedaje.|
|/hostingenvironments/suspend/action|Suspende los entornos de hospedaje.|
|/hostingenvironments/metricdefinitions/read|Obtiene las definiciones de métricas de los entornos de hospedaje.|
|/hostingEnvironments/workerPools/Read|Obtener propiedades de Hola de un grupo de trabajo en un entorno de servicio de aplicaciones|
|/hostingEnvironments/workerPools/Write|Crea un nuevo grupo de trabajo en un entorno de App Service o actualiza uno que ya existe|
|/hostingenvironments/workerpools/metricdefinitions/read|Obtiene las definiciones de métricas de los grupos de trabajo de los entornos de hospedaje.|
|/hostingenvironments/workerpools/metrics/read|Obtiene las métricas de los grupos de trabajo de los entornos de hospedaje.|
|/hostingenvironments/workerpools/skus/read|Obtiene las SKU de los grupos de trabajo de los entornos de hospedaje.|
|/hostingenvironments/workerpools/usages/read|Obtiene los usos de los grupos de trabajo de los entornos de hospedaje.|
|/hostingenvironments/sites/read|Obtiene las instancias de Web Apps de los entornos de hospedaje.|
|/hostingenvironments/serverfarms/read|Obtiene los planes de App Service de los entornos de hospedaje.|
|/hostingenvironments/usages/read|Obtiene los usos de los entornos de hospedaje.|
|/hostingenvironments/capacities/read|Obtiene las funcionalidades de los entornos de hospedaje.|
|/hostingenvironments/operations/read|Obtiene las operaciones de los entornos de hospedaje.|
|/hostingEnvironments/multiRolePools/Read|Obtener propiedades de Hola de un grupo de front-end en un entorno de servicio de aplicaciones|
|/hostingEnvironments/multiRolePools/Write|Crea un nuevo grupo de front-end en un entorno de App Service o actualiza uno que ya existe|
|/hostingenvironments/multirolepools/metricdefinitions/read|Obtiene las definiciones de métricas de los grupos MultiRole de los entornos de hospedaje.|
|/hostingenvironments/multirolepools/metrics/read|Obtiene las métricas de los grupos MultiRole de los entornos de hospedaje.|
|/hostingenvironments/multirolepools/skus/read|Obtiene las SKU de los grupos MultiRole de los entornos de hospedaje.|
|/hostingenvironments/multirolepools/usages/read|Obtiene los usos de los grupos MultiRole de los entornos de hospedaje.|
|/hostingenvironments/diagnostics/read|Obtiene los diagnósticos de los entornos de hospedaje.|
|/publishingusers/read|Obtiene los usuarios de publicación.|
|/publishingusers/write|Actualiza los usuarios de publicación.|
|/checknameavailability/read|Comprueba si el nombre de recurso está disponible.|
|/geoRegions/Read|Obtener lista de Hola de regiones geográficas.|
|/sites/Read|Obtener propiedades de Hola de una aplicación Web|
|/sites/Write|Crea una nueva aplicación web o actualiza una ya existente|
|/sites/Delete|Eliminación de una aplicación web existente|
|/sites/backup/Action|Crea una copia de seguridad de una nueva aplicación web|
|/sites/publishxml/Action|Obtiene el xml del perfil de publicación de una aplicación web|
|/sites/publish/Action|Publica una aplicación web|
|/sites/restart/Action|Reinicia una aplicación web|
|/sites/start/Action|Inicia una aplicación web|
|/sites/stop/Action|Detiene una aplicación web|
|/sites/slotsswap/Action|Intercambia ranuras de implementación de aplicación web|
|/sites/slotsdiffs/Action|Obtiene las diferencias de configuración entre la aplicación web y las ranuras|
|/sites/applySlotConfig/Action|Aplicar configuración de ranura de aplicación web de la aplicación actual de web de destino ranura toohello|
|/sites/resetSlotConfig/Action|Restablece la configuración de la aplicación web|
|/sites/functions/action|Funciones de Web Apps.|
|/sites/listsyncfunctiontriggerstatus/action|Enumera las instancias de Web Apps de estado del desencadenador de funciones de sincronización.|
|/sites/networktrace/action|Realiza un seguimiento de red de las instancias de Web Apps.|
|/sites/newpassword/action|Genera una nueva contraseña para las instancias de Web Apps.|
|/sites/sync/action|Sincroniza las instancias de Web Apps.|
|/sites/operationresults/read|Obtiene los resultados de la operación de Web Apps.|
|/sites/webjobs/read|Obtiene los WebJobs de Web Apps.|
|/sites/backup/read|Obtiene una copia de seguridad de Web Apps.|
|/sites/backup/write|Actualiza la copia de seguridad de Web Apps.|
|/sites/metricdefinitions/read|Obtiene las definiciones de métricas de Web Apps.|
|/sites/metrics/read|Obtiene las métricas de Web Apps.|
|/sites/continuouswebjobs/delete|Elimina WebJobs continuos de Web Apps.|
|/sites/continuouswebjobs/read|Obtiene WebJobs continuos de Web Apps.|
|/sites/continuouswebjobs/start/action|Inicia WebJobs continuos de Web Apps.|
|/sites/continuouswebjobs/stop/action|Detiene WebJobs continuos de Web Apps.|
|/sites/domainownershipidentifiers/read|Obtiene identificadores de propiedad de dominio de Web Apps.|
|/sites/domainownershipidentifiers/write|Actualiza identificadores de propiedad de dominio de Web Apps.|
|/sites/premieraddons/delete|Elimina complementos Premier de Web Apps.|
|/sites/premieraddons/read|Obtiene complementos Premier de Web Apps.|
|/sites/premieraddons/write|Actualiza complementos Premier de Web Apps.|
|/sites/triggeredwebjobs/delete|Elimina WebJobs desencadenados de Web Apps.|
|/sites/triggeredwebjobs/read|Obtiene WebJobs desencadenados de Web Apps.|
|/sites/triggeredwebjobs/run/action|Ejecuta WebJobs desencadenados de Web Apps.|
|/sites/hostnamebindings/delete|Elimina enlaces de nombre de host de Web Apps.|
|/sites/hostnamebindings/read|Obtiene enlaces de nombre de host de Web Apps.|
|/sites/hostnamebindings/write|Actualiza enlaces de nombre de host de Web Apps.|
|/sites/virtualnetworkconnections/delete|Elimina conexiones de red virtual de Web Apps.|
|/sites/virtualnetworkconnections/read|Obtiene conexiones de red virtual de Web Apps.|
|/sites/virtualnetworkconnections/write|Actualiza conexiones de red virtual de Web Apps.|
|/sites/virtualnetworkconnections/gateways/read|Obtiene puertas de enlace de conexiones de red virtual de Web Apps.|
|/sites/virtualnetworkconnections/gateways/write|Actualiza puertas de enlace de conexiones de red virtual de Web Apps.|
|/sites/publishxml/read|Obtiene el XML de publicación de Web Apps.|
|/sites/hybridconnectionrelays/read|Obtiene las retransmisiones de conexiones híbridas de Web Apps.|
|/sites/perfcounters/read|Obtiene los contadores de rendimiento de Web Apps.|
|/sites/usages/read|Obtiene los usos de Web Apps.|
|/sites/slots/Write|Crea una nueva ranura de aplicación web o actualiza una ya existente|
|/sites/slots/Delete|Elimina una ranura de aplicación web existente|
|/sites/slots/backup/Action|Crea una nueva copia de seguridad de ranura de aplicación web.|
|/sites/slots/publishxml/Action|Obtiene el xml del perfil de publicación de una ranura de aplicación web|
|/sites/slots/publish/Action|Publica una ranura de aplicación web|
|/sites/slots/restart/Action|Reinicia una ranura de aplicación web|
|/sites/slots/start/Action|Inicia una ranura de aplicación web|
|/sites/slots/stop/Action|Detiene una ranura de aplicación web|
|/sites/slots/slotsswap/Action|Intercambia ranuras de implementación de aplicación web|
|/sites/slots/slotsdiffs/Action|Obtiene las diferencias de configuración entre la aplicación web y las ranuras|
|/sites/slots/applySlotConfig/Action|Aplicar configuración de ranura de aplicación web de ranura de destino ranura toohello actual.|
|/sites/slots/resetSlotConfig/Action|Restablece la configuración de ranuras de la aplicación web|
|/sites/slots/Read|Obtener propiedades de Hola de una ranura de implementación de aplicación Web|
|/sites/slots/newpassword/action|Genera una nueva contraseña para las ranuras de instancias de Web Apps.|
|/sites/slots/sync/action|Sincroniza ranuras de Web Apps.|
|/sites/slots/operationresults/read|Obtiene los resultados de la operación de ranuras de Web Apps.|
|/sites/slots/webjobs/read|Obtiene los WebJobs de ranuras de Web Apps.|
|/sites/slots/backup/write|Actualiza la copia de seguridad de ranuras de Web Apps.|
|/sites/slots/metricdefinitions/read|Obtiene las definiciones de métricas de ranuras de Web Apps.|
|/sites/slots/metrics/read|Obtiene las métricas de ranuras de Web Apps.|
|/sites/slots/continuouswebjobs/delete|Elimina WebJobs continuos de ranuras de Web Apps.|
|/sites/slots/continuouswebjobs/read|Obtiene WebJobs continuos de ranuras de Web Apps.|
|/sites/slots/continuouswebjobs/start/action|Inicia WebJobs continuos de ranuras de Web Apps.|
|/sites/slots/continuouswebjobs/stop/action|Detiene WebJobs continuos de ranuras de Web Apps.|
|/sites/slots/premieraddons/delete|Elimina complementos Premier de ranuras de Web Apps.|
|/sites/slots/premieraddons/read|Obtiene complementos Premier de ranuras de Web Apps.|
|/sites/slots/premieraddons/write|Actualiza complementos Premier de ranuras de Web Apps.|
|/sites/slots/triggeredwebjobs/delete|Elimina WebJobs desencadenados de ranuras de Web Apps.|
|/sites/slots/triggeredwebjobs/read|Obtiene WebJobs desencadenados de ranuras de Web Apps.|
|/sites/slots/triggeredwebjobs/run/action|Ejecuta WebJobs desencadenados de ranuras de Web Apps.|
|/sites/slots/hostnamebindings/delete|Elimina enlaces de nombre de host de ranuras de Web Apps.|
|/sites/slots/hostnamebindings/read|Obtiene enlaces de nombre de host de ranuras de Web Apps.|
|/sites/slots/hostnamebindings/write|Actualiza enlaces de nombre de host de ranuras de Web Apps.|
|/sites/slots/phplogging/read|Obtiene Phplogging de ranuras de Web Apps.|
|/sites/slots/virtualnetworkconnections/delete|Elimina conexiones de red virtual de ranuras de Web Apps.|
|/sites/slots/virtualnetworkconnections/read|Obtiene conexiones de red virtual de ranuras de Web Apps.|
|/sites/slots/virtualnetworkconnections/write|Actualiza conexiones de red virtual de ranuras de Web Apps.|
|/sites/slots/virtualnetworkconnections/gateways/write|Actualiza puertas de enlace de conexiones de red virtual de ranuras de Web Apps.|
|/sites/slots/usages/read|Obtiene los usos de ranuras de Web Apps.|
|/sites/slots/hybridconnection/delete|Elimine la conexión híbrida de ranuras de Web Apps.|
|/sites/slots/hybridconnection/read|Obtiene la conexión híbrida de ranuras de Web Apps.|
|/sites/slots/hybridconnection/write|Actualiza la conexión híbrida de ranuras de Web Apps.|
|/sites/slots/config/Read|Obtiene las opciones de configuración de ranura de Web Apps|
|/sites/slots/config/list/Action|Muestra las opciones confidenciales de seguridad de ranuras de Web Apps como las credenciales de publicación, la configuración de la aplicación y las cadenas de conexión|
|/sites/slots/config/Write|Actualiza las opciones de configuración de ranura de Web Apps|
|/sites/slots/config/delete|Elimina la configuración de ranuras de Web Apps.|
|/sites/slots/instances/read|Obtiene instancias de ranuras de Web Apps.|
|/sites/slots/instances/processes/read|Obtiene procesos de instancias de ranuras de Web Apps.|
|/sites/slots/instances/deployments/read|Obtiene implementaciones de instancias de ranuras de Web Apps.|
|/sites/slots/sourcecontrols/Read|Obtiene las opciones de configuración de control de código fuente de ranuras de Web Apps|
|/sites/slots/sourcecontrols/Write|Actualiza las opciones de configuración de control de código fuente de ranuras de Web Apps|
|/sites/slots/sourcecontrols/Delete|Elimina las opciones de configuración de control de código fuente de ranuras de Web Apps|
|/sites/slots/restore/read|Obtiene la restauración de ranuras de Web Apps.|
|/sites/slots/analyzecustomhostname/read|Obtiene el nombre de host personalizado del análisis de ranuras de Web Apps.|
|/sites/slots/backups/Read|Obtener propiedades de Hola de copia de seguridad de ranuras de aplicación web|
|/sites/slots/backups/list/action|Muestra las copias de seguridad de ranuras de Web Apps.|
|/sites/slots/backups/restore/action|Restaura las copias de seguridad de ranuras de Web Apps.|
|/sites/slots/deployments/delete|Elimina las implementaciones de ranuras de Web Apps.|
|/sites/slots/deployments/read|Obtiene las implementaciones de ranuras de Web Apps.|
|/sites/slots/deployments/write|Actualiza las implementaciones de ranuras de Web Apps.|
|/sites/slots/deployments/log/read|Obtiene el registro de implementaciones de ranuras de Web Apps.|
|/sites/hybridconnection/delete|Elimina la conexión híbrida de Web Apps.|
|/sites/hybridconnection/read|Obtiene la conexión híbrida de Web Apps.|
|/sites/hybridconnection/write|Actualiza la conexión híbrida de Web Apps.|
|/sites/recommendationhistory/read|Obtiene el historial de recomendaciones de Web Apps.|
|/sites/recommendations/Read|Obtener lista de Hola de recomendaciones para la aplicación web.|
|/sites/recommendations/disable/action|Deshabilita las recomendaciones de Web Apps.|
|/sites/config/Read|Obtiene las opciones de configuración de Web Apps|
|/sites/config/list/Action|Muestra las opciones confidenciales de seguridad de Web Apps como las credenciales de publicación, la configuración de la aplicación y las cadenas de conexión|
|/sites/config/Write|Actualiza las opciones de configuración de Web Apps|
|/sites/config/delete|Elimina la configuración de Web Apps.|
|/sites/instances/read|Obtiene instancias de Web Apps.|
|/sites/instances/processes/delete|Elimina procesos de instancias de Web Apps.|
|/sites/instances/processes/read|Obtiene procesos de instancias de Web Apps.|
|/sites/instances/deployments/read|Obtiene implementaciones de instancias de Web Apps.|
|/sites/sourcecontrols/Read|Obtiene las opciones de configuración de control de código fuente de Web Apps|
|/sites/sourcecontrols/Write|Actualiza las opciones de configuración de control de código fuente de Web Apps|
|/sites/sourcecontrols/Delete|Elimina las opciones de configuración de control de código fuente de Web Apps|
|/sites/restore/read|Obtiene la restauración de Web Apps.|
|/sites/analyzecustomhostname/read|Analiza el nombre de host personalizado.|
|/sites/backups/Read|Obtener propiedades de Hola de copia de seguridad de una aplicación web|
|/sites/backups/list/action|Muestra las copias de seguridad de Web Apps.|
|/sites/backups/restore/action|Restaura las copias de seguridad de Web Apps.|
|/sites/snapshots/read|Obtiene instantáneas de Web Apps.|
|/sites/functions/delete|Elimina funciones de Web Apps.|
|/sites/functions/listsecrets/action|Muestra secretos de Web Apps.|
|/sites/functions/read|Obtiene funciones de Web Apps.|
|/sites/functions/write|Actualiza funciones de Web Apps.|
|/sites/deployments/delete|Elimina las implementaciones de Web Apps.|
|/sites/deployments/read|Obtiene las implementaciones de Web Apps.|
|/sites/deployments/write|Actualiza las implementaciones de Web Apps.|
|/sites/deployments/log/read|Obtiene el registro de las implementaciones de Web Apps.|
|/sites/diagnostics/read|Obtiene diagnósticos de Web Apps.|
|/sites/diagnostics/workerprocessrecycle/read|Obtiene el reciclaje del proceso de trabajo de diagnóstico de Web Apps.|
|/sites/diagnostics/workeravailability/read|Obtiene el valor de Workeravailability de diagnóstico de Web Apps.|
|/sites/diagnostics/runtimeavailability/read|Obtiene la disponibilidad de tiempo de ejecución de diagnóstico de Web Apps.|
|/sites/diagnostics/cpuanalysis/read|Obtiene el valor de Cpuanalysis de diagnósticos de Web Apps.|
|/sites/diagnostics/servicehealth/read|Obtiene el estado del servicio de diagnóstico de Web Apps.|
|/sites/diagnostics/frebanalysis/read|Obtiene el análisis FREB de diagnóstico de Web Apps.|
|/availablestacks/read|Obtiene las pilas disponibles.|
|/isusernameavailable/read|Comprueba si el nombre de usuario está disponible.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Read|Obtener lista de Hola de API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Write|Agrega una nueva API o actualiza una que ya existe.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Delete|Elimina una API existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Read|Obtener lista de Hola de conexiones.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Write|Guarda una conexión nueva o actualiza una ya existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Delete|Elimina una conexión existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Read|Lee ConnectionAcls|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Write|Agrega o actualiza ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Delete|Elimina ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connectionAcls/Read|Lee ConnectionAcls para la API|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Read|Lee ConnectionAcls|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Write|Crea o actualiza las listas ACL de la API|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Delete|Elimina las listas ACL de la API|
|/serverfarms/Read|Obtener propiedades de hello en un Plan de servicio de aplicaciones|
|/serverfarms/Write|Crea un nuevo plan de App Service o actualiza uno que ya existe|
|/serverfarms/Delete|Eliminación de un plan del Servicio de aplicaciones|
|/serverfarms/restartSites/Action|Reinicia todas las instancias de Web Apps de un plan de App Service|
|/serverfarms/operationresults/read|Obtiene los resultados de la operación de planes de App Service.|
|/serverfarms/capabilities/read|Obtiene las funcionalidades de los planes de App Service.|
|/serverfarms/metricdefinitions/read|Obtiene las definiciones de métricas de los planes de App Service.|
|/serverfarms/metrics/read|Obtiene las métricas de los planes de App Service.|
|/serverfarms/hybridconnectionplanlimits/read|Obtiene los límites del plan de conexión híbrida de los planes de App Service.|
|/serverfarms/virtualnetworkconnections/read|Obtiene las conexiones de red virtual de los planes de App Service.|
|/serverfarms/virtualnetworkconnections/routes/delete|Elimina las rutas de las conexiones de red virtual de los planes de App Service.|
|/serverfarms/virtualnetworkconnections/routes/read|Obtiene las rutas de las conexiones de red virtual de los planes de App Service.|
|/serverfarms/virtualnetworkconnections/routes/write|Actualiza las rutas de las conexiones de red virtual de los planes de App Service.|
|/serverfarms/virtualnetworkconnections/gateways/write|Actualiza las puertas de enlace de las conexiones de red virtual de los planes de App Service.|
|/serverfarms/firstpartyapps/settings/delete|Elimina la configuración de aplicaciones propias de los planes de App Service.|
|/serverfarms/firstpartyapps/settings/read|Obtiene la configuración de aplicaciones propias de los planes de App Service.|
|/serverfarms/firstpartyapps/settings/write|Actualiza la configuración de aplicaciones propias de los planes de App Service.|
|/serverfarms/sites/read|Obtiene las instancias de Web Apps de los planes de App Service.|
|/serverfarms/workers/reboot/action|Reinicia los trabajos de los planes de App Service.|
|/serverfarms/hybridconnectionrelays/read|Obtiene las retransmisiones de conexión híbrida de los planes de App Service.|
|/serverfarms/skus/read|Obtiene las SKU de los planes de App Service.|
|/serverfarms/usages/read|Obtiene los usos de los planes de App Service.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/read|Obtiene las instancias de Web Apps de las retransmisiones de espacios de nombres de conexión híbrida de los planes de App Service.|
|/ishostnameavailable/read|Comprueba si el nombre de host está disponible.|
|/connectionGateways/Read|Obtener lista de Hola de puertas de enlace de conexión.|
|/connectionGateways/Write|Crea o actualiza una puerta de enlace de conexión.|
|/connectionGateways/Delete|Elimina una puerta de enlace de conexión.|
|/connectionGateways/Join/Action|Se une a una puerta de enlace de conexión.|
|/classicmobileservices/read|Obtiene Mobile Services clásico.|
|/skus/read|Obtiene las SKU.|
|/certificates/Read|Obtener lista de Hola de certificados.|
|/certificates/Write|Agrega un nuevo certificado o actualiza uno existente.|
|/certificates/Delete|Elimina un certificado existente.|
|/operations/read|Obtiene operaciones.|
|/recommendations/Read|Obtener lista de Hola de recomendaciones para las suscripciones.|
|/ishostingenvironmentnameavailable/read|Averigua si el nombre del entorno de hospedaje está disponible.|
|/apiManagementAccounts/Read|Obtener lista de Hola de ApiManagementAccounts.|
|/apiManagementAccounts/Write|Agrega una nueva ApiManagementAccount o actualiza una que ya existe|
|/apiManagementAccounts/Delete|Elimina una ApiManagementAccount existente|
|/apiManagementAccounts/connectionAcls/Read|Obtener lista de Hola de ACL de conexión.|
|/apiManagementAccounts/apiAcls/Read|Lee ConnectionAcls|
|/connections/Read|Obtener lista de Hola de conexiones.|
|/connections/Write|Crea o actualiza una conexión.|
|/connections/Delete|Elimina una conexión.|
|/connections/Join/Action|Se une a una conexión.|
|/connections/confirmconsentcode/action|Confirma el código de consentimiento de conexiones.|
|/connections/listconsentlinks/action|Enumera los vínculos de consentimiento de las conexiones.|
|/deploymentlocations/read|Obtiene las ubicaciones de implementación.|
|/sourcecontrols/read|Obtiene los controles de origen.|
|/sourcecontrols/write|Actualiza los controles de origen.|
|/managedhostingenvironments/read|Obtiene los entornos de hospedaje administrados.|
|/managedhostingenvironments/sites/read|Obtiene las instancias de Web Apps de los entornos de hospedaje administrados.|
|/managedhostingenvironments/serverfarms/read|Obtiene los planes de App Service de los entornos de hospedaje administrados.|
|/locations/managedapis/read|Obtiene las API administradas de ubicaciones.|
|/locations/apioperations/read|Obtiene las operaciones de API de ubicaciones.|
|/locations/connectiongatewayinstallations/read|Obtiene las instalaciones de puertas de enlace de conexiones de ubicaciones.|
|/listSitesAssignedToHostName/Read|Obtener los nombres de sitios asignados toohostname.|

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo demasiado[crear un rol personalizado](role-based-access-control-custom-roles.md).

- Hola de revisión [integrada en roles RBAC](role-based-access-built-in-roles.md).

- Obtenga información acerca de cómo toomanage tener acceso a las asignaciones de [usuario](role-based-access-control-manage-assignments.md) o [por recurso](role-based-access-control-configure.md) 
