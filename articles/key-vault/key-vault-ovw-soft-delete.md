---
ms.assetid: 
title: "eliminación temporal del almacén de claves de aaaAzure | Documentos de Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Información general sobre la eliminación temporal de Azure Key Vault

Característica de eliminación temporal del almacén de claves permite recuperar los almacenes de hello eliminado y objetos de almacén, conocidos como eliminación de software. En concreto, tratamos Hola los escenarios siguientes:

- Compatibilidad con la eliminación recuperable de una instancia de Key Vault
- Compatibilidad con la eliminación recuperable de objetos de Key Vault (por ejemplo, claves, secretos y certificados)

## <a name="supporting-interfaces"></a>Interfaces admitidas

Hello característica de eliminación de software inicialmente, está disponible a través de hello REST, .NET / interfaces de C# y PowerShell. Para obtener más información, consulte referencias toohello [referencia de almacén de claves](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Escenarios

Los almacenes Azure Key Vault son recursos controlados que se administran por medio de Azure Resource Manager. Azure Resource Manager especifica además un comportamiento bien definido para su eliminación, lo que conlleva que una operación DELETE ejecutada correctamente debería traducirse en que ese recurso deje de estar accesible. direcciones de la característica de eliminación de software de Hola Hola recuperación del objeto de hello eliminado, si la eliminación de hello ha sido accidental o intencionado.

1. En el escenario típico de hello, un usuario puede haber eliminado por accidente un almacén de claves o un objeto de almacén de claves; Si ese almacén de claves o clave del almacén de objeto estaban toobe recuperables durante un período predeterminado, usuario Hola puede deshacer la eliminación de Hola y recuperar sus datos.

2. En un escenario diferente, un usuario malintencionado puede intentar toodelete un almacén de claves o un objeto de almacén de claves, como una clave dentro de un almacén, toocause una interrupción del negocio. Separar la eliminación de hello del almacén de claves de Hola o del objeto de almacén de claves de eliminación real de Hola de hello datos subyacentes puede usarse como medida de seguridad, por ejemplo, restringen los permisos en tooa de eliminación de datos diferente, confianza rol. Este enfoque requiere un cuórum efectivo para una operación que, en caso contrario, podría provocar una pérdida de datos inmediata.

### <a name="soft-delete-behavior"></a>Comportamiento de eliminación temporal

Con esta característica, Hola operación DELETE en un almacén de claves o un objeto almacén de claves es una eliminación de software, eficazmente contienen recursos de Hola durante un período de retención determinada, mientras que aporta apariencia de hello ese objeto Hola se elimina. servicio de Hello aún más proporciona un mecanismo para recuperar el objeto de hello eliminado, básicamente deshaciendo la eliminación de Hola. 

La eliminación temporal es un comportamiento opcional de Key Vault y no **está habilitado de forma predeterminada** en esta versión. Para obtener más información acerca de cómo habilitar la eliminación de software para el almacén de claves, consulte las instrucciones específicas de hello en referencia de hello para la interfaz de Hola de su elección, [referencia de almacén de claves](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Recuperación de Key Vault

Tras eliminar un almacén de claves, servicio de hello crea un recurso de proxy en la suscripción de hello, agregar metadatos suficientes para la recuperación. recurso de proxy de Hola es un objeto almacenado, disponible en hello misma ubicación que el almacén de claves de hello eliminado. 

### <a name="key-vault-object-recovery"></a>Recuperación de un objeto de Key Vault

Cuando se elimina un objeto de almacén de claves, como una clave, servicio Hola colocará objeto hello en estado eliminado, lo que las operaciones de recuperación de tooany inaccesible. En este estado, objeto de almacén de claves de hello sólo puede aparecer, recuperada o forzosamente/eliminará de forma permanente. 

En hello mismo almacén de claves, tiempo programará eliminación Hola de hello subyacente toohello correspondiente de datos eliminado el almacén de claves o el objeto de almacén de claves para la ejecución después de un intervalo de retención predeterminado. Hola DNS registros toohello almacén correspondiente también se conserva durante Hola del intervalo de retención de saludo.

### <a name="soft-delete-retention-period"></a>Período de retención de la eliminación temporal

Los recursos eliminados temporalmente se conservan durante un período de tiempo determinado: 90 días. Durante el intervalo de retención de eliminación de software de hello, Hola después de aplicar:

- Puede enumerar todos los almacenes de claves de Hola y objetos de almacén de claves en estado de eliminación de software de hello para la suscripción, así como información de eliminación y recuperación de acceso sobre ellos.
    - Solo los usuarios con permisos especiales pueden consultar los almacenes eliminados. Se recomienda que los usuarios creen un rol personalizado con estos permisos especiales para tratar los almacenes eliminados.
- Un almacén de claves con hello no se puede crear el mismo nombre en hello indicarlo; en consecuencia, no se puede crear un objeto de almacén de claves en un almacén determinado si ese almacén de claves contiene un objeto con hello mismo nombre y que está en estado eliminado 
- Solo un usuario con privilegios en concreto puede restaurar un almacén de claves o un objeto de almacén de claves mediante la emisión de un comando de recuperación en el recurso de proxy correspondiente de Hola.
    - usuario de Hello, miembro del rol personalizado de hello, que tiene el privilegio de hello toocreate un almacén de claves en el grupo de recursos de Hola puede restaurar el almacén de Hola.
- Solo un usuario con privilegios específicamente a la fuerza puede eliminar un almacén de claves o un objeto de almacén de claves mediante la emisión de un comando de eliminación en el recurso de proxy correspondiente de Hola.

A menos que se recupera un almacén de claves o un objeto de almacén de claves, en hello final del servicio de Hola de intervalo de retención de hello realiza una purga de almacén de claves de hello eliminado o un objeto almacén de claves y su contenido. La eliminación de recursos no se puede volver a programar.

### <a name="permitted-purge"></a>Purga permitida

Permanentemente eliminar, purga, un almacén de claves es posible a través de una operación POST en el recurso de proxy de Hola y requiere privilegios especiales. Por lo general, solo el propietario de suscripción Hola será capaz de toopurge un almacén de claves. desencadenadores de operación POST de Hola Hola eliminación inmediata y no recuperable de ese almacén. 

Una excepción toothis si resulta que Hola Hola suscripción de Azure se ha marcado como *no eliminable*. En este caso, solo el servicio de hello, a continuación, puede realizar la eliminación real de Hola y lo hace como un proceso programado. 



