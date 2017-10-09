---
title: aaaMicrosoft cifrado en el resto de datos de Azure | Documentos de Microsoft
description: "Este artículo proporciona información general del cifrado de datos de Microsoft Azure en rest, Hola capacidades generales y consideraciones generales."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Cifrado en reposo de datos de Azure
Hay varias herramientas en los datos de Microsoft Azure toosafeguard según las necesidades de seguridad y cumplimiento de la compañía tooyour. Este documento se centra en cómo datos estén protegidos en rest a través de Microsoft Azure, describen Hola diversos componentes que participan en la implementación de protección de datos de Hola y revisan las ventajas y desventajas de métodos de protección de la administración de claves diferente Hola. 

El cifrado en reposo es un requisito de seguridad habitual. Una ventaja de Microsoft Azure es que las organizaciones pueden lograr cifrado en reposo sin necesidad de costo de Hola de implementación y el riesgo de hello y administración de una solución de administración de claves personalizados. Las organizaciones tienen la opción de Hola de permitir Azure administrar completamente el cifrado en reposo. Además, las organizaciones tienen varias tooclosely opciones Administrar cifrado ni claves de cifrado.

## <a name="what-is-encryption-at-rest"></a>¿Qué es el cifrado en reposo?
Cifrado en reposo hace referencia toohello criptográficos codificación (cifrado) de datos cuando se conservan. Hello cifrado en diseños de Rest de Azure use cifrado simétrico tooencrypt y descifrar grandes cantidades de datos rápidamente según el modelo conceptual sencillo de tooa:

- Una clave de cifrado simétrico es datos de uso tooencrypt tal y como se conservan 
- Hola la misma clave de cifrado es que los datos de uso toodecrypt tal y como lo preparamos para su uso en la memoria
- Se pueden particionar datos y se pueden usar claves diferentes para cada partición
- Las claves deben almacenarse en una ubicación segura con directivas de control de acceso limitar las identidades de toocertain de acceso y uso de claves de registro. Las claves de cifrado de datos a menudo se cifran con toofurther limitar el acceso de cifrado asimétrico (descrito en hello *clave jerarquía*, más adelante en este artículo)

Hola anterior describe elementos comunes de alto nivel Hola de cifrado en reposo. En la práctica, los escenarios de control y administración de la clave, así como las convicciones de escala y disponibilidad, requieren construcciones adicionales. A continuación se describen los componentes y conceptos del cifrado en reposo de Microsoft Azure.

## <a name="hello-purpose-of-encryption-at-rest"></a>propósito de Hola de cifrado en reposo
El cifrado en reposo es tooprovide previsto de protección de datos para datos en reposo (como se describió anteriormente.) Los ataques contra los datos en reposo incluyen el intentos del tooobtain acceso físico del hardware de los toohello en qué Hola se almacenan los datos y, a continuación, poner en peligro Hola contenía datos. En este tipo de ataque, unidad de disco duro de un servidor puede se maneja durante el mantenimiento, lo que permite a un atacante en unidad de disco duro tooremove Hola. Más adelante atacante Hola aplicaría unidad de disco duro de hello en un equipo con sus datos de control tooattempt tooaccess Hola. 

El cifrado en reposo es atacante de hello tooprevent diseñada tengan acceso a datos de hello sin cifrar asegurándose de hello datos se cifran en el disco. Si un atacante tooobtain cifra una unidad de disco duro con este tipo datos y no hay claves de cifrado de toohello de acceso, atacante hello no podría comprometer los datos de hello sin dificultad excelente. En este escenario, un atacante tendría tooattempt ataques contra los datos cifrados que son mucho más complejos y consumir recursos que si tuviera acceso sin cifrar datos en un disco duro. Por este motivo, el cifrado en reposo es muy recomendable y es un requisito de alta prioridad para muchas organizaciones. 

En algunos casos, también se requiere el cifrado en reposo como necesidad de la organización de los esfuerzos de cumplimiento y gobernanza de datos. Las normas gubernamentales y del sector, como HIPAA, PCI y FedRAMP, y los requisitos de regulación internacionales, diseñan las medidas de seguridad específicas a través de procesos y directivas relativas a los requisitos de protección y cifrado de datos. Para muchos de esos reglamentos, el cifrado en reposo es una medida obligatoria necesaria para la protección y administración de datos compatibles. 

Además toocompliance y requisitos de regulación, cifrado en reposo se debería percibir como una capacidad de la plataforma de defensa en profundidad. Aunque Microsoft proporciona una plataforma compatible para los servicios, aplicaciones, y datos, la instalación completa y la seguridad física, auditoría y control de acceso a datos, es importante tooprovide adicionales "superpuesta" las medidas de seguridad en caso de una de Hola medidas de otro seguridad produce un error. El cifrado en reposo proporciona un mecanismo de grupo defensivo adicional.

Microsoft está cifrado tooproviding Confirmar opciones de rest a través de servicios en la nube y de administración adecuado de los clientes de tooprovide de claves de cifrado y toologs de acceso que se muestra cuando se utilizan las claves de cifrado. Además, Microsoft está trabajando hacia el objetivo de Hola de hacer que todos los datos de clientes que se cifran en reposo de forma predeterminada.

## <a name="azure-encryption-at-rest-components"></a>Componentes del cifrado en reposo de Azure

Como se describió anteriormente, objetivo Hola de cifrado en reposo es que los datos que se guardan en el disco se cifran con una clave de cifrado secretas. tooachieve ese objetivo proteger creación de claves, almacenamiento, control de acceso y administración de se deben proporcionar las claves de cifrado de Hola. Aunque los detalles pueden variar, servicios de Azure cifrado en las implementaciones de Rest se pueden describir en términos de Hola por debajo de los conceptos que, a continuación, se ilustran en hello siguiente diagrama.

![Componentes](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Azure Key Vault

ubicación de almacenamiento de Hola de claves de cifrado de Hola y claves de toothose de control de acceso es tooan central de cifrado en el modelo de rest. las claves de Hello necesitan toobe muy protegida pero fáciles de administrar los usuarios especificados y los servicios de toospecific disponible. Para los servicios de Azure, el almacén de claves de Azure es Hola recomienda soluciones de almacenamiento de claves y proporciona una experiencia de administración comunes en los servicios. Las claves se almacenan y administran en los almacenes de claves, y se puede dar el almacén de claves de acceso tooa toousers o servicios. Azure Key Vault admite la creación del cliente de claves o importación de claves de cliente para su uso en escenarios de clave de cifrado administrada por el cliente.

### <a name="azure-active-directory"></a>Azure Active Directory

Claves de hello toouse permisos almacenado en el almacén de claves de Azure, toomanage o tooaccess para el cifrado en Rest cifrado y descifrado, puede indicarse tooAzure cuentas de Active Directory. 

### <a name="key-hierarchy"></a>Jerarquía de las claves

Normalmente se usa más de una clave de cifrado en una implementación de cifrado en reposo. El cifrado asimétrico es útil para establecer la confianza de Hola y autenticación necesaria para la administración y acceso a la clave. El cifrado simétrico es más eficaz para el cifrado masivo y descifrado, lo que permite un cifrado más seguro y un mejor rendimiento. Además, limitar el uso de Hola de un disminuye de clave de cifrado única riesgo de Hola que Hola clave se verá comprometida y Hola costo de volver a cifrar cuando se debe reemplazar una clave. ventajas de hello tooleverage de cifrado simétrico y asimétrico y limitar el uso de Hola y la exposición de una sola clave, el cifrado Azure en modelos de rest usar una jerarquía de claves que se compone de los siguientes tipos de claves de hello:

- **Clave de cifrado de datos (DEK)** : una clave simétrica de AES256 usa tooencrypt una partición o un bloque de datos.  Un único recurso puede tener muchas particiones y muchas claves de cifrado de datos. Cifrar cada bloque de datos con una clave diferente dificulta los ataques de análisis criptográficos. Necesita acceso tooDEKs Hola proveedor o aplicación de instancia del recurso que está cifrado y descifrado de un bloque específico. Cuando se reemplaza una DEK con una nueva clave solo hello datos de su bloque asociado deben ser volverá a cifrar con una clave nueva Hola.
- **Clave de cifrado de claves (KEK)** : una clave de cifrado asimétrico utiliza tooencrypt hello las claves de cifrado de datos. Uso de una clave de cifrado de clave permite hello las claves de cifrado de datos propios toobe cifrados y controlado. entidad de Hola que tiene acceso toohello KEK puede ser diferente de la entidad de Hola que requiere Hola DEK. Esto permite que una entidad toobroker acceso toohello DEK a fin de hello consistente en garantizar un acceso limitado de cada partición de toospecific DEK. Puesto que hello KEK es necesario toodecrypt Hola DEK, Hola KEK eficazmente es un punto único por el que se puede eliminar eficazmente DEK por la eliminación de hello KEK.

Claves de cifrado de datos de Hello, cifradas con hello las claves de cifrado de clave se almacenan por separado y solo una entidad con toohello de acceso a que la clave de cifrado de clave puede obtener las claves de cifrado de datos cifrados con dicha clave. Se admiten diferentes modelos de almacenamiento de claves. Analizaremos cada modelo con más detalle más adelante en la sección siguiente Hola.

## <a name="data-encryption-models"></a>Modelos de cifrado de datos

Descripción Hola varios modelos de cifrado y sus ventajas y desventajas es fundamental para entender cómo Hola diversos proveedores de recursos de Azure implementan cifrado en reposo. Estas definiciones se comparten entre todos los proveedores de recursos en taxonomía y de Azure tooensure common language. 

Hay tres escenarios para el cifrado del lado servidor:

- Cifrado del lado servidor mediante claves administradas del servicio
    - Los proveedores de recursos Azure realizar operaciones de cifrado y descifrado de Hola
    - Microsoft administra las claves de Hola
    - Funcionalidad de nube completa

- Cifrado del lado servidor mediante claves administradas por el cliente en Azure Key Vault
    - Los proveedores de recursos Azure realizar operaciones de cifrado y descifrado de Hola
    - El cliente controla las claves mediante Azure Key Vault
    - Funcionalidad de nube completa

- El cifrado del lado servidor mediante claves administradas por el cliente en el hardware controlado por el cliente
    - Los proveedores de recursos Azure realizar operaciones de cifrado y descifrado de Hola
    - Claves de controles de cliente en el hardware controlado por el cliente
    - Funcionalidad de nube completa

Para el cifrado del lado cliente, tenga en cuenta Hola siguiente:

- Los servicios de Azure no pueden ver los datos descifrados
- Los clientes administran y almacenan las claves en ubicaciones locales (o en otras ubicaciones seguras). Las claves no son servicios tooAzure disponibles
- Funcionalidad de nube reducida

cifrado de Hello admitida los modelos de dividir en dos grupos principales de Azure: "Cliente cifrado" y "servidor" como se mencionó anteriormente. Tenga en cuenta que, independientemente del cifrado de hello en el modelo de rest usa unos servicios de Azure siempre se recomienda Hola uso de un transporte seguro como TLS o HTTPS. Por lo tanto, el cifrado de transporte debe tratarse con el protocolo de transporte de hello y no debe ser un factor importante para determinar qué cifrado en toouse de modelo de rest.

### <a name="client-encryption-model"></a>Modelo de cifrado del cliente

Modelo de cifrado de cliente refiere tooencryption que se realiza fuera de hello Azure o el proveedor de recursos de servicio de Hola o aplicación que realiza la llamada. cifrado de Hello puede realizarse mediante la aplicación de servicio de hello en Azure, o por una aplicación que se ejecuta en el centro de datos de cliente de Hola. En cualquier caso, cuando se aprovechan este modelo de cifrado, Hola proveedor de recursos de Azure recibe un blob cifrado de datos sin datos de saludo de hello capacidad toodecrypt de ninguna manera o tener acceso a claves de cifrado de toohello. En este modelo, administración de claves de Hola se realiza mediante Hola/aplicación de servicio de llamada y es completamente opaco toohello servicio de Azure.

![Cliente](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Modelo de cifrado del lado servidor

Modelos de cifrado del servidor, consulte tooencryption que llevan a cabo Hola servicio de Azure. En este modelo, Hola proveedor de recursos realiza Hola cifrar y descifrar las operaciones. Por ejemplo, el almacenamiento de Azure puede recibir datos en las operaciones de texto sin formato y llevará a cabo el descifrado y cifrado de hello internamente. Hola proveedor de recursos podría utilizar claves de cifrado que están administradas por Microsoft o por el cliente de hello según Hola proporcionada la configuración. 

![Server](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Modelos de administración de claves de cifrado del lado servidor

Cada uno de cifrado del lado servidor hello en modelos de rest implica características distintivas de administración de claves. Esta información incluye de dónde y cómo se crean y almacenan las claves de cifrado como así como modelos de acceso de Hola y Hola procedimientos de rotación de claves. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Cifrado del lado servidor mediante claves administradas del servicio

Para muchos clientes, requisito esencial hello es tooensure que Hola datos se cifra cuando encuentre en estado inactivo. Cifrado del lado servidor mediante las claves del servicio administrado permite este modelo permite a los clientes recursos específicos de toomark Hola (cuenta de almacenamiento, base de datos SQL, etc.) para el cifrado y salir de todos los aspectos de la administración de claves, como la emisión de claves, rotación y copia de seguridad tooMicrosoft. Mayoría de los servicios de Azure que admiten el cifrado en reposo normalmente admitiendo este modelo de delegación de la administración de Hola de tooAzure de claves de cifrado de Hola. proveedor de recursos de Azure de Hello crea claves hello, coloca en un almacenamiento seguro y recuperarlas cuando sea necesario. Esto significa que el servicio de hello tiene claves de acceso completa de toohello y servicio hello tiene control total sobre la administración de ciclo de vida de credenciales de Hola.

![administrado](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Cifrado del lado servidor mediante las claves del servicio administrado por lo tanto rápidamente direcciones Hola necesidad toohave el cifrado en reposo con el cliente de toohello sobrecarga baja. Cuando esté disponible un cliente normalmente abre Hola portal de Azure para la suscripción de destino de Hola y el proveedor de recursos y comprueba un cuadro que indica preferirían hello toobe de datos cifrado. El cifrado del lado servidor de algunos Resource Manager con las claves administradas del servicio se encuentra activado de forma predeterminada. 

Cifrado del lado servidor con las claves de Microsoft administrado implica servicio hello tiene acceso completo toostore y administra las claves de Hola. Mientras que algunos clientes pueden desear claves de hello toomanage porque creen que pueden garantizar una mayor seguridad, hello costo y los riesgos asociados con una solución de almacenamiento de claves personalizados se deben considerar al evaluar este modelo. En muchos casos, una organización puede determinar que las restricciones de recursos o los riesgos de una solución local pueden mayor riesgo de Hola de administración en la nube de cifrado de hello en claves de rest.  Sin embargo, este modelo podría no ser suficiente para las organizaciones que tienen la creación de requisitos toocontrol Hola o ciclo de vida de las claves de cifrado de Hola o personal diferentes toohave administrar claves de cifrado de un servicio que los que administrar el servicio de hello (es decir, segregación de administración de claves de hello modelo general de administración para el servicio de hello).

##### <a name="key-access"></a>Acceso a la clave

Cuando se usa el cifrado de servidor con los servicios de administrar claves, Hola creación de claves, acceso de almacenamiento y el servicio se administran por servicio Hola. Por lo general, los proveedores de recursos de Azure atractivos Hola almacenará Hola claves de cifrado de datos en un almacén de datos toohello de cierre y rápidamente disponible y es accesible al Hola claves de cifrado de clave se almacenan en un almacén interno seguro.

**Ventajas**

- Instalación simple
- Microsoft administra la redundancia, el backup y la rotación de claves
- Cliente no tiene Hola costo asociado con el riesgo de Hola o implementación de un esquema personalizado de administración de claves.

**Desventajas**

- Ningún control al cliente sobre las claves de cifrado de hello (especificación de clave del ciclo de vida, revocación, etcetera.)
- Ninguna administración de claves de toosegregate de capacidad del modelo de administración global para servicio de Hola

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Cifrado del lado servidor mediante claves administradas por el cliente en Azure Key Vault 

En escenarios donde el requisito de hello es tooencrypt datos de hello en reposo y los clientes las claves de cifrado de Hola de control pueden usar el cifrado de servidor mediante claves de cliente administrada en el almacén de claves. Algunos servicios pueden almacenar únicamente la clave de cifrado de clave de raíz de hello en el almacén de claves de Azure y Hola de almacén cifra la clave de cifrado de datos en un detalle de datos toohello ubicación interna. En que los clientes de escenario pueden poner sus propias tooKey (BYOK: aportar su propia clave), el almacén de claves o generar nuevos y usarlos tooencrypt recursos de hello deseado. Mientras Hola proveedor de recursos realiza operaciones de cifrado y descifrado de hello usa clave Hola configurado como clave de raíz de Hola para todas las operaciones de cifrado. 

##### <a name="key-access"></a>Acceso a la clave

Hello modelo de cifrado del lado servidor con claves administradas por el cliente en el almacén de claves de Azure implica Hola servicio acceso Hola claves tooencrypt y descifrar según sea necesario. Cifrado de claves de rest se realizan servicio tooa accesible a través de una directiva de control de acceso conceder ese clave Hola de tooreceive de acceso de la identidad de servicio. Un servicio de Azure que se ejecuta en nombre de una suscripción asociada puede configurarse con una identidad para ese servicio dentro de esa suscripción. servicio de Hello puede realizar la autenticación de Azure Active Directory y recibir un token de autenticación está identificando como ese servicio actúa en nombre de suscripción de Hola. Ese token puede ser presentado tooKey almacén tooobtain una clave se haya otorgado acceso a.

Para las operaciones con claves de cifrado, se puede conceder una identidad de servicio tooany de acceso del programa Hola a las siguientes operaciones: descifrar, cifrar, unwrapKey, wrapKey, compruebe, iniciar sesión, obtener, lista, actualizar, crear, importar, eliminar, una copia de seguridad y restauración.

tooobtain una clave para su uso en cifrar o descifrar datos en la identidad del servicio rest Hola ese Hola, Administrador de recursos que se ejecutará la instancia de servicio deben tener desencapsulado (clave de tooget hello para el descifrado) y WrapKey (tooinsert una clave en el almacén de claves al crear una nueva clave).


>[!NOTE] 
>Para obtener más detalles sobre el almacén de claves autorización vea Hola proteger su página de almacén de claves en hello [documentación del almacén de claves de Azure](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Ventajas**

- Control total sobre las claves de hello usados: cifrado de claves se administran en el almacén de claves del cliente de hello bajo el control del cliente de Hola.
- Capacidad tooencrypt maestro de varios servicios tooone
- Puede separar la administración de claves de modelo de administración global para servicio de Hola
- Puede definir el servicio y la ubicación de la clave en regiones

**Desventajas**

- El cliente tiene responsabilidad total para la administración de acceso a las claves
- El cliente tiene responsabilidad total para la administración del ciclo de vida de las claves
- Sobrecarga de configuración e instalación adicional

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>El cifrado del lado servidor mediante claves administradas del servicio en el hardware controlado por el cliente

En escenarios donde el requisito de hello tooencrypt Hola datos en reposo y administrar las claves de hello en un repositorio propietario fuera de control de Microsoft, algunos servicios de Azure habilitan el modelo de administración de claves de hello Host su propia clave (HYOK). En este modelo, servicio Hola debe recuperar la clave de Hola desde un sitio externo y, por tanto, se ven afectadas las garantías de rendimiento y la disponibilidad y configuración es más compleja. Además, dado que servicio Hola tienen acceso toohello DEK durante el cifrado de Hola y las operaciones de descifrado Hola garantías de seguridad general de este modelo son similares hello toowhen claves son administradas por el cliente en el almacén de claves de Azure.  Como resultado, este modelo no es adecuado para la mayoría de las organizaciones a menos que tengan requisitos específicos de administración de claves que se necesiten. Debido a limitaciones de toothese, la mayoría de los servicios de Azure no admiten el cifrado de servidor mediante claves de servidor administrado en el hardware del cliente controlado.

##### <a name="key-access"></a>Acceso a la clave

Cuando se usa el cifrado de servidor mediante las claves de servicio administrada en el hardware del cliente controlado las claves de Hola se mantienen en un sistema configurado por el cliente de Hola. Los servicios de Azure que admitan este modelo proporcionan un medio para establecer a un cliente de conexión segura tooa proporcionado almacén de claves.

**Ventajas**

- Control total sobre la clave raíz de hello usados: un almacén proporcionadas por el cliente administra las claves de cifrado
- Capacidad tooencrypt maestro de varios servicios tooone
- Puede separar la administración de claves de modelo de administración global para servicio de Hola
- Puede definir el servicio y la ubicación de la clave en regiones

**Desventajas**

- Responsabilidad total para la disponibilidad, rendimiento, seguridad y almacenamiento de claves
- Responsabilidad total para la administración de acceso a las claves
- Responsabilidad total para la administración del ciclo de vida de las claves
- Costos significativos de mantenimiento en curso, configuración y configuración
- Dependencia de aumento en la disponibilidad de red entre el centro de datos de cliente de Hola y centros de datos de Azure.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Cifrado en reposo en servicios en la nube de Microsoft

Los servicios en la nube de Microsoft se utilizan en los tres modelos de la nube: IaaS, PaaS, SaaS. A continuación encontrará ejemplos de cómo encajan en cada modelo:

- Servicios de software, que se hace referencia tooas Software como un servidor o SaaS, que tiene la aplicación proporcionada por la nube de hello, como Office 365.
- Servicios de la plataforma qué clientes aprovechan nube hello en sus aplicaciones mediante la nube de Hola para cosas como la funcionalidad de bus de almacenamiento, el análisis y el servicio.
- Servicios de infraestructura o de infraestructura como servicio (IaaS) en el cliente que implementar sistemas operativos y aplicaciones que se hospedan en hello en la nube y posiblemente aprovechando otros servicios en la nube.

### <a name="encryption-at-rest-for-saas-customers"></a>Cifrado en reposo para clientes de SaaS

Los clientes del software como servicio (SaaS) suelen tener el cifrado en reposo habilitado o disponible en cada servicio. Servicios de Office 365 tiene varias opciones para los clientes tooverify o habilitar un cifrado en reposo. Para obtener información acerca de los servicios de Office 365, vea las tecnologías de cifrado de datos para Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Cifrado en reposo para clientes PaaS

Plataforma como datos de un cliente de servicio (PaaS) normalmente reside en un entorno de ejecución de la aplicación y cualquier proveedor de recursos de Azure utiliza toostore los datos del cliente. cifrado de hello toosee rest opciones disponibles tooyou examinar la tabla de Hola a continuación para plataformas de almacenamiento y de aplicaciones de Hola que usar. Si se admite, se proporcionan vínculos tooinstructions acerca de cómo habilitar el cifrado en reposo para cada proveedor de recursos. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Cifrado en reposo para clientes de IaaS

Los clientes de la infraestructura como servicio (IaaS) pueden tener una variedad de servicios y aplicaciones en uso. Los servicios de IaaS pueden habilitar el cifrado en reposo en sus discos duros virtuales y máquinas virtuales que se hospedan en Azure mediante Azure Disk Encryption. 

#### <a name="encrypted-storage"></a>Almacenamiento cifrado

Al igual que PaaS, las soluciones IaaS pueden sacar provecho de otros servicios de Azure que almacenan los datos que se cifran en reposo. En estos casos, puede habilitar Hola cifrado en el soporte técnico de Rest proporcionada por cada servicio de Azure consumido. Hola tabla siguiente enumera almacenamiento principal de hello, servicios y plataformas de aplicación y modelo Hola de cifrado en reposo admitida. Si se admite, se proporcionan vínculos tooinstructions acerca de cómo habilitar el cifrado en reposo. 

#### <a name="encrypted-compute"></a>Compute de cifrado

Un cifrado completo en la solución de Rest requiere ese Hola datos nunca se guardan en formato descifrado. Mientras está en uso, en un saludos de carga del servidor pueden se almacenen los datos en la memoria, los datos localmente de varias maneras, incluido el archivo de paginación de Windows hello, un volcado de memoria, cualquier registro hello y aplicación puede realizar. tooensure estos datos se cifran en reposo las aplicaciones IaaS pueden usar el cifrado de disco de Azure en una máquina virtual de IaaS de Azure (Windows o Linux) y un disco virtual. 

#### <a name="custom-encryption-at-rest"></a>Cifrado de datos en reposo personalizado

Se recomienda que siempre que sea posible, las aplicaciones IaaS saquen provecho de las opciones de cifrado en reposo y Azure Disk Encryption proporcionadas por los servicios de Azure consumidos. En algunos casos, como requisitos de cifrado irregulares o almacenamiento basado en distintas de Azure, un desarrollador de una aplicación de IaaS que necesite tooimplement cifrado coloque por sí mismos. Las soluciones de los desarrolladores de IaaS podrían integrarse mejor con las expectativas de administración y del cliente de Azure mediante el aprovechamiento de ciertos componentes de Azure. En concreto, los desarrolladores deben extremar hello Azure Key Vault tooprovide servicio almacenamiento seguro de claves, así como proporcionar a sus clientes con opciones de clave de administración coherente con el de Azure más servicios de la plataforma. Además, las soluciones personalizadas deben usar claves de cifrado de tooaccess cuentas de servicio de Azure administra las identidades de servicio tooenable. Para encontrar información para desarrolladores sobre Azure Key Vault y las identidades de servicio administradas, consulte sus respectivos SDK.

## <a name="azure-resource-providers-encryption-model-support"></a>Compatibilidad con modelo de cifrado de proveedores de recursos de Azure

Servicios de Microsoft Azure cada admitir uno o más de cifrado de hello en modelos de rest. Para algunos servicios, sin embargo, uno o varios de los modelos de cifrado de hello pueden no ser aplicable. Además, los servicios pueden liberar compatibilidad para estos escenarios en distintas programaciones. Esta sección describe el cifrado de hello en el soporte técnico de rest en tiempo de Hola de redactar este artículo para cada uno de los servicios de almacenamiento de datos de Azure principales Hola.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Cualquier cliente mediante las características de la infraestructura de Azure como servicio (IaaS) puede lograr el cifrado en reposo para sus discos y máquinas virtuales de IaaS y discos mediante Azure Disk Encryption. Para obtener más información en el disco de Azure cifrado vea hello [documentación de cifrado del disco de Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Almacenamiento de Azure

Azure Blob y Archivo admiten el cifrado en reposo para escenarios cifrados del lado servidor, así como datos cifrados del cliente (cifrado del lado cliente).

- Lado servidor: Los clientes que usan Azure Blob Storage pueden habilitar el cifrado en reposo en cada cuenta de recursos de Azure Storage. Una vez habilitado el cifrado del servidor se realiza de manera transparente toohello aplicación. Para más información, consulte [Cifrado del servicio Azure Storage para datos en reposo](https://docs.microsoft.com/azure/storage/storage-service-encryption).
- Lado cliente: Se admite el cifrado del lado cliente de Azure Blobs. Cuando se usa el cifrado en el cliente los clientes cifrar Hola datos y cargar datos de Hola como un blob cifrado. Administración de claves se realiza por el cliente de Hola. Consulte [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) (Cifrado del lado cliente y Azure Key Vault para Microsoft Azure Storage) para más información.


#### <a name="sql-azure"></a>SQL Azure

SQL Azure admite actualmente el cifrado en reposo para escenarios de cifrado en el lado cliente y en el lado servicio administrados por Microsoft.

Compatibilidad con servidor actualmente proporciona el cifrado a través de la característica SQL Hola denominado cifrado de datos transparente. Una vez que un cliente de SQL Azure habilita la clave TDE se crea y administra automáticamente para él. Cifrado en reposo puede habilitarse en los niveles de base de datos y el servidor de Hola. A partir de junio de 2017, el [cifrado de datos transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) se habilitará de forma predeterminada en las bases de datos recién creadas.

Cliente de cifrado de datos de SQL Azure se admite a través de hello [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) característica. Always Encrypted utiliza una clave que se crea y se almacena por cliente Hola. Los clientes pueden almacenar la clave maestra de hello en un almacén de certificados de Windows, el almacén de claves de Azure o un módulo de seguridad de Hardware local. Usar SQL Server Management Studio, los usuarios SQL elegir qué clave les gustaría usar toouse tooencrypt qué columna.

|                                  |                |                     | **Modelo de cifrado**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Cliente** |
|                                  | **Administración de claves** | **Clave administrada del servicio** | **Cliente administrado en Key Vault** | **Cliente administrado en local** |        |
| **Almacenamiento y bases de datos**            |                |                     |                              |                              |        |
| Disco (IaaS)                      |                | -                   | Sí                          | Sí*                         | -      |
| SQL Server (IaaS)                |                | Sí                 | Sí                          | Sí                          | Sí    |
| SQL Azure (PaaS)                 |                | Sí                 | Vista previa                      | -                            | Sí    |
| Azure Storage (blobs en bloques o en páginas) |                | Sí                 | Vista previa                      | -                            | Sí    |
| Azure Storage (archivos)            |                | Sí                 | -                            | -                            | -      |
| Azure Storage (tablas, colas)   |                | -                   | -                            | -                            | Sí    |
| Cosmos DB (documento DB)          |                | Sí                 | -                            | -                            | -      |
| StorSimple                       |                | Sí                 | -                            | -                            | Sí    |
| Backup                           |                | -                   | -                            | -                            | Sí    |
| **Inteligencia y análisis**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | Sí                 | -                            | -                            | -      |
| Aprendizaje automático de Azure           |                | -                   | Vista previa                      | -                            | -      |
| Análisis de transmisiones de Azure           |                | Sí                 | -                            | -                            | -      |
| HDInsights (Azure Blob Storage)  |                | Sí                 | -                            | -                            | -      |
| HDInsights (Data Lake Storage)   |                | Sí                 | -                            | -                            | -      |
| Almacén de Azure Data Lake            |                | Sí                 | Sí                          | -                            | -      |
| Azure Data Catalog               |                | Sí                 | -                            | -                            | -      |
| Power BI                         |                | Sí                 | -                            | -                            | -      |
| **Servicios IoT**                     |                |                     |                              |                              |        |
| IoT Hub                          |                | -                   | -                            | -                            | Sí    |
| Bus de servicio                      |                | -              | -                            | -                            | Sí    |
| Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Conclusión

Protección de datos del cliente almacenados dentro de los servicios de Azure es de gran importancia tooMicrosoft. Hospedado de Azure todos los servicios están confirmado tooproviding cifrado en Opciones de Rest. Los servicios fundamentales como el almacenamiento Azure Storage, SQL Azure y análisis e inteligencia de las claves proporcionan ya opciones de cifrado en reposo. Algunos de estos servicios admiten claves de cliente controlada y cifrado en el cliente, así como cifrado y claves administradas del servicio. Servicios de Microsoft Azure están mejorando ampliamente cifrado con una disponibilidad de Rest y nuevas opciones están planificadas para vista previa y la disponibilidad general en los próximos meses de Hola.

