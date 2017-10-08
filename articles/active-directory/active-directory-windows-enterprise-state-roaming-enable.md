---
title: aaaEnable itinerancia de estado de empresa en Azure Active Directory | Documentos de Microsoft
description: "Preguntas más frecuentes sobre la configuración Enterprise State Roaming en dispositivos de Windows. Itinerancia de estado de Enterprise proporciona a los usuarios una experiencia unificada a través de sus dispositivos de Windows y reduce el tiempo de hello necesario para configurar un nuevo dispositivo."
services: active-directory
keywords: "estado de empresa móvil, nube de windows, la itinerancia de estado de enterprise tooenable"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Habilitación de Enterprise State Roaming en Azure Active Directory
Itinerancia de estado de empresa es la organización de tooany disponible con una suscripción Premium de Azure Active Directory (Azure AD). Para obtener más información acerca de cómo tooget una suscripción de Azure AD, vea hello [página del producto de Azure AD](https://azure.microsoft.com/services/active-directory).

Cuando se habilita la itinerancia de estado de empresa, su organización se le otorgarán automáticamente licencias para una tooAzure de suscripción gratuita y de uso limitado a Rights Management. Esta suscripción gratuita es tooencrypting limitado y descifrar los datos de aplicación sincronizadas Hola itinerancia de estado de Enterprise servicio; y la configuración de enterprise debe tener una suscripción de pago toouse Hola todas las capacidades de Azure Rights Management.

Después de obtener una suscripción de Azure AD Premium, siga estas tooenable pasos itinerancia de estado de Enterprise:

1. Inicio de sesión toohello portal de Azure clásico.
2. Hola izquierda, seleccione **ACTIVE DIRECTORY**y, a continuación, seleccione directorio de hello para el que desee tooenable itinerancia de estado de empresa.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Vaya toohello **configurar** ficha en la parte superior de Hola.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Desplácese hacia abajo en la página de Hola y seleccione **a los usuarios pueden sincronizar la configuración y datos de aplicaciones empresariales**y, a continuación, haga clic en **guardar**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Para una configuración de tooroam de dispositivos Windows 10 con hello servicio itinerancia de estado de empresa, dispositivos de hello deben autenticarse mediante una identidad de Azure AD. Para los dispositivos que están combinada tooAzure AD, inicio de sesión principal del usuario de hello es identidad hello Azure AD, por lo que se requiere ninguna configuración adicional. Para los dispositivos que usan un Active Directory local tradicional, Hola Administrador de TI debe [conectar Hola dispositivos Unidos a dominio tooAzure AD para Windows 10 experimenta](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Almacenamiento de datos de sincronización
Datos de itinerancia de estado de empresa se hospedan en uno o varios [regiones de Azure](https://azure.microsoft.com/regions/) que mejor se alinee con el valor de país o región de hello establecido en la instancia de Azure Active Directory Hola. Los datos de Enterprise State Roaming se particionan en función de las tres regiones geográficas principales: Norteamérica, EMEA y APAC. Datos de itinerancia de estado de empresa para el inquilino de Hola se encuentra localmente con la región geográfica de hello y no se replican entre regiones.  Por ejemplo, los clientes que tienen su tooone de conjunto de valor de país o región de países EMEA como "Francia" o "Zambia" tendrá sus datos hospedan en uno o de hello regiones de Azure en Europa.  Los clientes que establecer su valor de país o región en Azure AD tooone de países de América del Norte como "United States" o "Canadá" tendrán sus datos hospedan en uno o varios de hello regiones de Azure en hello Estados Unidos.  Los clientes que establecer su valor de país o región en Azure AD tooone de países APAC como "Australia" o "Nueva Zelanda" tendrán sus datos hospedan en uno o varios de hello regiones de Azure en Asia.  Países Sudamérica y datos Antártida se hospedará en uno o más regiones de Azure en hello Estados Unidos.  valor de país o región de Hola se establece como parte del proceso de creación del directorio de Azure AD hello y no se puede modificar posteriormente. 

Para más detalles sobre la ubicación de almacenamiento de datos, genere una incidencia con el [soporte técnico de Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Administración de Enterprise State Roaming
Los administradores globales de Azure AD pueden habilitar y deshabilitar la itinerancia de estado de empresa en hello portal de Azure clásico.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Los administradores globales pueden limitar los grupos de seguridad de configuración de la sincronización toospecific.

Administradores globales también pueden ver un informe de estado de sincronización de dispositivos por usuario mediante la selección de un usuario determinado en la instancia de Active Directory de hello **usuarios** lista y haga clic en **dispositivos** ficha y seleccione Vista **Dispositivos sincronizando ajustes y datos de aplicaciones empresariales**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Retención de datos
TooAzure datos sincronizados a través de itinerancia de estado de empresa se retendrán indefinidamente a menos que se realiza una operación de eliminación manual o datos de hello en cuestión determinado toobe obsoletos. 

**Eliminación explícita:** Hola datos se eliminan cuando un administrador de Azure elimina un usuario o un directorio o un administrador solicita explícitamente que los datos están toobe eliminado.

* **Eliminación de usuario**: cuando se elimina un usuario en Azure AD, cuenta de usuario de hello itinerancia de datos se marcarán para su eliminación y se eliminará de 90 días de too180. 
* **Eliminación de inquilinos**: la eliminación de un directorio completo en Azure AD se realiza inmediatamente. Todos los datos de configuración de hello asociado con el directorio se marcarán para su eliminación y se eliminará de 90 días de too180. 
* **En la eliminación de la petición**: si hello Azure AD administrador desea toomanually elimina los datos o los datos de configuración de un usuario específico, Hola, administrador puede presentar una incidencia a [soporte técnico de Azure](https://azure.microsoft.com/support/). 

**Una eliminación de datos, es decir obsoleto**: datos que no se ha accedido para un año ("período de retención de Hola") se tratará como obsoleta y se puede eliminar de Azure. período de retención de Hello es toochange de asunto, pero no será inferior a 90 días. los datos obsoletos de Hello pueden ser un conjunto específico de valores de configuración de Windows/aplicación o toda la configuración de un usuario. Por ejemplo:

* Si no hay ningún dispositivo acceso a una colección de configuraciones concretas (por ejemplo, se quita una aplicación de dispositivo de Hola o un grupo de configuración, como "Tema" está deshabilitado para todos los dispositivos de un usuario), entonces esa colección quedarán obsoleta tras período de retención de Hola y puede ser eliminar. 
* Si un usuario ha desactivado la sincronización de configuración en todos los dispositivos de sus, a continuación, ninguno de los datos de configuración de Hola se accederá y todos los datos de configuración de Hola para ese usuario dejará de ser obsoletos y pueden eliminarse tras período de retención de Hola. 
* Si Azure AD de Hola, Administrador de directorio se desactiva itinerancia de estado de empresa para hello todo el directorio, a continuación, todos los usuarios en cuanto directory dejará de sincronización de configuración, y todos los datos de configuración para todos los usuarios quedarán obsoletos y podrían eliminarse tras período de retención de Hola. 

**Elimina la recuperación de datos**: directiva de retención de datos de hello no es configurable. Una vez que se ha eliminado permanentemente datos hello, no será recuperable. Sin embargo, es importante toonote que Hola los datos de configuración sólo se eliminarán de Azure, no el dispositivo de usuario final Hola. Si cualquier dispositivo más adelante se vuelve a conectar el servicio de movilidad de estado de Enterprise toohello, configuración de hello nuevo se sincronizan y almacenados en Azure.

## <a name="related-topics"></a>Temas relacionados
* [Información general de Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Preguntas más frecuentes sobre itinerancia de datos y configuración](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Configuración de MDM y directivas de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referencia de la configuración de movilidad de Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
