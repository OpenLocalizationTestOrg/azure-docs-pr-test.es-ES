---
title: "aaaEncryption en almacén de Azure Data Lake | Documentos de Microsoft"
description: "Descripción del funcionamiento del cifrado y la rotación de claves en Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Cifrado de datos en Azure Data Lake Store

El cifrado en Azure Data Lake Store le ayuda a proteger sus datos, implementar directivas de seguridad de empresa y satisfacer los requisitos de cumplimiento normativo. En este artículo se proporciona información general de diseño de Hola y se describe algunos de los aspectos técnicos de Hola de implementación.

Data Lake Store admite el cifrado de datos tanto en reposo como en tránsito. En el caso de datos en reposo, Data Lake Store admite el cifrado transparente "activado de forma predeterminada". Con más detalle, esto significa:

* **De forma predeterminada**: cuando se crea una nueva cuenta de almacén de Data Lake, el valor predeterminado es Hola habilita el cifrado. Por lo tanto, los datos que se almacenan en el almacén de Data Lake siempre están toostoring anterior cifrado en medios persistentes. Este es el comportamiento de Hola para todos los datos y no se puede cambiar después de crear una cuenta.
* **Transparente**: almacén de Data Lake automáticamente cifra datos anteriores toopersisting y descifra los datos anteriores tooretrieval. cifrado de Hola se configura y administra en el nivel de almacén de Data Lake Hola por un administrador. No se realizan cambios datos toohello acceder a las API. Por lo tanto, no se requiere ningún cambio en las aplicaciones y los servicios que interactúan con Data Lake Store a causa del cifrado.

Los datos en tránsito (también conocidos como datos en movimiento) también se cifran siempre en Data Lake Store. Por otra parte media toopersistent de tooencrypting datos toostoring anterior, Hola datos están protegidos también siempre a través de HTTPS en tránsito. HTTPS es Hola único protocolo admitido para hello que REST de almacén de datos Lake interfaces. Hello diagrama siguiente muestra cómo se convierte en cifra los datos en el almacén de Data Lake:

![Diagrama de cifrado de datos en Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Configuración del cifrado con Data Lake Store

El cifrado para Data Lake Store se configura durante la creación de la cuenta y siempre está habilitado de forma predeterminada. Puede administrar las claves de hello usted mismo o permitir que el almacén de Data Lake toomanage para que (Esto es predeterminado de hello).

Para más información, consulte [Introducción](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

## <a name="how-encryption-works-in-data-lake-store"></a>Funcionamiento del cifrado en Data Lake Store

Hello siguiente información cubre cómo claves de cifrado maestra toomanage y explica Hola tres tipos diferentes de teclas que puede utilizar en el cifrado de datos de almacén de Data Lake.

### <a name="master-encryption-keys"></a>Claves de cifrado maestras

Data Lake Store proporciona dos modos de administración de claves de cifrado maestras (MEK). Por ahora, suponga que clave de cifrado maestra hello es clave de nivel superior de Hola. Clave de cifrado maestra toohello de acceso es necesario toodecrypt los datos almacenados en el almacén de Data Lake.

modos de Hello dos para administrar la clave de cifrado maestra Hola son los siguientes:

*   Claves administradas por el servicio
*   Claves administradas por el cliente

En ambos modos, clave de cifrado maestra Hola se protege mediante el almacenamiento en el almacén de claves de Azure. El almacén de claves es un servicio completamente administrado y altamente seguro en Azure que puede ser claves criptográficas toosafeguard usado. Para más información, consulte [Key Vault](https://azure.microsoft.com/services/key-vault).

Ésta es una breve comparación de capacidades que proporcionan dos modos de Hola de administrar MEKs Hola.

|  | Claves administradas por el servicio | Claves administradas por el cliente |
| --- | --- | --- |
|¿Cómo se almacenan los datos?|Siempre cifrado toobeing anterior almacenado.|Siempre cifrado toobeing anterior almacenado.|
|¿Dónde se almacena la clave de cifrado maestra Hola?|Key Vault|Key Vault|
|¿Son cualquier cifrado de claves almacenadas en hello borrar fuera de almacén de claves? |No|No|
|¿Hola MEK se puede recuperar el almacén de claves?|No. Después de hello que MEK se almacena en el almacén de claves, solo se puede utilizar para el cifrado y descifrado.|No. Después de hello que MEK se almacena en el almacén de claves, solo se puede utilizar para el cifrado y descifrado.|
|¿Quién posee instancia del almacén de claves de Hola y Hola MEK?|Hola servicio de almacén de Data Lake|Es propietario de instancia de almacén de claves de hello, que pertenece a su propia suscripción de Azure. Hola MEK en el almacén de claves puede administrarse mediante software o hardware.|
|¿Puede revocar el acceso toohello MEK para hello servicio de almacén de Data Lake?|No|Sí. Puede administrar listas de control de acceso en el almacén de claves y quitar la identidad del servicio de toohello acceso control entradas para el servicio de almacén de Data Lake Hola.|
|¿Puede eliminar permanentemente hello MEK?|No|Sí. Si elimina hello MEK desde el almacén de claves, no se puede descifrar datos Hola Hola cuenta de almacén de Data Lake por cualquier usuario, incluido el servicio de almacén de Data Lake Hola. <br><br> Si explícitamente hecho hello MEK anterior toodeleting, desde el almacén de claves, se puede restaurar hello MEK y, a continuación, se pueden recuperar datos de Hola. Sin embargo, si no no hecho hello MEK anterior toodeleting, desde el almacén de claves, Hola Hola cuenta de almacén de Data Lake no pueden nunca se descifran datos a partir de ahí.|


Además de esta diferencia de que administra hello MEK e instancia de almacén de claves de hello en el que reside, rest Hola de diseño de Hola Hola mismo para ambos modos.

Es importante tooremember siguiente de hello cuando se elige el modo de Hola para hello las claves de cifrado maestra:

*   Puede elegir si toouse administradas por el cliente claves o servicio administrado al aprovisionar una cuenta de almacén de Data Lake.
*   Después de aprovisiona una cuenta de almacén de Data Lake, no se puede cambiar el modo de saludo.

### <a name="encryption-and-decryption-of-data"></a>Cifrado y descifrado de datos

Hay tres tipos de claves que se utilizan en el diseño de Hola de cifrado de datos. Hello en la tabla siguiente proporciona un resumen:

| Clave                   | Abreviatura | Asociada a | Ubicación de almacenamiento                             | Escriba       | Notas                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Clave de cifrado maestra | MEK          | Cuenta de Data Lake Store | Key Vault                              | Asimétrica | Puede administrarla Data Lake Store o usted.                                                              |
| Clave de cifrado de datos   | DEK          | Cuenta de Data Lake Store | Almacenamiento persistente, administrada por el servicio Data Lake Store | Simétrica  | Hola DEK se cifra mediante hello MEK. Hola que DEK cifrada es lo que se almacena en medios persistentes. |
| Clave de cifrado de bloque  | BEK          | Un bloque de datos | None                                         | Simétrica  | Hola BEK se deriva de bloque de datos de Hola y de saludo DEK.                                                      |

Hola siguiente diagrama muestra estos conceptos:

![Claves de cifrado de datos](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Algoritmo de seudoprueba si hay un archivo toobe descifrado:
1.  Comprobar si Hola DEK para cuenta de almacén de Data Lake hello es almacenada en caché y preparado para su uso.
    - Si no es así, leer Hola cifra la DEK desde el almacenamiento persistente y enviarlo tooKey almacén toobe descifrado. Hola de caché descifra la DEK en memoria. Ahora está listo toouse.
2.  Para cada bloque de datos en el archivo hello:
    - Hola de lectura cifrarse bloque de datos desde el almacenamiento persistente.
    - Generar hello BEK de hello DEK y bloque cifrado de Hola de datos.
    - Usar datos de hello BEK toodecrypt.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Algoritmo de seudoprueba cuando un bloque de datos cifrado de toobe:
1.  Comprobar si Hola DEK para cuenta de almacén de Data Lake hello es almacenada en caché y preparado para su uso.
    - Si no es así, leer Hola cifra la DEK desde el almacenamiento persistente y enviarlo tooKey almacén toobe descifrado. Hola de caché descifra la DEK en memoria. Ahora está listo toouse.
2.  Generar un BEK único para el bloque de Hola de datos a partir de hello DEK.
3.  Cifrar el bloque de datos de hello con hello BEK, mediante el uso de cifrado AES-256.
4.  Bloque de datos cifrados de Hola de almacén de datos en el almacenamiento persistente.

> [!NOTE] 
> Por motivos de rendimiento Hola borrar DEK Hola se almacena en caché en memoria durante un período corto e inmediatamente se borra después. En medios persistentes, siempre se almacena cifrada mediante hello MEK.

## <a name="key-rotation"></a>Rotación de claves

Cuando se usa claves administradas por el cliente, puede girar hello MEK. toolearn tooset una cuenta de almacén de Data Lake con claves administradas por el cliente, vea [Introducción](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Requisitos previos

Al configurar la cuenta de almacén de Data Lake hello, eligió toouse sus propias claves. Esta opción no se puede cambiar una vez creada la cuenta de hello. Hello pasos siguientes se supone que se utilizan claves administradas por el cliente (es decir, que haya elegido sus propias claves de almacén de claves).

Tenga en cuenta que si utiliza opciones predeterminadas de hello para el cifrado, los datos siempre se cifran mediante claves administradas por el almacén de Data Lake. En esta opción, no tiene claves de toorotate de capacidad de hello, que son administrados por el almacén de Data Lake.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>¿Cómo toorotate Hola MEK en almacén de Data Lake

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Examinar la instancia del almacén de claves toohello que almacena las claves asociadas a su cuenta de almacén de Data Lake. Seleccione **Claves**.

    ![Captura de pantalla de Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Seleccionar clave de hello asociada con su cuenta de almacén de Data Lake y crear una nueva versión de esta clave. Tenga en cuenta que almacén de Data Lake actualmente solo admite la rotación de claves tooa nueva versión de una clave. No es compatible con la rotación tooa otra clave.

   ![Captura de pantalla de la ventana Claves, donde se resalta Nueva versión](./media/data-lake-store-encryption/keynewversion.png)

4.  Busque la cuenta de almacenamiento de almacén de Data Lake toohello y seleccione **cifrado**.

    ![Captura de pantalla de la ventana de la cuenta de almacenamiento de Data Lake Store, con Cifrado resaltado](./media/data-lake-store-encryption/select-encryption.png)

5.  Un mensaje le notifica que hay una nueva versión de clave de la clave de Hola. Haga clic en **rotar la clave de** toohello clave nueva versión de hello de tooupdate.

    ![Captura de pantalla de la ventana Data Lake Store con el mensaje y Rotar clave resaltado](./media/data-lake-store-encryption/rotatekey.png)

Esta operación tardará menos de dos minutos y no hay ningún tiempo de inactividad previsto debido tookey rotación. Una vez completada la operación de hello, la nueva versión de hello de clave de hello está en uso.
