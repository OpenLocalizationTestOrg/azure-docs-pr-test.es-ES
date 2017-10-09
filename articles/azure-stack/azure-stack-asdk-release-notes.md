---
title: "notas de la versión de aaaMicrosoft Kit de desarrollo de pila de Azure | Documentos de Microsoft"
description: 
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: helaw
ms.openlocfilehash: c1644f224933a63e1f0265b6ef4113789900cf12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-release-notes"></a>Notas de la versión de Azure Stack Development Kit
Estas notas de la versión proporcionan información sobre las nuevas características y los problemas conocidos.

## <a name="release-build-201706271"></a>Compilación de versión 20170627.1
A partir de hello [20170627.1](azure-stack-updates.md#determine-the-current-version) versión, Azure pila Proof of Concept ha sido tooAzure cuyo nombre ha cambiado el Kit de desarrollo de pila.  Al igual que Hola prueba de concepto de pila de Azure, Kit de desarrollo de pila de Azure está dirigida toobe un desarrollo y entorno de evaluación usan características de Azure pila tooexplore y proporcionan una plataforma de desarrollo para la pila de Azure.

### <a name="whats-new"></a>Novedades
- Ahora puede usar recursos de pila de Azure 2.0 CLI toomanage desde una línea de comandos en sistemas operativos conocidos.
- Los tamaños de máquina virtual DSV2 permiten la portabilidad de plantilla entre Azure y Azure Stack.
- Operadores de la nube pueden obtener una vista previa experiencia de administración de capacidad de hello dentro de la hoja de administración de capacidad de Hola.
- Ahora puede usar datos de diagnóstico de toogather de extensión de diagnósticos de Azure de Hola de las máquinas virtuales.  La captura de estos datos resulta útil para analizar el rendimiento de la carga de trabajo y para investigar los problemas.
- Una nueva [experiencia de implementación](azure-stack-run-powershell-script.md) reemplaza los anteriores pasos generados por script para la implementación.  nueva experiencia de implementación Hola proporciona una interfaz gráfica comunes durante el ciclo de vida de hello toda la implementación.
- Ahora se admiten las cuentas Microsoft (MSA) durante la implementación.
- Ahora se admite Multi-Factor Authentication (MFA) durante la implementación.  Anteriormente, MFA debía deshabilitarse durante la implementación.

### <a name="known-issues"></a>Problemas conocidos
#### <a name="deployment"></a>Implementación
* Puede que observe que la implementación tarda más que en versiones anteriores. 
* Get-AzureStackLogs genera registros de diagnóstico, sin embargo, no iniciar la consola de toohello de progreso.
* Debe usar hello nueva [experiencia de implementación](azure-stack-run-powershell-script.md) toodeploy pila de Azure, o la implementación puede producir un error.

#### <a name="portal"></a>Portal
* Puede ver un panel en blanco en el portal de Hola.  Puede recuperar panel Hola seleccionando Hola engranaje en la esquina superior derecha del portal de Hola de hello, y seleccione "Restaurar la configuración predeterminada".
* Los inquilinos son marketplace completa de hello toobrowse pueda sin una suscripción y verán los elementos administrativos como planes y ofertas.  Estos elementos son tootenants no es funcional.
* Al seleccionar una instancia de rol de infraestructura, verá un error que muestra un error de referencia. Hello toorefresh de funcionalidad de actualización del explorador de Hola de uso del Portal de administración.
* botón de "mover" Hello está deshabilitado en la hoja de grupo de recursos de Hola.  Este es el comportamiento esperado, porque el movimiento de grupos de recursos entre suscripciones no se admite actualmente.
* Recibirá notificaciones repetidas para los elementos de Marketplace sindicados que hayan completado la descarga.
* No son suscripción de tooyour permisos tooview capaz de uso de portales de la pila de Azure de Hola.  Como solución alternativa, se pueden comprobar los permisos con Powershell.
* Debe agregar `-TenantID` como una marca al exportar una implementación completada como un script de automatización del portal de Hola.

#### <a name="services"></a>Services
* Servicios de almacén de claves se deben crear desde el portal del inquilino de Hola o API de inquilino.  Si se registran en como administrador, asegúrese de que toouse Hola inquilino portal toocreate que almacenes de credenciales de almacén de claves nuevo, secretos y las claves.
* No hay ninguna experiencia de Marketplace para crear conjuntos de escalado de máquinas virtuales, aunque se pueden crear mediante una plantilla.
* No se puede asociar un equilibrador de carga con una red de back-end mediante el portal de Hola.  Esta tarea se puede completar con PowerShell o con una plantilla.
* Los conjuntos de disponibilidad de la máquina virtual solo pueden configurarse con un dominio de error de uno y un dominio de actualización de uno.  
* Un inquilino debe tener una cuenta de almacenamiento antes de crear una nueva función de Azure Functions.
* Puede producir un error en la máquina virtual y el informe "no puede enlazar el argumento tooparameter 'Adaptador de red VM' porque es null."  Nueva implementación de máquina virtual de Hola se realiza correctamente.  
* La eliminación de las suscripciones del inquilino da como resultado recursos huérfanos.  Como alternativa, elimine primero los recursos del inquilino o todo grupo de recursos y, a continuación, elimine las suscripciones del inquilino. 
* Debe crear una regla NAT al crear un equilibrador de carga de red o recibirá un error cuando intente tooadd una regla NAT después de crea el equilibrador de carga de Hola.
* Los inquilinos pueden crear máquinas virtuales mayores de lo que permite la cuota.  Este comportamiento se debe a que las cuotas no se aplican.
* Los inquilinos son Hola determinada opción toocreate una máquina virtual con almacenamiento con redundancia geográfica.  Esta configuración hace que toofail de creación de máquina virtual.
* Esta operación puede tardar tooan hora antes de que los inquilinos pueden crear bases de datos en un nuevo SQL o MySQL SKU. 
* Creación de elementos directamente en SQL y servidores que no son realizados por el proveedor de recursos de Hola de hospedaje de MySQL no se admite y puede provocar un estado que no coinciden.
* AzureRM PowerShell 1.2.10 requiere pasos de configuración adicionales:
    * Ejecútelo después de ejecutar Add-AzureRMEnvironment para las implementaciones de Azure AD.  Indique los valores de nombre y GraphAudience de hello con valores obtenidos hello en `Add-AzureRMEnvironment`.
      
      ```PowerShell
      Set-AzureRmEnvironment -Name <Environment Name> -GraphAudience <Graph Endpoint URL>
      ```
    * Ejecútelo después de ejecutar Add-AzureRMEnvironment para las implementaciones de AD FS.  Indique los valores de nombre y GraphAudience de hello con valores obtenidos de hello `Add-AzureRMEnvironment`.
      
      ```PowerShell
      Set-AzureRmEnvironment <Environment Name> -GraphAudience <Graph Endpoint URL> -EnableAdfsAuthentication:$true
      ```
    
    Por ejemplo, siguiente Hola se utiliza para un entorno de Azure AD:

    ```PowerShell
      Set-AzureRmEnvironment AzureStack -GraphAudience https://graph.local.azurestack.external/
    ```

#### <a name="fabric"></a>Fabric
* proveedor de recursos de proceso de Hello muestra un estado desconocido.
* Hola, direcciones IP de BMC & modelo no se muestran en la información esencial de Hola de un nodo de la unidad de escala.  Este comportamiento es el esperado en Azure Stack Development Kit.
* acción de reinicio de Hello en función de infraestructura de controlador de proceso (instancia AzS XRP01) no debe usarse.
* hoja de copia de seguridad de infraestructura de Hello no debe usarse.
