---
title: "códigos de error de API de REST de aprendizaje de máquina aaaAzure | Documentos de Microsoft"
description: "Estos códigos de error podrían ser devueltos por una operación en un servicio web Azure Machine Learning."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Códigos de error de API de REST de Machine Learning
 
Hello siguientes códigos de error podrían ser devueltos por una operación en un servicio web de aprendizaje automático de Azure.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (código de estado HTTP 400)
 
Argumento no válido proporcionado.
 
Esta clase de errores significa que un argumento proporcionado en alguna parte no era válido. Podría tratarse de una credencial o la ubicación del pasado el servicio web de toohello de toosomething de almacenamiento de Azure. Consulte en el campo de "código de error" hello en hello "Detalles" sección toodiagnose qué argumento específico no era válido.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| BadParameterValue | valor del parámetro Hello proporcionado no satisface la regla de parámetro hello en el parámetro hello |
| BadSubscriptionId | Hola suscripción Id. de tooscore usado no es Hola uno presente en el recurso de Hola |
| BadVersionCall | Se pasó el parámetro de versión no válida durante la llamada de API de hello: {0}. Hola API de comprobación de página de ayuda para pasar la versión correcta de Hola y vuelva a intentarlo. |
| BatchJobInputsNotSpecified | Hola siguiendo las entradas necesarias no se especificaron con solicitud de hello: {0}. Asegúrese de que se especifican todos los datos de entrada e inténtelo de nuevo. |
| BatchJobInputsTooManySpecified | solicitud de Hello especifica más entradas lo definido en el servicio de Hola. Lista de entradas aceptadas: {0}. Asegúrese de que todos los datos de entrada se han especificado correctamente e inténtelo de nuevo. |
| BlobNameTooLong | La ruta de acceso de Azure Blob Storage proporcionada para la salida de diagnósticos es demasiado larga: {0}. Acorte la ruta de acceso de Hola y vuelva a intentarlo. |
| BlobNotFound | Hola tooaccess no se puede proporciona blobs de Azure: {0}.  Mensaje de error de Azure: {1}. |
| ContainerIsEmpty | No se proporcionó ningún nombre de contenedor de Azure Storage. Proporcione un nombre de contenedor válido e inténtelo de nuevo. |
| ContainerSegmentInvalid | Nombre de contenedor no válido. Proporcione un nombre de contenedor válido e inténtelo de nuevo. |
| ContainerValidationFailed | Error de validación del contenedor de blobs: {0}. |
| DataTypeNotSupported | Tipo de datos no admitido. Proporcione tipos de datos válidos e inténtelo de nuevo. |
| DuplicateInputInBatchCall | solicitud por lotes de Hello no es válido. No se puede especificar uno y varios entrada en hello mismo tiempo. Quite uno de estos elementos de solicitud de Hola y vuelva a intentarlo. |
| ExpiryTimeInThePast | Proporciona la hora de expiración es Hola anteriores: {0}. Proporcione una hora de expiración futura en UTC e inténtelo de nuevo. toonever expiran, establecer tooNULL de tiempo de expiración. |
| IncompleteSettings | Configuración de diagnósticos incompleta. |
| InputBlobRelativeLocationInvalid | No se proporcionó ningún nombre de Azure Storage Blob. Proporcione un nombre de blob válido e inténtelo de nuevo. |
| InvalidBlob | Especificación de blob no válido para blob: {0}. Compruebe que la cadena de conexión o ruta de acceso relativa, o la especificación de token de SAS sean correctas e inténtelo de nuevo. |
| InvalidBlobConnectionString | Hola la cadena de conexión especificada para uno de los blobs de entrada/salida de hello no válido: {0}. Corrija este problema e inténtelo de nuevo. |
| InvalidBlobExtension | Hola referencia: {0} tiene una extensión de archivo no válido o ausente. Las extensiones de archivo admitidas para este tipo de salida son: "{1}". |
| InvalidInputNames | Nombre (s) especificado en la solicitud de Hola de entrada de servicio no válida: {0}. Asignar entradas de hello datos de entrada toohello servicio correcto y vuelva a intentarlo. |
| InvalidOutputOverrideName | Nombre de invalidación de salida no válida: {0}. Hola servicio no tiene un nodo de salida con este nombre. Pase un toooverride de nombre de nodo de un resultado correcto (se aplica entre mayúsculas y minúsculas). |
| InvalidQueryParameter | Parámetro de consulta no válido '{0}'. {1} |
| MissingInputBlobInformation | Falta información de Azure Storage Blob. Proporcione una cadena de conexión y una ruta de acceso relativa o URI válidos e inténtelo de nuevo. |
| MissingJobId | No se proporcionó un identificador de trabajo. Un trabajo de Id. se devuelve cuando se envía un trabajo para hello primera vez. Compruebe el trabajo de hello Id es correcta e inténtelo de nuevo. |
| MissingKeys | No hay claves proporcionadas o no se proporcionó una clave primaria o secundaria. |
| MissingModelPackage | No se proporcionó un identificador de paquete de modelo o un paquete de modelo. Proporcione un identificador de paquete de modelo o un paquete de modelo válido e inténtelo de nuevo. |
| MissingOutputOverrideSpecification | solicitud de Hello falta la especificación de blob de hello para el reemplazo de salida {0}. Especifique una ubicación de blob válido con la solicitud de hello, o quite la especificación de salida de hello si no se desea ninguna invalidación de ubicación. |
| MissingRequestInput | servicio web de Hello espera una entrada, pero no se proporcionó ninguna entrada. Asegúrese de se proporcionan las entradas válidas para hello publicado puertos en el modelo de Hola de entrada e inténtelo de nuevo. |
| MissingRequiredGlobalParameters | No se proporcionaron todos los parámetros de servicio web necesarios. Compruebe los parámetros de Hola se espera para hello módulos son correctos y vuelva a intentarlo. |
| MissingRequiredOutputOverrides | Cuando se llama a un punto de conexión de servicio cifrada es obligatorio toopass en salida invalida los resultados del servicio de todos los Hola. Faltan invalidaciones en este momento para estas salidas: {0} |
| MissingWebServiceGroupId | No se proporcionó un identificador de grupo de servicio web. Proporcione un identificador de grupo de servicio web válido e inténtelo de nuevo. |
| MissingWebServiceId | No se proporcionó un identificador de servicio web. Proporcione un identificador de servicio web válido e inténtelo de nuevo. |
| MissingWebServicePackage | No se proporcionó ningún paquete de servicio web. Proporcione un paquete de servicio web válido e inténtelo de nuevo. |
| MissingWorkspaceId | No se proporcionó ningún identificador de área de trabajo. Proporcione un identificador de área de trabajo válido e inténtelo de nuevo. |
| ModelConfigurationInvalid | Configuración de modelo no válido en el paquete con el modelo Hola. Asegúrese de configuración del modelo de hello contiene la definición de puntos de conexión de salida, extremo de error std, y std punto de conexión e inténtelo de nuevo. |
| ModelPackageIdInvalid | Identificador de paquete de modelo no válido. Compruebe que ese Id. de paquete de modelo hello es correcta e inténtelo de nuevo. |
| RequestBodyInvalid | Ningún cuerpo de solicitud proporcionado o error al deserializar el cuerpo de la solicitud de saludo. |
| RequestIsEmpty | No se proporciona ninguna solicitud. Proporcione una solicitud válida e inténtelo de nuevo. |
| UnexpectedParameter | Parámetros inesperados proporcionados. Compruebe que todos los nombres de parámetro estén escritos correctamente, que solo e pasan los parámetros previstos e inténtelo de nuevo. |
| UnknownError | Error desconocido. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | No se pueden cambiar los requisitos de solicitudes simultáneas para el servicio web {0}. |
| WebServiceIdInvalid | Se proporcionó un identificador de servicio web no válido. El identificador del servicio web debe ser un guid válido. |
| WebServiceTooManyConcurrentRequestRequirement | No se puede establecer toomore de requisito de solicitudes simultáneas de {0}. |
| WebServiceTypeInvalid | Se proporcionó un tipo de servicio web no válido. Compruebe el tipo de servicio web válido de hello es correcto e inténtelo de nuevo. Tipos de servicio web válidos: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (código de estado HTTP 400)
 
Argumento de usuario no válido proporcionado.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| InputMismatchError | Los datos de entrada no coinciden con el esquema de puerto de entrada. |
| InputParseError | Error de análisis del vector de entrada.  Compruebe vector entrada hello tiene el número correcto de Hola de columnas y tipos de datos.  Detalles adicionales: {0}. |
| MissingRequiredGlobalParameters | Faltan parámetros esperados por el servicio web de Hola. Compruebe que todos los parámetros de hello necesario esperados por el servicio web de hello son correctos e inténtelo de nuevo. |
| UnexpectedParameter | Compruebe solo Hola necesarias se pasan parámetros que espera el servicio web de Hola y vuelva a intentarlo. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (código de estado HTTP 400)
 
Hola solicitud no es válida en el contexto actual de Hola.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| CannotStartJob | no se puede iniciar el trabajo de Hello porque está en estado {0}. |
| IncompatibleModel | modelo de Hello es incompatible con la versión de la solicitud de Hola. versión de la solicitud de Hello solo admite modelos de salida de datatable único. |
| MultipleInputsNotAllowed | modelo de Hello no permite que varias entradas. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (código de estado HTTP 400)
 
La ejecución del módulo encontró un error interno de biblioteca.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (código de estado HTTP 400)
 
Error de ejecución del módulo.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (código de estado HTTP 400)
 
Paquete de servicio web no válido. Compruebe el paquete de servicio web de hello proporcionado es correcto e inténtelo de nuevo.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| FormatError | paquete de servicio web de Hello es incorrecto. Detalles: {0} |
| RuntimesError | gráfico de paquete de servicio de Hello web no es válido. Detalles: {0} |
| ValidationError | gráfico de paquete de servicio de Hello web no es válido. Detalles: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>No autorizado (código de estado HTTP 401)
 
Solicitud es recursos tooaccess no autorizado.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| AdminRequestUnauthorized | No autorizado |
| ManagementRequestUnauthorized | No autorizado |
| ScoreRequestUnauthorized | Credenciales no válidas proporcionadas. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (código de estado HTTP 404)
 
Recurso no encontrado.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| ModelPackageNotFound | Paquete de modelo no encontrado. Compruebe el paquete con el modelo Hola Id es correcta e inténtelo de nuevo. |
| WebServiceIdNotFoundInWorkspace | No se encuentra el servicio web en esta área de trabajo. Hay una incoherencia entre webServiceId Hola y Hola workspaceId. Compruebe el servicio web de hello proporcionado es parte del área de trabajo de Hola y vuelva a intentarlo. |
| WebServiceNotFound | Servicio web no encontrado. Compruebe el servicio web de hello Id es correcta e inténtelo de nuevo. |
| WorkspaceNotFound | Espacio de trabajo no encontrado. Compruebe el área de trabajo de hello Id es correcta e inténtelo de nuevo. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (código de estado HTTP 408)
 
no se pudo completar la operación de Hola en hello permitido de tiempo.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| RequestCanceled | Se canceló la solicitud por cliente Hola. |
| ScoreRequestTimeout | Tiempo de espera agotado para esta solicitud de ejecución. |
 
## <a name="conflict-http-status-code-409"></a>Conflict (código de estado HTTP 409)
 
El recurso ya existe.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Nombre del parámetro de salida no válido. Pruebe a usar columnas de hello metadatos editor módulo toorename e inténtelo de nuevo. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (código de estado HTTP 413)
 
modelo de Hello tenía excedido la cuota de memoria de hello asignada tooit.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| OutOfMemoryLimit | modelo de Hello consume más memoria que estaba destinado a contener lo. Memoria máximo permitido para el modelo de hello es {0} MB. Compruebe el modelo por si tiene problemas. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (código de estado HTTP 500)
 
Error interno en la ejecución.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | el proceso de contenedor de Hola se bloqueó con error del sistema |
| ContainerProcessTerminatedWithUnknownError | el proceso de contenedor de Hola se bloqueó con error desconocido |
| ContainerValidationFailed | Error de validación del contenedor de blobs: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | No se proporcionaron argumentos. Compruebe que se pasan argumentos válidos e inténtelo de nuevo. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | El identificador de puerto {0} tiene un tipo de datos no admitido: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Error en la generación de Swagger. Detalles: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | Código de estado de trabajo desconocido {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage. Detalles: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (código de estado HTTP 500)
 
Error interno en la ejecución. Sistema con poca memoria. Vuelva a intentarlo.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (código de estado HTTP 500)
 
Paquete de modelo no válido. Compruebe el paquete con el modelo Hola proporcionado es correcto e inténtelo de nuevo.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (código de estado HTTP 500)
 
Paquete de servicio web no válido. Compruebe el paquete de hello web proporcionada es correcta e inténtelo de nuevo.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| ModuleError | gráfico de paquete de servicio de Hello web no es válido. Detalles: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (código de estado HTTP 503)
 
no se puede ejecutar la solicitud de Hello como Hola contenedores se está inicializando.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (código de estado HTTP 503)
 
El servicio no está disponible temporalmente.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| NoMoreResources | No hay recursos disponibles para la solicitud. |
| RequestThrottled | Solicitud limitada para el punto de conexión {0}. Hola la simultaneidad máximo para el punto de conexión de hello es {1}. |
| TooManyConcurrentRequests | Demasiadas solicitudes simultáneas enviadas. |
| TooManyHostsBeingInitialized | Hola demasiados hosts que se inicializa al mismo tiempo. Considere la posibilidad de limitarlo o intentarlo de nuevo. |
| TooManyHostsBeingInitializedPerModel | Hola demasiados hosts que se inicializa al mismo tiempo. Considere la posibilidad de limitarlo o intentarlo de nuevo. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (código de estado HTTP 504)
 
no se pudo completar la operación de Hola en hello permitido de tiempo.
 
| Código de error | Mensaje de usuario |
| ---------- |--------------|
| BackendInitializationTimeout | no se pudo completar la inicialización del servicio web Hello en hello permitido de tiempo. |
| BackendScoreTimeout | no se pudo completar la ejecución de la solicitud de servicio de Hello web dentro de hello permitido de tiempo. |
 
