---
title: seguridad de serie 8000 aaaStorSimple | Documentos de Microsoft
description: "Describe las características de privacidad que protegen el servicio de StorSimple, dispositivo y datos de forma local y en la nube de Hola y seguridad Hola."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 48dd449d2908c21fe05d0ed37a4dc6f3e306e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>Protección de datos y seguridad de StorSimple

## <a name="overview"></a>Información general

La seguridad es una preocupación clave para cualquier persona que va a adoptar una nueva tecnología, especialmente cuando se usa tecnología de hello con datos confidenciales o propios. A medida que evalúa distintas tecnologías, debe considerar mayores riesgos y costes para la protección de datos. StorSimple de Microsoft Azure proporciona tanto una solución de seguridad y privacidad para la protección de datos, ayudando a tooensure:

* **Confidencialidad** solo las entidades autorizadas pueden ver los datos.
* **Integridad** : solo las entidades autorizadas pueden modificar o eliminar los datos.

Hola solución de StorSimple de Microsoft Azure está formada por cuatro componentes principales que interactúan entre sí:

* **Servicio de administrador de dispositivos de StorSimple hospedado en Microsoft Azure** : usar tooconfigure y aprovisionar el servicio de administración de Hola Hola dispositivo StorSimple.
* **Dispositivo de StorSimple** : un dispositivo físico instalado en el centro de datos. Todos los hosts y los clientes que generan datos de conectan el dispositivo de StorSimple toohello y dispositivo Hola administra datos hello y pasa toohello nube de Azure según corresponda.
* **Clientes/hosts conectados toohello dispositivo** : Hola clientes en la infraestructura que se conectan toohello dispositivo de StorSimple y generar datos que es necesario toobe protegido.
* **Almacenamiento en nube** : Hola ubicación Hola donde se almacenan los datos de nube de Azure.

Hello las secciones siguientes describen características de seguridad de StorSimple de Hola que ayudan a proteger cada uno de estos componentes y los datos de hello almacenados en ellas. También incluye una lista de preguntas que puede tener sobre seguridad de Microsoft Azure StorSimple y sus correspondientes respuestas Hola.

## <a name="storsimple-device-manager-service-protection"></a>Protección del servicio StorSimple Device Manager

Hola servicio Administrador de dispositivos de StorSimple es un servicio de administración hospedado en Microsoft Azure y utiliza toomanage todos los dispositivos de StorSimple que la organización ha adquirido. Puede tener acceso a Hola servicio Administrador de dispositivos de StorSimple mediante su toolog de credenciales de la organización en toohello portal de Azure a través de un explorador web.

Acceso toohello servicio de administrador de dispositivos de StorSimple requiere que su organización tiene una suscripción de Azure que comprenda StorSimple. La suscripción rige las características de Hola que puede tener acceso en hello portal de Azure. Si su organización no tiene una suscripción de Azure y desea toolearn más información acerca de esto, consulte [suscribirse a Azure como organización](../active-directory/sign-up-organization.md).

Como Hola servicio Administrador de dispositivos de StorSimple se hospeda en Azure, está protegido por las características de seguridad de Azure de Hola. Para obtener más información acerca de las características de seguridad de hello proporcionadas por Microsoft Azure, visite toohello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>Protección del dispositivo de StorSimple

dispositivo de StorSimple de Hello es un dispositivo de almacenamiento de híbrido local que contiene unidades de estado sólido (SSD) y unidades de disco duro (HDD) junto con controladoras redundantes y capacidades de conmutación por error automática. controladores de Hello administran el almacenamiento niveles, al colocar actualmente usados (o activos) los datos en el almacenamiento local (en el dispositivo StorSimple de Hola o servidores locales), mientras se mueve en la nube toohello datos utilizados con menos frecuencia.

Solo los autorizados StorSimple dispositivos pueden toojoin Hola servicio Administrador de dispositivos de StorSimple que creó en la suscripción de Azure. tooauthorize un dispositivo, debe registrar con el servicio de administrador de dispositivos de StorSimple de hello proporcionando la clave de registro del servicio de Hola. clave de registro del servicio de Hello es una clave aleatoria de 128 bits generada en hello portal de Azure.

![Clave de registro del servicio](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn cómo obtener un go de clave, de registro de servicio demasiado[paso 2: clave de registro del servicio de Get hello](storsimple-8000-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).

clave de registro del servicio de Hello es una clave larga que contiene 100 caracteres. Puede copiar la clave de Hola y guardarla en un archivo de texto en una ubicación segura para que se pueden usar dispositivos adicionales tooauthorize según sea necesario. Si la clave de registro del servicio de Hola se pierde después de registrar su primer dispositivo, puede generar una nueva clave de hello servicio Administrador de dispositivos de StorSimple. Esto no afectará a operación Hola de dispositivos existentes.

Después de registra un dispositivo, utiliza tokens toocommunicate con Microsoft Azure. no se utiliza la clave de registro del servicio de Hello después del registro de dispositivo.

> [!NOTE]
> Se recomienda regenerar la clave de registro del servicio de hello después de cada uso.


## <a name="protect-your-storsimple-solution-via-passwords"></a>Protección de la solución de StorSimple mediante contraseñas

Las contraseñas son un aspecto importante de seguridad del equipo y se usa ampliamente en la solución de StorSimple de hello toohelp Asegúrese de que los datos están accesible tooauthorized exclusivamente a los usuarios. StorSimple permite hello tooconfigure siguientes contraseñas:

* Contraseña para el administrador del dispositivo de StorSimple
* Contraseñas para iniciador y destino del Protocolo de autenticación por desafío mutuo (CHAP)
* Contraseña para StorSimple Snapshot Manager

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Windows PowerShell para StorSimple y Hola contraseña de administrador de dispositivos de StorSimple

Windows PowerShell para StorSimple es una interfaz de línea de comandos que puede usar el dispositivo de StorSimple de toomanage Hola. Windows PowerShell para StorSimple tiene características que le permiten tooregister el dispositivo, configure la interfaz de red de hello en el dispositivo, instalar a ciertos tipos de actualizaciones, solucionar problemas en el dispositivo mediante el acceso a la sesión de soporte técnico de Hola y cambiar el estado del dispositivo de Hola . Puede tener acceso a Windows PowerShell para StorSimple conexión toohello la consola serie en el dispositivo de Hola o mediante la comunicación remota de Windows PowerShell.

La comunicación remota de PowerShell se puede realizar a través de HTTPS o HTTP. Si está habilitada la administración remota a través de HTTPS, deberá administración remota de hello toodownload certificado de dispositivo de hello e instalarlo en el cliente remoto Hola. Para obtener más información acerca de la comunicación remota de PowerShell, vaya demasiado[conectarse de forma remota el dispositivo de StorSimple tooyour](storsimple-8000-remote-connect.md).

Después de usar Windows PowerShell para StorSimple tooconnect toohello dispositivo, necesitará toolog tooprovide Hola dispositivo administrador contraseña en dispositivo toohello.

![Contraseña de administrador de dispositivo](./media/storsimple-security/DeviceAdminPW.png)

Mantener Hola seguir las prácticas recomendadas en cuenta:

* La administración remota está desactivada de manera predeterminada. Puede utilizar tooenable de servicio del Administrador de dispositivos de StorSimple de Hola. Como práctica recomendada de seguridad, se debe habilitar acceso remoto únicamente durante Hola período de tiempo que sea estrictamente necesario.
* Si cambia la contraseña de hello, ser seguro toonotify todos los usuarios de acceso remoto para que no sufran una pérdida de conectividad inesperada.
* Hola servicio Administrador de dispositivos de StorSimple no puede recuperar las contraseñas existentes: solo puede restablecer. Se recomienda que almacene todas las contraseñas en un lugar seguro para que no tenga tooreset una contraseña si olvido. Si necesita tooreset una contraseña, que seguro toonotify todos los usuarios antes de hacerlo.

Puede tener acceso a la interfaz de Windows PowerShell de hello mediante un dispositivo de toohello conexión serie. También puede tener acceso remoto si utiliza HTTP o HTTPS, lo que proporciona mayor seguridad. HTTPS proporciona un nivel de seguridad más alto que una conexión serie o HTTP. Sin embargo, toouse HTTPS, debe primero instalar un certificado en equipos de cliente de Hola que tendrá acceso a dispositivo de Hola. Puede descargar el certificado de acceso remoto de Hola desde la página de configuración de dispositivo de Hola Hola servicio Administrador de dispositivos de StorSimple. Si se pierde el certificado de hello para el acceso remoto, debe descargar un nuevo certificado y propagar a los clientes de tooall que están autorizados toouse de administración remota.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Contraseñas para iniciador y destino del Protocolo de autenticación por desafío mutuo (CHAP)

CHAP es un esquema de autenticación utilizado por hello identidad de hello del dispositivo StorSimple de toovalidate de clientes remotos. comprobación de Hola se basa en una contraseña compartida. CHAP puede ser unidireccional o mutuo (bidireccional). Con el CHAP unidireccional, el destino de hello (dispositivo de StorSimple de hello) autentica un iniciador (host). CHAP bidireccional o mutuo requiere que el destino de hello autentique el iniciador de hello y, a continuación, el iniciador de hello autenticar destino Hola. StorSimple puede ser cualquiera de los métodos de toouse configurado.

Tenga en cuenta los siguiente hello cuando configure CHAP:

* nombre de usuario CHAP Hola debe contener menos de 233 caracteres.
* Contraseña CHAP de Hello debe tener entre 12 y 16 caracteres. Intentar toouse un nombre de usuario o una contraseña más larga se producirá un error de autenticación en el host de Windows hello.
* No se puede usar hello misma contraseña para el iniciador CHAP hello y el destino CHAP Hola.
* Después de establecer contraseña de hello, se puede cambiar pero no se puede recuperar. Si se cambia la contraseña de hello, ser seguro toonotify todos los usuarios de acceso remoto para que puedan conectarse sin problemas toohello dispositivo de StorSimple.

Para obtener más información acerca de CHAP y cómo tooconfigure como parte de la solución StorSimple, vaya demasiado[configurar CHAP para el dispositivo StorSimple](storsimple-8000-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>Contraseña para StorSimple Snapshot Manager

Administrador de instantáneas de StorSimple es un complemento de Microsoft Management Console (MMC) que usa grupos de volúmenes y copias de seguridad coherentes con la aplicación de hello Windows Volume Shadow Copy Service toogenerate. Además, puede usar la clonación y programaciones de copia de seguridad de administrador de instantáneas StorSimple toocreate o restaurar volúmenes.

Cuando se configura un administrador de instantáneas StorSimple toouse de dispositivo, podrá tooprovide requiere la contraseña del Administrador de instantáneas de StorSimple Hola. Esta contraseña se establece primero en Windows PowerShell para StorSimple durante el registro. contraseña Hello también puede establecer y cambiar de hello servicio Administrador de dispositivos de StorSimple. Esta contraseña autentica el dispositivo de hello con el Administrador de instantáneas de StorSimple.

![Contraseña para StorSimple Snapshot Manager](./media/storsimple-security/SnapshotMgrPassword.png)

contraseña de administrador de instantáneas StorSimple Hola debe tener 14 caracteres too15 y debe contener 3 o más de una combinación de caracteres en mayúsculas, minúsculas, numéricos y especiales. Después de establecer contraseña de administrador de instantáneas StorSimple hello, se puede cambiar pero no se puede recuperar. Si cambia la contraseña de hello, ser seguro toonotify todos los usuarios remotos.

Para obtener más información sobre el Administrador de instantáneas de StorSimple, vaya demasiado[¿qué es el Administrador de instantáneas StorSimple?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Procedimientos recomendados sobre las contraseñas

Le recomendamos que use siguiente Hola directrices toohelp Asegúrese de que las contraseñas de StorSimple son seguras y están bien protegidas:

* Cambie las contraseñas cada tres meses. Cambiar las contraseñas de Hola se aplica cada año.
* Use contraseñas seguras. Para obtener más información, consulte demasiado[crear contraseñas más seguras y protegerlos](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Use siempre contraseñas diferentes para mecanismos de acceso diferentes; cada una de las contraseñas de Hola que especifique debe ser única.
* No comparta las contraseñas con nadie que no sea el dispositivo de StorSimple de hello tooaccess autorizados.
* No hable acerca de una contraseña junto a otros o revele formato Hola de una contraseña.
* Si sospecha que una cuenta o contraseña se ha puesto en peligro, informar de departamento de seguridad de información de incidente tooyour Hola.
* Considere todas las contraseñas como información confidencial y sensible. 

## <a name="storsimple-data-protection"></a>Protección de datos de StorSimple

Esta sección describen las características de seguridad de StorSimple de Hola que protegen los datos en tránsito y los datos almacenados.

Como se describe en otras secciones, las contraseñas son tooauthorize usado y autentican a los usuarios para poder tener acceso tooyour StorSimple solución. Otra consideración de seguridad es la protección de los datos ante usuarios no autorizados mientras se transfieren entre sistemas de almacenamiento y mientras se almacenan. Hello las secciones siguientes describen características de protección de datos de hello proporcionadas con StorSimple.

> [!NOTE]
> La desduplicación de proporciona protección adicional para los datos almacenados en el dispositivo de StorSimple de Hola y de almacenamiento de Microsoft Azure. Cuándo se desduplican los datos, objetos de datos de Hola se almacenan independientemente de hello metadatos utilizados toomap y tener acceso a ellos: hay ningún dato de hello tooreconstruct de contexto de nivel de almacenamiento disponibles en función de la estructura del volumen, el sistema de archivos o el nombre de archivo.


## <a name="protect-data-flowing-through-hello-service"></a>Proteger los datos que fluyen a través del servicio Hola

propósito principal de Hola de hello servicio Administrador de dispositivos de StorSimple es toomanage y configurar el dispositivo de StorSimple Hola. Hola servicio Administrador de dispositivos de StorSimple se ejecuta en Microsoft Azure. Usar datos de configuración de dispositivo de Azure tooenter portal hello y, a continuación, Microsoft Azure usa el dispositivo de toohello datos de hello toosend de servicio Administrador de dispositivos de StorSimple de Hola. Usos de StorSimple un sistema de pares de claves asimétricas toohelp Asegúrese de que no darán como resultado un riesgo de hello servicio de Azure en una situación de riesgo almacenan información.

![Cifrado de datos a bordo](./media/storsimple-security/DataEncryption.png)

sistema de clave asimétrica Hola ayuda a proteger los datos de Hola que fluye a través del servicio hello como sigue:

1. Un certificado de cifrado de datos que utiliza un par de claves público y privado asimétricas se genera en el dispositivo de Hola y datos de hello tooprotect usado. Hola claves se generan cuando se registra el primer dispositivo de Hola.
2. claves de certificado de cifrado de datos de Hola se exportan a un archivo de intercambio de información Personal (.pfx) que está protegido por hello servicio datos clave de cifrado, que es una clave segura de 128 bits generada aleatoriamente por el primer dispositivo de Hola durante el registro.
3. clave pública de Hello del certificado de Hola de forma segura estará disponible toohello servicio de administrador de dispositivos de StorSimple y clave privada de hello permanece en el dispositivo de Hola.
4. Hola de datos Iniciando servicio Hola se cifra con clave pública y descifrar utilizando la clave privada de hello almacenada en el dispositivo de hello, asegurarse de esa Hola servicio de Azure no puede descifrar los datos de Hola que fluyen toohello dispositivo.

se genera la clave de cifrado de datos del servicio de Hello en sólo Hola el primer dispositivo registrado con el servicio de Hola. Todos los dispositivos subsiguientes que están registrados con el servicio de hello deben usar hello misma clave de cifrado de datos de servicio.

> [!IMPORTANT]
> Es muy importante toomake una copia de la clave de cifrado de datos del servicio de Hola y guárdelo en una ubicación segura. Una copia de la clave de cifrado de datos del servicio de hello debe almacenarse de forma que puede tener acceso a una persona autorizada y puede ser el Administrador de dispositivos de toohello comunicado fácilmente.
> 
> Si se pierde la clave de cifrado de datos del servicio de hello, una persona de soporte técnico de Microsoft puede ayudarle a tooretrieve proporcionado que tienen al menos un dispositivo en un estado en línea. Se recomienda cambiar la clave de cifrado de datos del servicio de hello después de haberlos recuperado. Para obtener instrucciones, vaya demasiado[clave de cifrado de datos del servicio de cambio hello](storsimple-service-dashboard.md#change-the-service-data-encryption-key).

Puede cambiar la clave de cifrado de datos del servicio de Hola y el correspondiente certificado de cifrado de datos Hola seleccionando hello **la clave de cifrado de datos del servicio de cambio** opción en el panel de servicio de Hola. tooensure que la seguridad de los datos no se ve comprometida, debe usar una físico StorSimple dispositivo toochange Hola servicio datos clave de cifrado. El cambio de claves de cifrado de Hola requiere que todos los dispositivos se actualicen con una clave nueva Hola. Por lo tanto, recomendamos que cambie la clave de hello cuando todos los dispositivos están en línea. Si los dispositivos están sin conexión, es posible que las claves cambien en momentos distintos. dispositivos de Hello con claves antiguas seguirán toorun capaz de copias de seguridad, pero no se toorestore capaz de datos hasta que se actualiza la clave de Hola. Para obtener más información, consulte demasiado[panel de servicio de administrador de dispositivos de StorSimple de uso hello](storsimple-8000-service-dashboard.md).

la clave de cifrado de datos del servicio de Hola y el certificado de cifrado de datos de hello no expiran. Sin embargo, se recomienda que cambie el cifrado de datos del servicio de hello clave anualmente toohelp evitar poner en peligro clave.

## <a name="protect-data-at-rest"></a>Protección de los datos en reposo

dispositivo de StorSimple de Hello administra datos almacenándolos en capas localmente y en la nube de hello, según su frecuencia de uso. Todos los equipos que están conectados toohello dispositivo envío datos toohello dispositivo, lo que, a continuación, mueve datos toohello en la nube, según corresponda de host. Se transfieren datos de nube de hello dispositivo toohello forma segura a través de Internet de Hola. Cada dispositivo tiene un destino de iSCSI que expone todos los volúmenes compartidos en ese dispositivo. Todos los datos se cifran antes de enviarse toocloud almacenamiento. 

![Clave de cifrado de almacenamiento en la nube](./media/storsimple-security/CloudStorageEncryption.png)

toohelp garantizar la seguridad de Hola y la integridad de los datos mueve toohello en la nube, StorSimple permite las claves de cifrado de almacenamiento de toodefine en la nube como se indica a continuación:

* Especificar clave de cifrado de almacenamiento de nube de hello cuando se crea un contenedor de volúmenes. clave de Hello no se puede modificar o agregar más adelante.
* Hola a todos los volúmenes en un recurso compartido de contenedor de volumen misma clave de cifrado. Si desea una forma diferente de cifrado para un volumen específico, se recomienda crear un nuevo toohost de contenedor de volumen en dicho volumen.
* Al especificar clave de cifrado de almacenamiento de nube de Hola Hola servicio Administrador de dispositivos de StorSimple, clave de Hola se cifra con hello parte pública de la clave de cifrado de datos del servicio de hello y, a continuación, envía toohello dispositivo.
* clave de cifrado de almacenamiento de Hello en la nube no se almacena en el servicio de Hola y se conoce sólo funciona como dispositivo toohello.
* Especificar una clave de cifrado de almacenamiento en la nube es opcional. Puede enviar datos que han sido cifrados en el dispositivo de hello host toohello.

### <a name="additional-security-best-practices"></a>Prácticas recomendadas de seguridad adicionales

* División de tráfico: aísle la SAN iSCSI del tráfico de usuario en una LAN corporativa mediante la implementación de una red totalmente separada y a través de VLAN donde el aislamiento físico no es opción. Una red dedicada para el almacenamiento iSCSI garantizará la seguridad de Hola y el rendimiento de los datos críticos para la empresa. No se recomienda combinar el tráfico de usuario y almacenamiento en una LAN corporativa y puede aumentar la latencia y provocar errores en la red.
* Para la seguridad de la red en el lado host, utilice interfaces de red que admitan el motor de descarga de TCP/IP (TOE). TOE reduce la carga de la CPU procesando TCP en el adaptador de red de Hola.

## <a name="protect-data-via-storage-accounts"></a>Protección de datos a través de cuentas de almacenamiento

Cada suscripción de Microsoft Azure puede crear una o más cuentas de almacenamiento. (Una cuenta de almacenamiento proporciona un espacio de nombres único para trabajar con datos almacenados en la nube de Azure hello). Cuenta de almacenamiento de tooa de acceso se controla mediante claves de acceso y suscripción de hello asociadas con esa cuenta de almacenamiento.

Cuando se crea una cuenta de almacenamiento, Microsoft Azure genera dos claves de acceso de almacenamiento de 512 bits, uno de los cuales se utiliza para la autenticación cuando accede a la cuenta de almacenamiento de hello de dispositivo de StorSimple Hola. Observe que solo se usa una de estas claves. Hello otra se mantiene en reserva, lo que permite claves hello toorotate periódicamente. las claves de toorotate, asegúrese de clave secundaria de hello active y, a continuación, la clave principal de Hola de eliminación. A continuación, puede crear una nueva clave para su uso durante la siguiente rotación de Hola. (Por motivos de seguridad, muchos centros de datos requieren que las claves se roten).

Se recomienda seguir estos procedimientos recomendados para la rotación de claves:

* Conviene Rotar claves cuenta de almacenamiento con regularidad toohelp asegurarse de que la cuenta de almacenamiento no tiene acceso a usuarios no autorizados.
* Periódicamente, el Administrador de Azure debe cambiar o volver a generar clave primaria o secundaria de hello mediante el uso de la sección de almacenamiento de Hola de hello cuenta de almacenamiento de Azure toodirectly portal acceso Hola.

## <a name="protect-data-via-encryption"></a>Protección de datos mediante cifrado

StorSimple usa Hola posteriores tooprotect datos almacenados en los algoritmos de cifrado o desplazan entre los componentes de saludo de la solución StorSimple.

| Algoritmo | Longitud de la clave | Protocolos/aplicaciones/comentarios |
| --- | --- | --- |
| RSA |2048 |Hola tooencrypt portal Azure datos de configuración que se envían toohello dispositivo usa RSA PKCS 1 v1.5: por ejemplo, almacenamiento de credenciales, configuración de dispositivo de StorSimple, la cuenta y las claves de cifrado de almacenamiento en la nube. |
| AES |256 |AES con CBC es la parte pública de hello tooencrypt usado de la clave de cifrado de datos del servicio de hello antes de enviarlo toohello portal de Azure desde el dispositivo de StorSimple Hola. También se utiliza con datos de tooencrypt de dispositivo de StorSimple de hello antes de enviar datos de hello toohello cuenta de almacenamiento de nube. |

## <a name="storsimple-cloud-appliance-security"></a>Seguridad de StorSimple Cloud Appliance

[!INCLUDE [storsimple Cloud Appliance security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Preguntas más frecuentes

Hola continuación se indican algunas preguntas y respuestas sobre seguridad y StorSimple de Microsoft Azure.

**P:** Mi servicio se ha puesto en peligro. ¿Cuáles deben ser mis siguientes pasos?

**R:** debe cambiar inmediatamente la clave de cifrado de datos del servicio de Hola y claves de cuenta de almacenamiento de Hola Hola cuenta de almacenamiento que se está usando para apilar datos. Para obtener instrucciones, vaya a:

* [Cambiar la clave de cifrado de datos del servicio de Hola](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Rotación de claves de cuentas de almacenamiento](storsimple-8000-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**P: ¿** tengo un nuevo dispositivo de StorSimple que se pide la clave de registro del servicio de Hola. ¿Cómo la recupero?

**R:** esta clave se creó al crear servicio de administrador de dispositivos de StorSimple de Hola por primera vez. Cuando se usa el dispositivo de toohello de tooconnect del servicio de administrador de dispositivos de StorSimple de hello, puede usar tooview de página de inicio rápido de servicio de Hola o clave de registro del servicio de hello regenerar. Generar una nueva clave de registro de servicio no afectará a los dispositivos ya registrados de Hola. Para obtener instrucciones, vaya a:

* [Ver o volver a generar clave de registro del servicio de Hola](storsimple-8000-manage-service.md##regenerate-the-service-registration-key)

**P:** Perdí mi clave de cifrado de datos de servicio. ¿Qué puedo hacer?

**R:** Póngase en contacto con el soporte técnico de Microsoft. Puede registrar en la sesión de soporte técnico de tooa en el dispositivo y ayudarle a recuperar la clave de hello (siempre al menos un dispositivo está en línea). Inmediatamente después de obtener la clave de cifrado de datos del servicio de hello, debe cambiarlo tooensure esa clave nueva Hola se conoce solo tooyou. Para obtener instrucciones, vaya a:

* [Cambiar la clave de cifrado de datos del servicio de Hola](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**P: ¿** autorizado un dispositivo para un cambio de clave de cifrado de datos de servicio, pero no se inició el proceso de cambio de clave de Hola. ¿Cuál debo hacer?

**R:** si ha expirado el período de tiempo de espera de hello, necesitará tooreauthorize dispositivo de Hola para cambio de clave de cifrado de datos de servicio de Hola y vuelva a iniciar el proceso de Hola.

**P: ¿** he cambiado la clave de cifrado de datos del servicio de hello, pero no he podido tooupdate Hola otros dispositivos dentro de 4 horas. ¿Es necesario toostart nuevo?

**R:** Hola período de tiempo de 4 horas es solo para iniciar el cambio de Hola. Después de iniciar el proceso de actualización de hello en hello había autorizado dispositivo StorSimple, Hola autorización sigue siendo válida hasta que se actualizan todos los dispositivos.

**P: ¿** nuestro administrador de StorSimple ha dejado la empresa de Hola. ¿Cuál debo hacer?

**R:** cambie y restablezca las contraseñas que permiten el dispositivo de StorSimple de toohello de acceso y cambiar Hola servicio datos cifrado tooensure clave que Hola conozca la nueva información no toounauthorized personal de Hola. Para obtener instrucciones, vaya a:

* [Usar toochange de servicio del Administrador de dispositivos de StorSimple de hello las contraseñas de storsimple](storsimple-8000-change-passwords.md)
* [Cambiar la clave de cifrado de datos del servicio de Hola](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Configurar CHAP para el dispositivo StorSimple](storsimple-8000-configure-chap.md)

**P: ¿** quiero tooprovide Hola Administrador de instantáneas StorSimple contraseña tooa host que se conecta el dispositivo de StorSimple toohello, pero Hola contraseña no está disponible. ¿Qué puedo hacer?

**R:** si ha olvidado la contraseña de hello, debe crear uno nuevo. A continuación, asegúrese de tooinform todos los usuarios existentes que Hola contraseña se ha cambiado y que deben actualizar su clientes toouse Hola nueva contraseña. Para obtener instrucciones, vaya a:

* [Cambiar la contraseña de administrador de instantáneas StorSimple Hola](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)
* [Autenticar un dispositivo](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**P: ¿** certificado Hola para toohello de acceso remoto de Windows PowerShell para StorSimple se ha modificado en el dispositivo de Hola. ¿Cómo actualizo mis clientes de acceso remoto?

**R:** puede descargar el certificado nuevo de Hola de hello servicio Administrador de dispositivos de StorSimple y, después, proporcionarla toobe instalado en el almacén de certificados de Hola de los clientes de acceso remoto. Para obtener instrucciones, vaya a:

* [Cmdlet Import-Certificate](https://technet.microsoft.com/library/hh848630.aspx)

**P: ¿** Mis datos están protegidos si Hola servicio Administrador de dispositivos de StorSimple está en peligro?

**P:** Los datos de configuración del servicio se cifran siempre con su clave pública cuando accede a ella desde un explorador web. Porque el servicio de hello no tiene clave privada de acceso toohello, servicio de hello no puede ser capaz de toosee cualquier dato. Si Hola servicio Administrador de dispositivos de StorSimple está en peligro, no hay ningún efecto, ya que no han ningún claves almacenadas en hello servicio Administrador de dispositivos de StorSimple.

**P: ¿** si alguien logra el certificado de cifrado de datos de access toohello, los datos se verá comprometidos?

**R:** Microsoft Azure almacena la clave de cifrado de datos del cliente de hello (archivo .pfx) en un formato cifrado. Dado que se cifra el archivo .pfx de Hola y Hola servicio StorSimple no tiene archivo .pfx de hello servicio datos cifrado toodecrypt clave hello, simplemente obtener archivo de acceso toohello .pfx no expondrá ningún secreto.

**P:** ¿Qué ocurre si una entidad gubernamental pide mis datos a Microsoft?

**R:** porque todos los datos de Hola se cifran en el servicio de Hola y Hola clave privada se mantiene con el dispositivo de hello, hello gubernamental organismo debe solicitar al cliente hello datos Hola.

## <a name="next-steps"></a>Pasos siguientes

[Implementación del dispositivo de StorSimple](storsimple-8000-deployment-walkthrough-u2.md)

