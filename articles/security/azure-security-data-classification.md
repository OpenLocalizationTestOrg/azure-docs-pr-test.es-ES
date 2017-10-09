---
title: "aaaData clasificación de Azure | Documentos de Microsoft"
description: "Este artículo proporciona una introducción toohello conceptos básicos de la clasificación de datos y resalta su valor, en concreto en el contexto de Hola de cloud computing y con Microsoft Azure"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Clasificación de datos para Azure
Este artículo proporciona una introducción toohello conceptos básicos de la clasificación de datos y su valor, en concreto en el contexto de Hola de cloud computing y con Microsoft Azure resalta. 

## <a name="data-classification-fundamentals"></a>Fundamentos de la clasificación de datos
Para clasificar correctamente los datos de una organización, es necesario comprender el amplio abanico de necesidades de la organización y conocer de forma exhaustiva dónde residen sus recursos de datos.  

Los datos existen en uno de estos tres estados básicos: 

* En reposo 
* En curso 
* En tránsito 

Los tres estados requieren soluciones técnicas únicas para la clasificación de datos, pero hello aplicados principios de clasificación de datos debe ser Hola igual para cada uno. Los datos que esté clasificados como confidencial tienen toostay confidencial si está en reposo, en proceso y en tránsito. 

Además, los datos pueden ser estructurados o no estructurados. Procesos de clasificación típico para hello estructura de datos que se encuentran en las bases de datos y hojas de cálculo son menos complejo y lento toomanage que los de los datos no estructurados, como documentos, código fuente y correo electrónico. 

> [!TIP]
> Para más información acerca de las funcionalidades de Azure y los procedimientos recomendados para el cifrado de datos, lea [Azure Data Security and Encryption Best Practices](azure-security-data-encryption-best-practices.md) (Procedimientos recomendados de cifrado y seguridad de datos en Azure)
> 
> 

Por lo general, las organizaciones tendrán más datos no estructurados que estructurados. Independientemente de si los datos son estructurados o no estructurados, es importante sensibilidad datos toomanage. Cuando se implementa correctamente, la clasificación de datos le ayuda a garantizar que los datos confidenciales o activos se administran con mayor supervisión de recursos de datos que se consideran toodistribute público o libre. 

### <a name="controlling-access-toodata"></a>Control de acceso toodata
Con frecuencia la autenticación y la autorización se confunden y no se comprende bien su función. En realidad son muy diferentes, como se muestra en la figura siguiente de Hola.  

![Control y acceso a datos](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Autenticación
Autenticación normalmente consta de al menos dos partes: un tooidentify de Id. de usuario o nombre de usuario un usuario y un símbolo (token), como una contraseña, tooconfirm que Hola credencial de nombre de usuario es válido. proceso de Hello no proporciona Hola usuario autenticado con acceso a los elementos de tooany o servicios; comprueba que ese usuario hello es quien dice ser.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) proporciona servicios de identidad basado en la nube que le permiten tooauthenticate y autorizan a los usuarios. 
> 
> 

### <a name="authorization"></a>Autorización
La autorización es el proceso de hello consistente en proporcionar un tooaccess de capacidad de Hola de usuario autenticado de una aplicación, conjunto de datos, archivo de datos o algún otro objeto. Asignar los usuarios autenticados Hola derechos toouse, modificar o eliminar elementos que pueden tener acceso requiere clasificación toodata de atención. 

La autorización correctamente requiere la implementación de un mecanismo toovalidate los usuarios individuales necesita archivos de tooaccess y la información en función de una combinación de rol, la directiva de seguridad y consideraciones de la directiva de riesgo. Por ejemplo, datos de aplicaciones específicas line-of-business (LOB) que no precise toobe tiene acceso a todos los empleados, y solo un pequeño subconjunto de los empleados probablemente necesitará tener acceso toohuman archivos de recursos (RR). Pero para las organizaciones toocontrol quién puede acceder a datos, como así como cuándo y cómo, debe ser un sistema eficaz para autenticar a los usuarios en su lugar. 

> [!TIP]
> en Microsoft Azure, asegúrese de que tooleverage Azure Role-Based Access Control (RBAC) toogrant únicamente Hola una cantidad de acceso que los usuarios necesitan tooperform sus trabajos. Lectura [usar recursos de Active Directory de rol asignaciones toomanage acceso tooyour](../active-directory/role-based-access-control-configure.md) para obtener más información. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Roles y responsabilidades en la informática en la nube
Aunque los proveedores de nube pueden ayudar a administrar los riesgos, los clientes necesitan tooensure que administración de clasificación de datos y se implementa correctamente el cumplimiento tooprovide Hola nivel adecuado de servicios de administración de datos.  

Clasificación de datos varían las responsabilidades se basa en qué modelo de servicio de nube está en su lugar, como se muestra en la figura siguiente de Hola. tres modelos de servicio de nube principal Hola son infraestructura como servicio (IaaS), plataforma como servicio (PaaS) y el software como servicio (SaaS). Implementación de mecanismos de clasificación de datos también varían según dependencia hello y expectativas Hola del proveedor de nube. 

![Roles](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Aunque tú eres responsable de clasificar los datos, los proveedores de nube deben hacer compromisos escritos acerca de cómo se van a proteger y mantener la privacidad de Hola Hola de datos de clientes almacenados dentro de la nube.  

* **Proveedores de IaaS** requisitos se limitan tooensuring que Hola entorno virtual puede dar cabida a las capacidades de clasificación de datos y los requisitos de cumplimiento del cliente. Proveedores de IaaS tienen un rol más pequeño en la clasificación de datos porque sólo necesitarán tooensure que los datos del cliente aborda los requisitos de cumplimiento. Sin embargo, los proveedores aún deben asegurarse que sus entornos virtuales de abordar los requisitos de clasificación de datos de adición toosecuring sus centros de datos.
* **Proveedores de PaaS** responsabilidades se pueden combinar, porque plataforma Hola podría ser usada en seguridad tooprovide enfoque por capas para una herramienta de clasificación. Proveedores de PaaS pueden ser responsables de la autenticación y posiblemente algunas reglas de autorización y deben proporcionar seguridad y el nivel de aplicación de tootheir de capacidades de clasificación de datos. Mucho como proveedores de IaaS, PaaS proveedores necesitan tooensure que su plataforma cumple con los requisitos de clasificación de datos relevantes.
* **Proveedores de SaaS** con frecuencia se considerará como parte de una cadena de autorización, y se necesita tooensure que Hola datos almacenados en la aplicación de SaaS hello puede controlarse mediante tipo de clasificación. Aplicaciones de SaaS se pueden utilizar para las aplicaciones LOB, y por su propia naturaleza necesita tooprovide Hola significa tooauthenticate y autorizar a los datos que se usa y se almacena. 

## <a name="classification-process"></a>Proceso de clasificación
¿Muchas organizaciones que entender Hola necesario para la clasificación de datos y desea tooimplement enfrentan a un desafío básico: donde toobegin?

Una manera sencilla y eficaz de clasificación de datos de tooimplement es toouse hello PLAN, lo hace, modelo de comprobación, ACT de [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). Hola siguiente ilustración, los gráficos de las tareas hello toosuccessfully necesario implementar la clasificación de datos en este modelo.  

1. **PLANEAR**. Identificar los activos de datos, un programa de clasificación de datos custodia toodeploy hello y desarrollar perfiles de protección. 
2. **HACER**. Una vez acordadas directivas de clasificación de datos, implementar programa hello y tecnologías de cumplimiento según sea necesario para datos confidenciales.  
3. **COMPROBAR**. Comprobar y validar informes tooensure que herramientas de Hola y los métodos que se va a utilizar eficazmente se dirección Hola directivas de clasificación. 
4. **ACTUAR**. Revisar el estado de Hola de acceso a datos y revisar los archivos y datos que requieren revisión utilizando una reclasificación y cambios de revisión metodología tooadopt y tooaddress nuevos riesgos.  

![Planear, hacer, comprobar, actuar](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Selección de un modelo terminológico apto para sus necesidades
Existen varios tipos de procesos para la clasificación de datos, incluidos los procesos manuales, de procesos basada en la ubicación que clasificación los datos según la ubicación de un usuario o del sistema, según las aplicaciones de procesos como la clasificación de la base de datos específica y automatizada procesos usados por varias tecnologías, algunos de los cuales se describen en la sección de "Protección de datos confidenciales" hello más adelante en este artículo.  

En este artículo se presentan dos modelos terminológicos generalizados que se basan en los extendidos y respetados en el sector. Estos modelos de terminología, que ofrecen tres niveles de sensibilidad de clasificación, se muestran en hello en la tabla siguiente.  

> [!NOTE]
> al clasificar un archivo o recurso que combina datos que normalmente se clasificaría en distintos niveles de nivel más alto de Hola de clasificación presente deben establecer Hola clasificación general. Por ejemplo, un archivo que contenga datos sensibles y restringidos se debe clasificar como restringido.  
> 
> 

| **Confidencialidad** | **Modelo terminológico 1** | **Modelo terminológico 2** |
| --- | --- | --- |
| Alto |Confidencial |Restringido |
| Mediano |Solo para uso interno |Sensible |
| Bajo |Público |Sin restricciones |

#### <a name="confidential-restricted"></a>Confidencial (restringida)
La información que esté clasificada como confidencial o restringido incluye datos que pueden ser tooone grave o más usuarios o las organizaciones si comprometidas o perdidas. Esta información se proporciona con frecuencia en forma de "necesidad tooknow" y puede incluir: 

* Datos personales, entre ellos información de identificación personal, como los números de documento nacional de identidad o del seguro social, números de pasaporte, números de tarjeta de crédito, números del permiso de conducción, historias clínicas y números identificativos de pólizas de seguro de salud.  
* Registros financieros, incluidos los números de cuentas financieras, como números de cuentas corrientes o de inversión. 
* Material de negocios, como documentos o datos exclusivos o propiedad intelectual específica.  
* Datos jurídicos, incluido el material que podría considerarse cubierto por el secreto profesional entre abogado y cliente. 
* Datos de autenticación, incluidas claves criptográficas privadas, pares de nombre de usuario y contraseña u otras secuencias de identificación, como archivos de claves biométricas privadas. 

Los datos que se clasifican como confidenciales poseen con frecuencia requisitos reglamentarios y de cumplimiento para el tratamiento de los datos. 

#### <a name="for-internal-use-only-sensitive"></a>Solo para uso interno (sensible)
La información que se clasifica como de confidencialidad media incluye archivos y datos que no acarrearían repercusiones graves para un individuo o una organización si se pierden o destruyen. Tal información podría incluir: 

* Correo electrónico, la mayoría de los cuales se puedan eliminar o distribuida sin causar una crisis (excepto los buzones de correo o correo electrónico de personas que se identifican en la clasificación de hello confidencial).  
* Documentos y archivos que no contienen datos confidenciales.

Por lo general, esta clasificación engloba todo lo que no es confidencial. Esta clasificación puede abarcar la mayor parte de los datos empresariales, ya que la mayoría de los archivos que se administran o utilizan a diario pueden clasificarse como sensibles. Con excepción de Hola de datos que se hace público o son confidencial, todos los datos dentro de una organización de negocios pueden estar clasificados como confidenciales de forma predeterminada. 

#### <a name="public-unrestricted"></a>Pública (sin restricciones)
La información que se clasifica como público incluye datos y los archivos que no son críticos toobusiness necesidades u operaciones. Esta clasificación también puede incluir datos que se ha deliberadamente publicada toohello pública para su uso, como anuncios de materiales o presione de marketing. Además, esta clasificación puede incluir datos como mensajes de correo electrónico no deseado almacenados por un servicio de correo electrónico. 

### <a name="define-data-ownership"></a>Definición de la propiedad de los datos
Es importante tooestablish una cadena de custodia claro de propiedad para todos los activos de datos. Hello tabla siguiente identifican las funciones de propiedad de datos diferentes en los esfuerzos de clasificación de datos y sus derechos respectivos.  

| **Rol** | **Creación** | **Modificar o eliminar** | **Delegar** | **Lectura** | **Archivar o restaurar** |
| --- | --- | --- | --- | --- | --- |
| Propietario |X |X |X |X |X |
| Administrador de recursos de datos | | |X | | |
| Administrador | | | | |X |
| Usuario\* | |X | |X | |

**Un administrador puede otorgar derechos adicionales a los usuarios, por ejemplo, para editar y eliminar* 

> [!NOTE]
> En esta tabla no se proporciona una lista exhaustiva de roles y derechos, sino solo una muestra representativa. 
> 
> 

Hola **propietario del recurso de datos** es Hola creador original de los datos de hello, que pueden delegar la propiedad y asignar custodia. Cuando se crea un archivo, el propietario de hello debe ser capaz de tooassign una clasificación, lo que significa que tienen un toounderstand responsabilidad lo que debe toobe clasificado como confidenciales se basa en las directivas de su organización. Todos los datos del propietario de recursos de datos se pueden clasificar de forma automática como Solo para uso interno (sensible) a menos que sea responsable de tener en propiedad o crear tipos de datos confidenciales (restringidos). Con frecuencia, Hola su rol cambiará después de que se clasifican los datos de Hola. Por ejemplo, propietario de hello puede crear una base de datos de información confidencial y ceder a su custodia de datos de toohello de derechos.  

> [!NOTE]
> los propietarios de activos de datos suelen utilizar una combinación de servicios, dispositivos y medios, algunos de los cuales son personales y algunos de los cuales pertenecen toohello organización. Una directiva clara de la organización puede ayudar a asegurarse de que el uso de dispositivos como equipos portátiles y dispositivos inteligentes cumpla las instrucciones de clasificación de datos.  
> 
> 

Hola **custodia de activos de datos** está asignado por el propietario del recurso de hello (o su delegado) toomanage Hola asset correspondiente tooagreements con el propietario del recurso de Hola o según los requisitos de la directiva es aplicable. Idealmente, rol de custodia de hello puede implementarse en un sistema automatizado. Custodia de activos corresponda garantiza que los controles de acceso necesarios se proporcionan y es responsables de administrar y proteger los activos delega tootheir atención. responsabilidades de Hola de custodia de activos de Hola se incluyen:  

* Proteger los activos de hello con arreglo a la dirección del propietario del recurso de Hola o de acuerdo con el propietario del recurso de Hola 
* Garantizar que se cumplan de directivas de clasificación 
* Informar a los propietarios de los activos de los cambios tooagreed-en controles o de protección procedimientos anteriores toothose los cambios surten efecto 
* Propietario del recurso toohello informes acerca de la eliminación de tooor de cambios de las responsabilidades de custodia de hello activo 
* Un **administrador** representa a un usuario que es responsable de garantizar que se mantenga la integridad, pero no es propietario, administrador ni usuario del recurso de datos. De hecho, muchos de los roles de administrador proporcionan servicios de administración del contenedor de datos sin necesidad de acceder a los datos toohello. rol de administrador de Hello incluye copias de seguridad y restauración de los datos de hello, mantenimiento de registros de activos de hello, y elegir, adquirir y usar Hola dispositivos y almacenamiento que activos de Hola de casa. 
* usuario de activos de Hello incluye cualquier usuario que se le concede acceso toodata o un archivo. Asignación de acceso se delega a menudo por custodia de hello propietario toohello activo.  

### <a name="implementation"></a>Implementación
Consideraciones sobre la administración aplican las metodologías de clasificación de tooall. Estas consideraciones necesitan tooinclude saber quién, qué, dónde, cuándo y por qué un recurso de datos podría ser utilizado, tiene acceso a, cambiado o eliminado. Toda la administración de activos debe realizarse una vez que entienda cómo una organización ve sus riesgos, pero se puede aplicar una metodología simple tal como se define en el proceso de clasificación de datos de Hola. Las consideraciones adicionales para la clasificación de datos incluyen hello introducción de nuevas aplicaciones y herramientas y administración de cambios después de que se implementa un método de clasificación.  

### <a name="reclassification"></a>Reclasificación
Reclasificar o cambiar el estado de clasificación de Hola de un recurso de datos necesita toobe realiza cuando un usuario o el sistema determina la importancia de dicho activo datos de Hola o se ha cambiado el perfil de riesgo. Este trabajo es importante para garantizar que el estado de clasificación de hello sigue toobe actual y válido. Gran parte del contenido que no se clasifica manualmente se puede clasificar de forma automática o el propietario o el administrador de recursos de datos puede hacerlo en función del uso. 

### <a name="manual-data-reclassification"></a>Reclasificación manual de datos
Idealmente, este esfuerzo garantiza que los detalles de Hola de un cambio de captura y se audita. motivo más probable de Hello modificar la clasificación manual sería por motivos de confidencialidad, o para los registros que se mantiene en formato de papel o un tooreview de datos de requisito que originalmente se clasifican incorrectamente. Dado que este documento considera que la clasificación de datos y mover datos toohello en la nube, los esfuerzos de reclasificación manual requiere atención en caso por caso y una revisión de administración de riesgos sería ideal tooaddress requisitos de clasificación. Por lo general, un intento de este tipo se considere la posibilidad de directiva de la organización de hello sobre lo que debe toobe clasificado, Hola estado de clasificación predeterminado (todos los datos y archivos confidenciales pero no confidencial) y aceptar excepciones para los datos de alto riesgo. 

### <a name="automatic-data-reclassification"></a>Reclasificación automática de datos
Reclasificación automática de los datos usa Hola mismo general de reglas como la clasificación manual. excepción de Hello es que pueden garantizar soluciones automatizadas que las reglas se seguido y aplican según sea necesario. La clasificación de datos puede realizarse como parte de una directiva de cumplimiento de clasificación de datos, que se puede aplicar cuando los datos estén almacenados, en uso y en tránsito mediante tecnología de autorización.

* Basada en la aplicación. El uso de determinadas aplicaciones establece de forma predeterminada un nivel de clasificación. Por ejemplo, los datos procedentes de software de administración de las relaciones con el cliente (CRM), de Recursos Humanos o de herramientas de administración de historias clínicas son confidenciales de forma predeterminada. 
* Basada en la ubicación. La ubicación de los datos puede ayudar a identificar su nivel de confidencialidad. Por ejemplo, los datos que se almacenan por un recursos humanos o el departamento financiero están más probable que toobe confidencial por naturaleza.  

### <a name="data-retention-recovery-and-disposal"></a>Retención, recuperación y eliminación de datos
La recuperación y la eliminación de datos, al igual que su reclasificación, es un aspecto esencial de la administración de los recursos de datos. Hello principios para la recuperación de datos y eliminación se definiría una directiva de retención de datos y la aplica de hello igual manera que reclasificación de datos; roles de administrador y custodia de hello como una tarea de colaboración que realiza un intento de este tipo.  

Error toohave una directiva de retención de datos puede significar toocomply pérdidas o errores de datos con los requisitos legales y normativos la detección. La mayoría de las organizaciones que no tienen una directiva de retención de datos definida claramente suelen toouse una directiva de retención predeterminado "tenerlo todo". Sin embargo, este tipo de directiva de retención conlleva riesgos adicionales en los escenarios de servicios en la nube. 

Por ejemplo, una directiva de retención de datos para proveedores de servicios de nube puede considerarse como "duración de saludo de la suscripción de hello" (siempre que servicio Hola se paga por, se retienen los datos de hello). Es posible que un acuerdo de pago por retención de este tipo no tenga en cuenta las directivas de retención corporativas o reglamentarias. La definición de una directiva para datos confidenciales puede garantizar que los datos se almacenen y eliminen de acuerdo con los procedimientos recomendados. Además, puede crearse una directiva de archivado tooformalize una descripción acerca de qué datos se debe desechar de y cuándo. 

Directiva de retención de datos debería solucionar Hola necesario normas y los requisitos de cumplimiento, así como los requisitos corporativos retención legal. Los datos clasificados podrían suscitar preguntas sobre la duración de la retención y las excepciones para los datos que se hayan almacenado con un proveedor. Estas preguntas son más probables para aquellos datos que no se hayan clasificado correctamente. 

> [!TIP]
> obtener más información sobre las directivas de retención de datos de Azure y mucho más leyendo hello [contrato Microsoft Online Subscription](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Protección de datos confidenciales
Después de que se clasifican los datos, buscar e implementar maneras tooprotect que los datos confidenciales se convierte en una parte integral de cualquier estrategia de implementación de protección de datos. Protección de datos confidenciales requiere datos de toohow de atención adicional se almacenan y se transmiten en arquitecturas convencionales, así como en la nube de Hola. 

Esta sección proporciona información básica acerca de algunas tecnologías que puede automatizar los esfuerzos de cumplimiento toohelp proteger los datos que se ha clasificado como confidencial. 

Como la siguiente figura muestra de Hola, estas tecnologías se pueden implementar como local o soluciones basadas en la nube, o en un modo híbrido, con algunas de ellos implementado de forma local y otras en la nube de Hola. (Algunas tecnologías, como el cifrado y la administración de derechos, amplían dispositivos toouser.)  

![Tecnologías](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Software de administración de derechos
Una solución para evitar la pérdida de datos es un software de administración de derechos. A diferencia de los métodos que traten toointerrupt Hola flujo de la información en los puntos de salida en una organización, software de administración de derechos funciona en niveles profundos de tecnologías de almacenamiento de datos. Los documentos se cifran y, para controlar quién puede descifrarlos, se usan controles de acceso que se definen en una solución de control de autenticación, como por ejemplo un servicio de directorio.  

> [!TIP]
> Puede usar Azure Rights Management (Azure RMS) como datos tooprotect soluciones de protección de información de hello en escenarios diferentes. Lea [¿Qué es Azure Rights Management?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) para más información sobre esta solución de Azure.
> 
> 

Algunas de las ventajas de Hola de software de administración de derechos incluyen: 

* Información sensible protegida. Los usuarios pueden proteger sus datos directamente mediante aplicaciones habilitadas para la administración de derechos. No se requiere ningún paso adicional: la experiencia de protección de datos es uniforme cuando se crean documentos, se envían correos electrónicos o se publican datos. 
* Protección viaja con datos de Hola. Los clientes permanecen en el control de quién tiene acceso a datos de tootheir, ya sea en nube de hello, infraestructura de TI existente, o en el escritorio del usuario de Hola. Las organizaciones pueden elegir tooencrypt sus datos y restringir el acceso según tootheir requisitos empresariales. 
* Directivas de protección de información predeterminadas. Los administradores y los usuarios pueden utilizar directivas estándar para muchos escenarios empresariales habituales, como "Información confidencial de la compañía: solo lectura" y "No reenviar". Un amplio conjunto de derechos de uso se admiten como lectura, copiar, imprimir, guardar, editar y reenviar tooallow flexibilidad en la definición de derechos de uso personalizados. 

> [!TIP]
> Los datos de Azure Storage se pueden proteger mediante el [Cifrado del servicio Almacenamiento de Azure](../storage/storage-service-encryption.md) para datos en reposo (versión preliminar). También puede usar [cifrado del disco de Azure](azure-security-disk-encryption.md) toohelp proteger los datos contenidos en los discos virtuales que usa máquinas virtuales de Azure.
> 
> 

### <a name="encryption-gateways"></a>Puertas de enlace de cifrado
Las puertas de enlace de cifrado funcionan en sus propios servicios de cifrado de capas tooprovide reenrutamiento en todos los datos de acceso basado en toocloud. Este enfoque no debe confundirse con el de una red privada virtual (VPN). Las puertas de enlace de cifrado son tooprovide diseñado un transparente soluciones basadas en toocloud de las capas.   

Las puertas de enlace de cifrado pueden proporcionar un medio toomanage y proteger los datos que se ha clasificado como confidencial mediante el cifrado de datos de hello en tránsito, así como datos en reposo.  

Las puertas de enlace de cifrado se colocan en Hola de flujo de datos entre los dispositivos de usuario y los servicios de cifrado y descifrado de tooprovide de centros de datos de aplicación. Estas soluciones, al igual que las VPN, son en su mayor parte soluciones locales. Únicamente son tooprovide diseñado un tercero con control sobre las claves de cifrado, lo que ayuda a reduce el riesgo de Hola de colocar datos de Hola y administración de claves con un proveedor. Estas soluciones están diseñadas, igual que el cifrado, toowork sencilla y transparente entre los usuarios y el servicio de Hola. 

> [!TIP]
> Puede usar Azure ExpressRoute tooextend sus redes locales en la nube de Microsoft de Hola a través de una conexión privada dedicada. Para más información sobre esta funcionalidad, consulte [Información técnica de ExpressRoute](../expressroute/expressroute-introduction.md). Otra opción para la conectividad entre locales, entre su red local y [Azure es una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Prevención de la pérdida de datos
Pérdida de datos (en ocasiones denominado tooas pérdida de datos) es una consideración importante y prevención de Hola de pérdida de datos externos a través de Insider malintencionada como accidental es fundamental para muchas organizaciones.  

Las tecnologías de prevención de pérdida de datos (DLP) pueden ayudar a garantizar que soluciones tales como los servicios de correo electrónico no transmitan datos que se hayan clasificado como confidenciales. Las organizaciones pueden sacar partido de las características DLP en los productos existentes toohelp evitar la pérdida de datos. Dichas características utilizan directivas que pueden crearse fácilmente desde el principio o mediante una plantilla suministrada por el proveedor de software de Hola.  

Tecnologías DLP pueden realizar un análisis profundo del contenido a través de coincidencias de palabras clave, coincidencias de diccionario, evaluaciones de expresiones regulares y otro contenido de toodetect de exámenes de contenido que infringe las directivas DLP organizativas. Por ejemplo, DLP puede ayudar a evitar la pérdida de Hola de hello siguientes tipos de datos: 

* Números de documento nacional de identidad o del seguro social 
* Información bancaria 
* Números de tarjeta de crédito  
* Direcciones IP 

Algunas tecnologías DLP también proporcionan la configuración de DLP de hello capacidad toooverride Hola (por ejemplo, si una organización necesita procesador de tootransmit número del seguro Social information tooa nómina). Además, es posible tooconfigure DLP para que los usuarios reciben notificaciones antes de que intente incluso toosend información confidencial que no se debe transmitir. 

> [!TIP]
> Puede usar Office 365 DLP capacidades tooprotect sus documentos. Para más información, lea [Office 365 compliance controls: Data Loss Prevention](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) (Controles de cumplimiento de Office 365: prevención de pérdida de datos).
> 
> 

## <a name="see-also"></a>Consulte también
* [Procedimientos recomendados de cifrado y seguridad de datos en Azure](azure-security-data-encryption-best-practices.md)
* [Procedimientos recomendados para la administración de identidades y la seguridad del control de acceso en Azure](azure-security-identity-management-best-practices.md)
* [Blog del equipo de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/)
* [Centro de respuesta de seguridad de Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

