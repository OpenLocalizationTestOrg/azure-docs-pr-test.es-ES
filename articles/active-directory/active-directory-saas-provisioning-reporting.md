---
title: "Generación de informes en aplicaciones tooSaaS de aprovisionamiento de cuentas de usuario automático de Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocheck Hola estado de trabajos de aprovisionamiento de cuentas de usuario automática y cómo tootroubleshoot Hola aprovisionamiento de usuarios individuales."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Tutorial: Creación de informes sobre el aprovisionamiento automático de cuentas de usuario


Azure Active Directory incluye una [servicio de aprovisionamiento de la cuenta de usuario](active-directory-saas-app-provisioning.md) que facilita la automatización Hola aprovisionamiento anula su aprovisionamiento de cuentas de usuario en aplicaciones de SaaS y otros sistemas, a fin de hello del ciclo de vida de identidad de extremo a extremo administración de. Azure AD admite previamente integradas de hello aplicaciones y sistemas en la sección "Destacado" hello del programa Hola a todos los conectores de aprovisionamiento de usuarios [Galería de aplicaciones de Azure AD](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

Este artículo describe cómo toocheck estado de Hola de aprovisionamiento de trabajos después de que se han establecido hasta y cómo tootroubleshoot Hola aprovisionamiento de usuarios individuales y grupos.

## <a name="overview"></a>Información general

Conectores de aprovisionamiento se configuran principalmente y configuran mediante hello [portal de administración de Azure](https://portal.azure.com), por hello siguiente [proporciona documentación](active-directory-saas-tutorial-list.md) para la aplicación hello donde usuario aprovisionamiento de cuentas se desea. Una vez configurados y en ejecución, es posible notificar trabajos de aprovisionamiento para una aplicación mediante uno de estos dos métodos:

* **Portal de administración de Azure** -este artículo describe principalmente al recuperar información de informe de hello [portal de administración de Azure](https://portal.azure.com), que proporciona tanto un informe de resumen de aprovisionamiento como aprovisionamiento detallada auditoría de registros para una aplicación determinada.

* **API de auditoría** -Azure Active Directory también proporciona una API que permite la recuperación mediante programación de hello detallada de aprovisionamiento de los registros de auditoría de auditoría. Vea [auditoría referencia de la API de Azure Active Directory](active-directory-reporting-api-audit-reference.md) para documentación específica toousing esta API. Aunque este artículo no cubre específicamente cómo toouse Hola API, que se detallan a tipos Hola de aprovisionamiento de eventos que se registran en el registro de auditoría de Hola.

### <a name="definitions"></a>Definiciones

Este artículo usa Hola después de términos, que se definen a continuación:

* **Sistema de origen** -repositorio Hola de usuarios que Hola servicio de aprovisionamiento de Azure AD se sincroniza desde. Azure Active Directory es el sistema de origen de hello para la mayoría de Hola de preintegrados aprovisionamiento conectores, sin embargo, hay algunas excepciones (ejemplo: sincronización de entrada de jornada laboral).

* **Sistema de destino** -repositorio Hola de usuarios que Hola servicio de aprovisionamiento de Azure AD se sincroniza con. Normalmente es una aplicación SaaS (ejemplos: Salesforce, ServiceNow, Google Apps, Dropbox para empresas), pero en algunos casos puede ser un sistema local como Active Directory (ejemplo: sincronización de entrada de Workday tooActive directorio).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Obtener informes del portal de administración de Azure Hola de aprovisionamiento

tooget información del informe para una aplicación determinada, el aprovisionamiento inicial iniciando hello [portal de administración de Azure](https://portal.azure.com) y aplicación de Enterprise toohello para el que se configura el aprovisionamiento de exploración. Por ejemplo, si va a aprovisionar usuarios tooLinkedIn elevar, detalles de la aplicación de toohello de ruta de acceso de hello navegación es:

**Azure Active Directory &gt; Aplicaciones empresariales &gt; Todas las aplicaciones &gt; LinkedIn Elevate**

Desde aquí, puede tener acceso a informe de resumen de aprovisionamiento de Hola y de registros de auditoría de aprovisionamiento de hello, ambos se describen a continuación.


### <a name="provisioning-summary-report"></a>Informe de resumen de aprovisionamiento

Hola informe resumen de aprovisionamiento está visible en hello **Provisioning** pestaña dada la aplicación. Se encuentra en la sección de detalles de sincronización de hello debajo **configuración**y proporciona Hola siguiente información:

* número total de usuarios de Hola y / grupos que se han sincronizado y están actualmente en el ámbito para el aprovisionamiento de entre el sistema de origen de Hola y el sistema de destino de Hola.

* Hola última Hola sincronización se ejecutó. Las sincronizaciones suelen producirse cada 20-40 minutos, una vez que haya finalizado una sincronización completa.

* Tanto si ha finalizado una sincronización completa inicial como si no.

* Si no se ha colocado Hola proceso de aprovisionamiento en cuarentena y qué motivo hello para el estado de cuarentena de hello p. ej. es (toocommunicate de error con el sistema de destino debido a credenciales de administrador de tooinvalid)

Hola informe resumen de aprovisionamiento debe ser Hola primer lugar administradores apariencia toocheck en estado operativo de Hola de trabajo de aprovisionamiento de Hola.

 ![Informe de resumen](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Registros de auditoría de aprovisionamiento
Todas las actividades realizadas por hello aprovisionamiento del servicio se registran en los registros de auditoría de hello Azure AD, que pueden verse en hello **registros de auditoría** pestaña hello **el aprovisionamiento de cuentas** categoría. Los tipos de eventos de actividades registradas incluyen:

* **Importar eventos** -cada vez que servicio de aprovisionamiento de hello Azure AD recupera información sobre un usuario individual o un grupo desde un sistema de origen o destino se registra un evento de "importación". Durante la sincronización, los usuarios se recuperan de sistema de origen de hello en primer lugar, con resultados de hello registrados como "importar" eventos. Hola, a continuación, se consulta Id. coincidentes de hello recuperado a los usuarios contra Hola destino sistema toocheck si los hay, con resultados de hello que también se registran como "importar" eventos. Estos eventos registran todos los atributos de usuario asignado y sus valores que estaban visibles para el servicio de aprovisionamiento de hello Azure AD en tiempo de Hola de evento Hola. 

* **Eventos de la regla de sincronización** : estos eventos de informes de resultados de Hola de reglas de asignación de atributos de Hola y cualquier configurado filtros de ámbito, después de haber importado datos de usuario y evalúan de sistemas de origen y destino de Hola. Por ejemplo, si un usuario en un sistema de origen se considera toobe en el ámbito de aprovisionamiento y toonot considerará como existe en el sistema de destino de hello, este evento registra que Hola usuario se aprovisionará en el sistema de destino de Hola. 

* **Exportar eventos** -cada vez que el servicio de aprovisionamiento de hello Azure AD escribe un usuario cuenta o grupo objeto tooa sistema de destino se registra un evento de "exportación". Estos eventos registran todos los atributos de usuario y sus valores que se hayan escrito Hola servicio de aprovisionamiento de Azure AD en tiempo de Hola de evento Hola. Si se produjo un error al escribir Hola usuario cuenta o grupo objeto toohello sistema de destino, se mostrará aquí.

* **Procesar los eventos de custodia** -depósitos de garantía de proceso se producen cuando hello aprovisionamiento del servicio encuentra un error al intentar una operación y comienza la operación de hello tooretry en un intervalo de retroceso de tiempo. Cada vez que se retire una operación de aprovisionamiento, se registra un evento de "custodia".

Al examinar los eventos de aprovisionamiento para un usuario individual, Hola normalmente se producen eventos en este orden:

1. Evento de importación: usuario se recupera del sistema de origen de Hola.

2. Evento de importación: sistema de destino es toocheck consultado existencia de Hola de usuario de hello recuperar.

3. Evento de regla de sincronización: datos de usuario de sistemas de origen y destino se evalúan con el atributo de hello configurado reglas de asignación y el ámbito filtros toodetermine qué acción, si lo hay, debe realizarse.

4. Exportar eventos: si el evento de regla de sincronización de hello dicta que una acción debe realizar (por ejemplo, agregar, actualizar, eliminar), a continuación, resultados de Hola de acción de Hola se registran en un evento de exportación.

![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Búsqueda de eventos de aprovisionamiento para un usuario específico

Hello caso de uso más comunes para los registros de auditoría de aprovisionamiento de hello es hello toocheck estado de una cuenta de usuario individual de aprovisionamiento. toolook eventos último de aprovisionamiento Hola para un usuario específico:

1. Vaya toohello **registros de auditoría** sección.

2. De hello **categoría** menú, seleccione **el aprovisionamiento de cuentas**.

3. Hola **intervalo de fechas** menú, intervalo de fechas de hello seleccione desea toosearch,

4. Hola **búsqueda** barra, escriba Hola identificador de usuario de hello desea toosearch para. formato de Hello del valor de identificador debe coincidir con lo que ha seleccionado como Hola principal identificador coincidente en la configuración de asignación de atributo de hello (por ejemplo, userPrincipalName o empleado número de Id.). valor de Id. de Hello necesario serán visible en la columna de destinos de Hola.

5. Presione ENTRAR toosearch. en primer lugar se devolverá Hello más reciente de aprovisionamiento de eventos.

6. Si se devuelven los eventos, tenga en cuenta los tipos de actividad de Hola y si se ha realizado correctamente o no. Si se devuelve ningún resultado, significa que el usuario de hello no existe o aún no se ha detectado por el proceso de aprovisionamiento si no se ha completado una sincronización completa de Hola.

7. Haga clic en los eventos individuales tooview extendido detalles, incluidas todas las propiedades de usuario que se recuperan, evaluar o escritas como parte del evento Hola.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Sugerencias para ver los registros de auditoría de aprovisionamiento de Hola

Para optimizar la legibilidad en hello portal de Azure, seleccione hello **columnas** botón y elija estas columnas:

* **Fecha** -muestra eventos de hello fecha Hola se han producido.
* **Uno o varios destinos** -muestra hello aplicación nombre e identificador de usuario que están sujetos Hola de evento de Hola.
* **Actividad** -Hola tipo de actividad, como se describió anteriormente.
* **Estado** : indica si el evento de Hola se realizó correctamente o no.
* **La razón del estado** -un resumen de lo que sucedió en hello aprovisionamiento de eventos.


## <a name="troubleshooting"></a>Solución de problemas

Hola registros de auditoría y el informe resumen de aprovisionamiento desempeñan un papel clave ayudar a los administradores a solucionar diversos problemas de aprovisionamiento de cuentas de usuario.

Para obtener instrucciones sobre cómo basada en escenario tootroubleshoot automática aprovisionamiento de usuario, consulte [problemas de configuración y el aprovisionamiento de usuarios tooan application](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
