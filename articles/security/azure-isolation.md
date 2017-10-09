---
title: "aaaIsolation Hola nube pública de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los servicios informáticos en la nube que incluyen una amplia selección de instancias de proceso y servicios que se pueden escalar arriba y abajo automáticamente toomeet hello las necesidades de su aplicación o enterprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Aislamiento de hello nube pública de Azure
##  <a name="introduction"></a>Introducción
### <a name="overview"></a>Información general
tooassist actuales y potenciales clientes Azure comprender y utilizar Hola varias funciones relacionadas con la seguridad está disponibles en y que lo rodea Hola plataforma Windows Azure, Microsoft ha desarrollado una serie de notas del producto, información general de seguridad, los procedimientos recomendados, y Listas de comprobación.
temas de Hello en cuanto a la amplitud y la profundidad de intervalo y se actualizan periódicamente. Este documento es parte de esa serie como se resume en la sección abstracta Hola que sigue.

### <a name="azure-platform"></a>Plataforma Azure
Azure es una plataforma de servicio de nube abierta y flexible que admite Hola selección más amplia de sistemas operativos, lenguajes de programación, marcos, herramientas, las bases de datos y dispositivos. Por ejemplo, puede:
- Ejecutar contenedores de Linux con integración con Docker.
- Compilar aplicaciones con JavaScript, Python, .NET, PHP, Java y Node.js.
- Crear back-ends para dispositivos iOS, Android y Windows.

Microsoft Azure es compatible con hello mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza.

Al compilar en, o migrar los activos de TI a un proveedor de servicios de nube pública, está confiando en tooprotect de capacidades de la organización a las aplicaciones y datos con Hola controles hello y servicios que proporcionan una seguridad de hello toomanage de basados en la nube activos.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus necesidades de seguridad. Además, Azure le proporciona una amplia gama de toocontrol de capacidad de hello y opciones de seguridad configurables usarlas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones. Este documento le ayuda a cumplir estos requisitos.

### <a name="abstract"></a>Descripción breve

Microsoft Azure permite toorun aplicaciones y máquinas virtuales (VM) en la infraestructura física compartida. Una de las aplicaciones de toorunning Hola motivaciones económico primos en un entorno de nube cuesta Hola capacidad toodistribute Hola de recursos compartidos entre varios clientes. Esta práctica de multiinquilino mejora la eficiencia al multiplexar los recursos entre los distintos clientes a un bajo costo. Desafortunadamente, también supone un riesgo Hola de uso compartido de los servidores físicos y otro toorun de recursos de infraestructura de las aplicaciones confidenciales y las máquinas virtuales que pueden pertenecer tooan arbitrario y los usuarios con malas intenciones.

En este artículo se describe cómo Microsoft Azure proporciona aislamiento contra usuarios malintencionados y no intencionados y actúa como una guía para diseñar soluciones de nube, ya que ofrece diversas tooarchitects de las opciones de aislamiento. En este documento se centra en la tecnología de hello de la plataforma Windows Azure y controles de seguridad orientado al cliente y no intenta tooaddress SLA, modelos y consideraciones sobre los procedimientos DevOps de precios.

## <a name="tenant-level-isolation"></a>Aislamiento en el nivel de inquilino
Una de las principales ventajas de Hola de cloud computing es el concepto de una infraestructura común compartido por varios clientes simultáneamente, lo que tooeconomies de escala. Este concepto se denomina multiinquilinato. Microsoft trabaja continuamente tooensure que arquitectura multiempresa de Hola de nube de Microsoft Azure es compatible con los estándares de seguridad, confidencialidad, privacidad, integridad y disponibilidad.

En hello habilitada para la nube al área de trabajo, un inquilino puede definirse como un cliente u organización que posee y administra una instancia específica de ese servicio en la nube. Con la plataforma de identidad de hello proporcionada por Microsoft Azure, un inquilino es simplemente una instancia dedicada de Azure Active Directory (Azure AD) que su organización recibe y posee cuando suscribe a un servicio de nube de Microsoft.

Cada directorio de Azure AD es distinto e independiente de otros directorios de Azure AD. Al igual que un edificio de oficinas corporativos es un tooonly específico activo seguro su organización, un directorio de Azure AD también fue diseñado toobe un activo seguro para su uso únicamente por su organización. Hola arquitectura de Azure AD aísla la información de datos y la identidad de cliente de mezclen. Esto significa que los usuarios y los administradores de un directorio de Azure AD no tendrán acceso a los datos de otro directorio, ya sea de manera involuntaria o malintencionada.

### <a name="azure-tenancy"></a>Inquilinato de Azure
Azure multiempresa (suscripción de Azure) hace referencia tooa "al cliente y facturación" relación y un único [inquilino](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) en [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). El aislamiento en el nivel de inquilino en Microsoft Azure se logra con Azure Active Directory y los [controles basados en roles](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) que ofrece. Cada suscripción de Azure está asociada a un directorio de Azure Active Directory (AD).

Los usuarios, grupos y aplicaciones desde ese directorio pueden administrar recursos en hello suscripción de Azure. Puede asignar estos derechos de acceso mediante Hola portal de Azure, herramientas de línea de comandos de Azure y las API de administración de Azure. Un inquilino de Azure está aislado lógicamente mediante límites de seguridad de forma que ningún cliente puede acceder o poner en riesgo los coinquilinos, ya sea de forma malintencionada o por accidente. Azure AD se ejecuta en servidores sin sistema operativo, aislados en un segmento de red separado donde el filtrado de paquetes de nivel de host y Firewall de Windows bloquean el tráfico y las conexiones no deseadas.

- Toodata de acceso de Azure AD requiere la autenticación del usuario a través de un [servicio de token de seguridad (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Obtener información sobre la existencia del usuario de hello, el estado habilitado y la función se utiliza por toodetermine de sistema de autorización de hello si inquilino de destino de hello acceso solicitado toohello está autorizado para este usuario en esta sesión.

![Inquilinato de Azure](./media/azure-isolation/azure-isolation-fig1.png)


- Los inquilinos son contenedores separados y no hay ninguna relación entre ellos.

- No hay acceso entre inquilinos a menos que un administrador lo conceda mediante federación o el aprovisionamiento de cuentas de usuario de otros inquilinos.

- Acceso físico tooservers que componen el servicio de hello Azure AD y los sistemas de acceso directo tooAzure de AD back-end está restringido.

- Usuarios de Azure AD no tienen acceso a los activos toophysical ni ubicaciones y, por lo tanto, no es posible que les toobypass Hola RBAC directiva comprobaciones lógicas indicadas después.

Por razones de diagnóstico y mantenimiento, se necesita y utiliza un modelo de operaciones que emplee un sistema de elevación de privilegios Just-In-Time. Azure AD Privileged Identity Management (PIM) introduce el concepto de Hola de administrador elegibles. Los [administradores aptos](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) deben ser usuarios que necesiten acceso con privilegios de vez en cuando, pero no todos los días. rol de Hello está inactivo hasta que el usuario de hello necesita acceso, a continuación, completar un proceso de activación y convertirlo en un administrador activo de una cantidad de tiempo predeterminada.

![Administración de identidades con privilegios de Azure AD](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory hospeda a todos los inquilinos en su propio contenedor protegido, con las directivas y permisos tooand dentro de contenedor de hello solamente posee y administra el inquilino de Hola.

concepto de Hola de contenedores de inquilinos es profundamente arraigado en el servicio de directorio de hello en todas las capas, de portales todos Hola almacenamiento de manera toopersistent.

Hola mismo físico incluso cuando los metadatos de varios inquilinos de Azure Active Directory se almacenan en disco, no hay ninguna relación entre los contenedores de Hola que no sea la que se define por servicio de directorio de hello, que a su vez viene determinado por el Administrador de inquilinos de Hola.

### <a name="azure-role-based-access-control-rbac"></a>Control de acceso basado en rol (RBAC) de Azure
[Azure Control de acceso basado en roles (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) le ayuda a tooshare diversos componentes disponibles dentro de una suscripción de Azure mediante la administración de acceso específica de Azure. RBAC de Azure le permite toosegregate tareas dentro de su organización y conceder acceso en función de lo que los usuarios necesitan tooperform sus trabajos. En lugar de proporcionar a todos los empleados permisos no restringidos en los recursos o la suscripción de Azure, puede permitir solo determinadas acciones.

RBAC de Azure tiene tres funciones básicas que se aplican a tipos de recursos de tooall:

- **Propietario** tiene acceso completo tooall recursos incluidos hello toodelegate derecho acceso tooothers.

- **Colaborador** puede crear y administrar todos los tipos de recursos de Azure, pero no se puede conceder acceso tooothers.

- **lector** solo puede ver los recursos existentes de Azure.

![Control de acceso basado en rol de Azure](./media/azure-isolation/azure-isolation-fig3.png)

rest Hola de roles RBAC hello en Azure que admita la administración de recursos específicos de Azure. Por ejemplo, hello rol Colaborador de máquina Virtual permite toocreate de usuario de Hola y administrar máquinas virtuales. No les concede acceso toohello red Virtual de Azure o subred Hola Hola máquina virtual se conecta a.

[Funciones integradas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) enumera Hola roles disponibles en Azure. Especifica las operaciones de Hola y ámbito que cada rol integrado concede toousers. Si está pensando toodefine sus propios roles para tener un mayor control, vea cómo toobuild [roles personalizados en Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Otras funcionalidades de Azure Active Directory incluyen:
- Azure AD permite a las aplicaciones de tooSaaS SSO, independientemente de dónde se hospedan. Algunas aplicaciones están federadas con Azure AD y otras usan SSO con contraseña. Las aplicaciones federadas también pueden admitir aprovisionamiento de usuarios y [almacén de contraseñas](https://www.techopedia.com/definition/31415/password-vault).

- Acceso toodata en [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) se controla mediante la autenticación. Cada cuenta de almacenamiento tiene una clave principal ([clave de la cuenta de almacenamiento](https://docs.microsoft.com/azure/storage/storage-create-storage-account), o SAK) y una clave secreta secundaria (firma de acceso compartido de Hola o SAS).

- Azure AD proporciona identidad como servicio a través de la federación (mediante los [Servicios de federación de Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs)), sincronización y replicación de directorios locales.

- [La autenticación multifactor Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) es servicio de la autenticación multifactor de Hola que requiere inicios de sesión de los usuarios tooverify mediante el uso de una aplicación móvil, una llamada de teléfono o un mensaje de texto. Se puede utilizar con los recursos de Azure AD toohelp seguras en entornos con el servidor de la autenticación multifactor Azure hello y también con aplicaciones personalizadas o directorios que usan Hola SDK.

- [Servicios de dominio de Azure AD](https://azure.microsoft.com/services/active-directory-ds/) le permite unir el dominio de Active Directory de máquinas virtuales de Azure tooan sin implementar controladores de dominio. Puede iniciar sesión en las máquinas virtuales toothese con sus credenciales corporativas de Active Directory y administrar las máquinas virtuales Unidos a un dominio mediante líneas de base de seguridad de directiva de grupo tooenforce en todas las máquinas virtuales de Azure.

- [Azure B2C Directory Active](https://azure.microsoft.com/services/active-directory-b2c/) proporciona un servicio de administración de identidad global de alta disponibilidad para las aplicaciones orientadas al consumidor que escala toohundreds de millones de identidades. Se puede integrar en plataformas móviles y web. Los consumidores pueden iniciar sesión tooall sus aplicaciones a través de experiencias personalizables con sus cuentas sociales existentes o mediante la creación de credenciales.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Aislamiento de los administradores de Microsoft y eliminación de datos
Microsoft toma medidas seguro tooprotect los datos de acceso inadecuado o el uso por personas no autorizadas. Estos controles y procesos operativos están respaldados por hello [condiciones de los servicios en línea](http://aka.ms/Online-Services-Terms), ¿qué oferta compromisos contractuales que controlan los datos de tooyour de acceso.

-   Los ingenieros de Microsoft no tiene datos de tooyour de acceso predeterminados en la nube de Hola. En su lugar, se les concede acceso, bajo la supervisión de la administración, solo cuando sea necesario. El acceso se controla y registra cuidadosamente y se revoca tan pronto como deje de ser necesario.

-   Microsoft puede contratar a otros servicios de compañías tooprovide limitado en su nombre. Subcontratistas pueden tener acceso a datos toodeliver solo Hola los servicios al cliente para los cuales, que hemos contratado tooprovide y se les prohíbe usarla para ningún otro propósito. Además, son toomaintain contractualmente enlazado Hola confidencialidad de la información de nuestros clientes.

Servicios de negocio con certificaciones auditados como ISO/IEC 27001 con regularidad comprobada por Microsoft y accredited auditoría empresas, que realizan el ejemplo auditorías tooattest ese acceso a únicamente con finalidad comercial legítima. Siempre puede tener acceso a sus propios datos de cliente en cualquier momento y por cualquier motivo.

Si se elimina ningún dato, Microsoft Azure eliminará datos hello, incluidas las copias en memoria caché o copia de seguridad. Para los servicios en el ámbito, se producirá dicha eliminación dentro de 90 días después del final de Hola Hola de período de retención. (En el ámbito servicios se definen en la sección de términos de procesamiento de datos de Hola de nuestro [condiciones de los servicios en línea](http://aka.ms/Online-Services-Terms).)

Si una unidad de disco que se usa para el almacenamiento sufre un error de hardware, queda fijada [borran o destruye](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) antes de que Microsoft lo devuelve toohello fabricante para su reemplazo o reparación. Hello sobrescribe los datos en la unidad de hello tooensure que Hola datos no se puede recuperar por ningún medio.

## <a name="compute-isolation"></a>Aislamiento de proceso
Microsoft Azure proporciona diversos servicios informáticos en la nube que incluyen una amplia selección de instancias de proceso y servicios que se pueden escalar arriba y abajo automáticamente toomeet hello las necesidades de su aplicación o enterprise. Estas instancia de proceso y servicio ofrecen aislamiento con los datos de toosecure de varios niveles sin sacrificar la flexibilidad de hello en configuración que demandan los clientes.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Aislamiento de Hyper-V y sistema operativo raíz entre la máquina virtual raíz y las máquinas virtuales invitadas
La plataforma de proceso de Azure se basa en la virtualización, lo que significa que todo el código del cliente se ejecuta en una máquina virtual de Hyper-V. En cada nodo de Azure (o punto de conexión de red), hay un hipervisor que se ejecuta directamente a través de hardware de Hola y divide un nodo en un número variable de invitado las máquinas virtuales (VM).


![Aislamiento de Hyper-V y sistema operativo raíz entre la máquina virtual raíz y las máquinas virtuales invitadas](./media/azure-isolation/azure-isolation-fig4.jpg)


Cada nodo tiene también una VM raíz especial, que se ejecuta Hola SO Host. Un límite crítico es el aislamiento de Hola de hello raíz VM invitado hello las máquinas virtuales e invitado hello las máquinas virtuales entre sí, administrado por el hipervisor de Hola y Hola raíz SO. emparejamiento de Hello hipervisor/SO raíz aprovecha las décadas de Microsoft de la experiencia de seguridad del sistema operativo y aprendizaje más reciente a partir Hyper-V de Microsoft, tooprovide un aislamiento sólido de máquinas virtuales invitadas.

Hola plataforma Windows Azure usa un entorno virtualizado. Instancias de usuario funcionan como máquinas virtuales independientes que no tiene el servidor de acceso tooa host físico, y este aislamiento se aplica mediante los niveles de privilegios (anillo 0/anillo 3) del procesador físico.

Anillo 0 es hello más con privilegios y 3 es hello menos. SO invitado de Hola se ejecuta en un 1 de anillo con menos privilegios, y las aplicaciones se ejecutan Hola 3 de anillo con privilegios mínimos. Esta virtualización de los recursos físicos provoca una separación clara de tooa entre SO invitado e hipervisor, resultante de separación de seguridad adicional entre dos Hola.

Hola hipervisor Azure actúa como un micro-kernel y pasa todas las solicitudes de acceso de hardware del host de toohello de máquinas virtuales de invitado para su procesamiento mediante una interfaz de memoria compartida denominada VMBus. Esto impide que los usuarios obtengan sistema toohello de acceso de lectura/escritura/ejecución sin procesar y reduce el riesgo de Hola de uso compartido de recursos del sistema.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Algoritmo avanzado de selección de ubicación de la máquina virtual y protección frente a ataques de canal lateral
Cualquier ataque entre VM conlleva dos pasos: colocar una máquina virtual controlados por el adversario en hello mismo host como una víctima de hello las máquinas virtuales y, a continuación, infracción tooeither de límite de aislamiento de hello le roban información confidencial de la víctima o afectar a su rendimiento para codicia o el vandalismo. Microsoft Azure proporciona protección frente a ambos pasos mediante el uso de un algoritmo avanzado de selección de ubicación de máquinas virtuales y protección frente a todos los ataques de canal lateral conocidos, incluidos los ataques de máquinas virtuales vecinas que puedan generar ruido.

### <a name="hello-azure-fabric-controller"></a>Hola controlador de tejido de Azure
Hola controlador de tejido de Azure es responsable de asignar recursos de infraestructura tootenant cargas de trabajo y administra las comunicaciones unidireccionales desde equipos de toovirtual de host de Hola. Hola VM el algoritmo colocar de controlador de tejido de Azure de hello es muy sofisticado y sea casi imposible toopredict como nivel de host físico.

![Hola controlador de tejido de Azure](./media/azure-isolation/azure-isolation-fig5.png)

Hola hipervisor Azure exige la memoria y separación del proceso entre máquinas virtuales y lo enruta forma segura los inquilinos tooguest SO de tráfico de red. Esto elimina la posibilidad de cualquier ataque de canal lateral en el nivel de máquina virtual.

En Azure, raíz de hello VM es especial: se ejecuta un sistema operativo reforzado llamado SO raíz de Hola que hospeda un agente de tejido (FA). FAs se utilizan en Activar toomanage invitado agentes (GA) en sistemas operativos de invitado en la tabla customer máquinas virtuales. Los agentes de tejido también administran los nodos de almacenamiento.

colección de hipervisor de Azure, Hello root SO/FA y cliente máquinas virtuales/GAs consta de un nodo de proceso. Los agentes de tejido son administrados por un controlador de tejido que se encuentra fuera de los nodos de proceso y almacenamiento (los clústeres de proceso y almacenamiento se administran mediante controladores de tejido diferentes). Si un cliente actualiza el archivo de configuración de la aplicación mientras se está ejecutando, Hola FC se comunica con hello FA, que, a continuación, pone en contacto con GAs, que notificar a la aplicación hello de cambio de configuración de Hola. En caso de hello de un error de hardware, Hola FC automáticamente se encuentra hardware disponible y se reiniciará Hola máquina virtual no existe.

![Controlador de tejido de Azure](./media/azure-isolation/azure-isolation-fig6.jpg)

La comunicación de un agente de controlador de tejido tooan es unidireccional. agente de Hello implementa un servicio protegido por SSL que sólo responde toorequests de controlador de Hola. No se puede iniciar controlador toohello de conexiones o en otros nodos internos privilegiados. Hola FC trata todas las respuestas como si fueran de confianza.


![Controlador de tejido](./media/azure-isolation/azure-isolation-fig7.png)

Aislamiento se extiende desde Hola raíz virtual de máquinas virtuales invitadas y Hola máquinas virtuales invitadas entre sí. Los nodos de proceso también están aislados de los nodos de almacenamiento para mejorar la protección.


hipervisor de Hola y sistemas operativos de host de hello proporcionan paquetes de red: filtros toohelp garantizar que las máquinas virtuales que no se confía no puede generar tráfico simulado o recibir el tráfico dirigido no toothem, extremos de la infraestructura de dirigir el tráfico tooprotected o enviar/recibir tráfico de difusión inadecuado.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>Las reglas adicionales configuradas de agente de controlador de tejido tooIsolate VM
De forma predeterminada, todo el tráfico se bloquea cuando se crea una máquina virtual y, a continuación, el agente de controlador de tejido de Hola configura Hola filtro tooadd reglas y las excepciones tooallow autorizado tráfico de paquetes.

Se programan dos categorías de reglas:

-   **Reglas de configuración de la máquina o la infraestructura**: de forma predeterminada, se bloquea toda la comunicación. No existe es excepciones tooallow toosend de una máquina virtual y recibir tráfico DHCP y DNS. Máquinas virtuales también puede enviar tráfico toohello "public" internet y enviar tráfico tooother máquinas virtuales dentro de Hola misma red Virtual de Azure y Hola de sistema operativo de servidor de activación. lista de máquinas virtuales de Hola de destinos permitidos de salida no incluye subredes de enrutador de Azure, administración de Azure y otras propiedades de Microsoft.

-   **Archivo de configuración de rol:** define Hola listas de Control de acceso (ACL) entrantes en función de modelo de servicio del inquilino de Hola.

### <a name="vlan-isolation"></a>Aislamiento de VLAN
Hay tres redes VLAN en cada clúster:

![Aislamiento de VLAN](./media/azure-isolation/azure-isolation-fig8.jpg)


-   VLAN principal: Hello interconexiones nodos de cliente no es de confianza

-   Hello FC VLAN – contiene confianza FCs y los sistemas auxiliares

-   Hola dispositivo VLAN: contiene la red de confianza y otros dispositivos de infraestructura

Se permite la comunicación Hola FC VLAN toohello VLAN principal, pero no se puede iniciar desde Hola principal VLAN toohello FC VLAN. También se bloquea la comunicación dispositivo toohello VLAN principal de hello VLAN. Esto garantiza que incluso si un nodo que ejecuta el código de cliente se ve comprometido, no se puede atacar nodos en hello FC o dispositivo VLAN.

## <a name="storage-isolation"></a>Aislamiento de almacenamiento
### <a name="logical-isolation-between-compute-and-storage"></a>Aislamiento lógico entre proceso y almacenamiento
Como parte fundamental de su diseño, Microsoft Azure separa las máquinas virtuales de proceso y las de almacenamiento. Esta separación permite cálculo y almacenamiento tooscale por separado, lo que sea más fácil tooprovide multiempresa y aislamiento.

Por consiguiente, se ejecuta el almacenamiento de Azure en un equipo independiente con ningún tooAzure de conectividad de red se calcula excepto lógicamente. [Esto](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) significa que, cuando se crea un disco virtual, no se asigna espacio en disco para toda su capacidad. En su lugar, se crea una tabla que asigna direcciones en hello tooareas de disco virtual en el disco físico de Hola y que la tabla se muestra inicialmente vacía. **primera vez que un cliente escribe datos en el disco virtual de hello, se asigna espacio en disco físico de Hola y un tooit de puntero se coloca en la tabla de Hola Hola.**
### <a name="isolation-using-storage-access-control"></a>Aislamiento con Storage Access Control
**Azure Storage Access Control** tiene un modelo de control de acceso simple. Cada suscripción de Azure puede crear una o más cuentas de almacenamiento. Cada cuenta de almacenamiento tiene una clave secreta única que es usado toocontrol acceder a los datos tooall en esa cuenta de almacenamiento.

![Aislamiento con Storage Access Control](./media/azure-isolation/azure-isolation-fig9.png)

**Obtener acceso a datos de almacenamiento de tooAzure (incluidas las tablas)** puede controlarse a través de un [SAS (firma de acceso compartido)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) símbolo (token), que concede acceso de ámbito. Hello SAS se se creó mediante una plantilla de consulta (URL) firmada con hello [SAK (clave de cuenta de almacenamiento)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Que [firmado URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) puede indicarse tooanother proceso (que es, delegado), que puede, a continuación, rellene los detalles de Hola de consulta de Hola y realizar Hola solicitud de servicio de almacenamiento de Hola. Una SAS permite toogrant acceso temporal tooclients sin revelar la clave secreta de la cuenta de almacenamiento de Hola.

Hola SAS significa que podemos concedemos a que un cliente de permisos limitados, tooobjects en la cuenta de almacenamiento para un periodo de tiempo y con un conjunto de permisos especificado. Se pueden conceder estos permisos limitados sin necesidad de tooshare las claves de acceso de cuenta.

### <a name="ip-level-storage-isolation"></a>Aislamiento del almacenamiento en el nivel de dirección IP
Puede establecer firewalls y definir un intervalo de direcciones IP para los clientes de confianza. Con un intervalo de direcciones IP, solo los clientes que tienen una dirección IP dentro del intervalo definido de hello pueden conectarse demasiado[el almacenamiento de Azure](https://docs.microsoft.com/azure/storage/storage-security-guide).

Datos de almacenamiento de información IP se pueden proteger contra usuarios no autorizados a través de un mecanismo de red que es usado tooallocate un túnel dedicado o dedicado de almacenamiento de tooIP de tráfico.

### <a name="encryption"></a>Cifrado
Azure ofrece los siguientes tipos de datos de tooprotect de cifrado:
-   Cifrado en tránsito

-   Cifrado en reposo

#### <a name="encryption-in-transit"></a>Cifrado en tránsito
Cifrado en tránsito es un mecanismo para proteger datos cuando se transmiten a través de redes. Con Azure Storage, puede proteger los datos mediante:

-   [Cifrado de nivel de transporte](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), como HTTPS para transferir datos a Almacenamiento de Azure o desde este servicio.

-   [Cifrado en el cable](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), como el cifrado SMB 3.0 para recursos compartidos de Azure File.

-   [Cifrado en el cliente](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), datos de hello tooencrypt antes de transferirse a almacenamiento y toodecrypt datos de hello después de que se transfiere fuera de almacenamiento.

#### <a name="encryption-at-rest"></a>Cifrado en reposo
Para muchas organizaciones, el [cifrado de los datos en reposo](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) es un paso obligatorio en lo que respecta a la privacidad de los datos, el cumplimiento y la soberanía de los datos. Hay tres características de Azure que proporcionan cifrado de datos "en reposo":

-   [Cifrado de almacenamiento del servicio](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) permite que el servicio de almacenamiento de hello cifrar automáticamente los datos al escribir tooAzure almacenamiento de toorequest.

-   [Cifrado en el cliente](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) también proporciona características de Hola de cifrado en reposo.

-   [Cifrado del disco Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) permite tooencrypt discos de hello OS y discos de datos usados por una máquina virtual de IaaS.

#### <a name="azure-disk-encryption"></a>Azure Disk Encryption
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) para máquinas virtuales le ayuda solucionar los aspectos de seguridad y cumplimiento normativo de su organización, ya que cifra los discos de las máquinas virtuales (incluidos los discos de inicio y de datos) con claves y directivas que se controlan en [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Hola soluciones de cifrado del disco para Windows se basa en [el cifrado de unidad BitLocker de Microsoft](https://technet.microsoft.com/library/cc732774.aspx), y Hola solución Linux se basa en [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

solución de Hello admite Hola los escenarios siguientes para las máquinas virtuales IaaS cuando están habilitadas en Microsoft Azure:
-   Integración con el Almacén de claves de Azure

-   Máquinas virtuales de nivel estándar: máquinas virtuales IaaS de las series A, D, DS, G, GS, etc.

-   Habilitación del cifrado en máquinas virtuales IaaS Linux y Windows

-   Deshabilitación del cifrado en las unidades de datos y del sistema operativo en máquinas virtuales IaaS Windows

-   Deshabilitación del cifrado en unidades de datos en máquinas virtuales IaaS Linux

-   Habilitación del cifrado en máquinas virtuales IaaS que ejecutan el sistema operativo cliente de Windows

-   Habilitación del cifrado en volúmenes con rutas de montaje

-   Habilitación del cifrado en máquinas virtuales Linux configuradas con seccionamiento de disco (RAID) mediante [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Habilitación del cifrado en máquinas virtuales Linux mediante el uso de [LVM (administrador de discos lógicos)](https://msdn.microsoft.com/library/windows/desktop/bb540532) en los discos de datos

-   Habilitación del cifrado en máquinas virtuales con Windows configuradas mediante Espacios de almacenamiento

-   Se admiten todas las regiones públicas de Azure.

solución de Hello no admite Hola siguientes escenarios, características y tecnologías de la versión de Hola:

-   Máquinas virtuales IaaS de nivel básico

-   Deshabilitación del cifrado en una unidad del sistema operativo para máquinas virtuales IaaS Linux

-   Máquinas virtuales de IaaS que se crean mediante el método de creación de VM clásica de Hola

-   Integración con el Servicio de administración de claves local

-   Azure Files (sistema de archivos compartido), Network File System (NFS), volúmenes dinámicos y máquinas virtuales Windows configuradas con sistemas RAID basadas en software

## <a name="sql-azure-database-isolation"></a>Aislamiento de base de datos de SQL Azure
Base de datos SQL es un servicio de base de datos relacional en la nube de Microsoft hello basándose en el motor de Microsoft SQL Server del líder del mercado de Hola y capaz de controlar las cargas de trabajo críticas. SQL Database ofrece aislamiento de datos predecible en el nivel de cuenta, basado en región o área geográfica, o basado en red, todo ello con una administración prácticamente inexistente.

### <a name="sql-azure-application-model"></a>Modelo de aplicación de SQL Azure

[Microsoft SQL Azure Database](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) es un servicio de base de datos relacional en la nube que se basa en la tecnología de SQL Server. Proporciona un servicio de base de datos de alta disponibilidad, escalable y multiinquilino, hospedado por Microsoft en la nube.

Desde una perspectiva de aplicación SQL Azure proporciona Hola después de jerarquía: cada nivel tiene contención de uno a varios de los niveles inferiores.

![Modelo de aplicación de SQL Azure](./media/azure-isolation/azure-isolation-fig10.png)

suscripción y la cuenta de hello son administración y la facturación de tooassociate de conceptos de plataforma de Microsoft Azure.

Servidores y bases de datos lógicas son conceptos específicos de SQL Azure y se administran mediante SQL Azure, que proporciona interfaces OData y TSQL, o bien con el portal de SQL Azure integrado en Azure Portal.

Los servidores de SQL Azure no son físicos ni instancias de máquinas virtuales, son colecciones de bases de datos que comparten administración y directivas de seguridad almacenadas en una base de datos llamada “maestra lógica”.

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Las bases de datos “maestras lógicas” incluyen:

-   Los inicios de sesión SQL utilizan tooconnect toohello server

-   Reglas de firewall

Información de facturación y relacionados con el uso para bases de datos de SQL Azure de hello no son el mismo servidor lógico garantiza toobe en hello misma instancia físico en clúster de SQL Azure, en su lugar, las aplicaciones deben proporcionar el nombre de base de datos de destino de hello al conectarse.

Desde la perspectiva del cliente, se crea un servidor lógico en una región geográfica gráfica mientras creación real del saludo del servidor hello se produce en uno de los clústeres de hello en la región de Hola.

### <a name="isolation-through-network-topology"></a>Aislamiento mediante topología de red

Cuando se crea un servidor lógico y se registra su nombre DNS, el nombre DNS de hello puntos toohello que se denomina dirección "VIP de puerta de enlace" en el centro de datos específicos de Hola donde se coloca los servidor hello.

Detrás de hello VIP (dirección IP virtual), tenemos una colección de servicios de puerta de enlace sin estado. En general, las puertas de enlace se ven involucradas cuando hay necesidades de coordinación entre varios orígenes de datos (base de datos maestra, base de datos de usuario, etc). Los servicios de puerta de enlace implementar siguiente hello:
-   **Proxy de conexión TDS.** Esto incluye Buscar base de datos de usuario en el clúster de back-end de hello, implementar la secuencia de inicio de sesión de hello y, a continuación, reenviar back y Hola TDS paquetes toohello back-end.

-   **Administración de bases de datos.** Esto incluye la implementación de una colección de operaciones de base de datos de los flujos de trabajo toodo CREATE/ALTER/DROP. se pueden invocar operaciones de base de datos de Hello rastrear los paquetes TDS o explícita APIs OData.

-   Operaciones de usuario, de inicio de sesión, CREATE, ALTER y DROP

-   Operaciones de administración del servidor lógico a través de API de OData

![Aislamiento mediante topología de red](./media/azure-isolation/azure-isolation-fig12.png)

nivel de Hello detrás de las puertas de enlace de Hola se denomina "back-end". Esto es donde se almacenan todos los datos de hello en un modo de alta disponibilidad. Cada sector de datos es toobelong dicha tooa "partición" o "unidad de conmutación por error", cada uno de ellos tiene al menos tres réplicas. Las réplicas se almacenan y replican por el motor de SQL Server y administradas por un tooas de sistema a menudo denominado "tejido" de conmutación por error.

Por lo general, sistema de back-end de hello no comunicar tooother saliente sistemas como precaución de seguridad. Se trata de sistemas toohello reservadas en la capa de hello front-end (puerta de enlace). máquinas de nivel de puerta de enlace de Hello tienen privilegios limitados en superficie expuesta a ataques Hola máquinas de back-end toominimize Hola como un mecanismo de defensa en profundidad.

### <a name="isolation-by-machine-function-and-access"></a>Aislamiento por función y acceso de la máquina
SQL Azure se compone de servicios que se ejecutan en máquinas de funciones diferentes. SQL Azure se divide en base de datos en la nube "back-end" y "front-end" entornos (/ administración de puerta de enlace), con el principio general de Hola de curso solo de tráfico al back-end y no espera. entorno de front-end de Hello toohello fuera de mundo de los demás servicios puede comunicar y por lo general, solo tiene permisos limitados en hello back-end (suficiente toocall Hola puntos de entrada necesidades tooinvoke).

## <a name="networking-isolation"></a>Aislamiento de red
La implementación de Azure tiene varios niveles de aislamiento de red. Hello siguiente diagrama muestra diferentes niveles de aislamiento de red que Azure proporciona toocustomers. Estos niveles son los modos nativo en hello plataforma Windows Azure propio y funciones definidas por el cliente. Entrada de Hola Internet DDoS de Azure proporciona aislamiento frente a ataques a gran escala en Azure. Hola siguiente nivel de aislamiento es definido por el cliente direcciones IP públicas (extremos), que son utilizado toodetermine qué tráfico puede pasar a través de la red virtual de hello en la nube servicio toohello. El aislamiento de la red virtual de Azure nativa garantiza un aislamiento completo de todas las demás redes y que el tráfico solo fluya a través de los métodos y las rutas de acceso configurados por el usuario. Estas rutas de acceso y los métodos son capa siguiente de hello, donde los NSG, UDR y dispositivos de red virtual pueden ser usado toocreate aislamiento límites tooprotect hello las implementaciones de aplicaciones en red Hola protegido.

![Aislamiento de red](./media/azure-isolation/azure-isolation-fig13.png)

**Aislamiento del tráfico:** A [red virtual](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) es el límite de aislamiento de tráfico de hello en hello plataforma Windows Azure. Máquinas virtuales (VM) en una red virtual no se puede comunicar directamente tooVMs en una red virtual diferente, incluso si ambas redes virtuales se crean por Hola a mismo cliente. El aislamiento consiste en una propiedad fundamental que garantiza que las máquinas virtuales del cliente y la comunicación sigan siendo privadas en una red virtual.

[Subred](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) ofrece un nivel de aislamiento adicional de la red virtual basado en un intervalo de direcciones IP. Direcciones IP de red virtual de hello, puede dividir una red virtual en varias subredes para la organización y la seguridad. Máquinas virtuales y PaaS rol instancias implementadas toosubnets (iguales o distintos) dentro de una red virtual pueden comunicarse entre sí sin ninguna configuración adicional. También puede configurar [grupo de seguridad de red (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow o denegar instancia de máquina virtual de tooa de tráfico de red según las reglas configuradas en la lista de control de acceso (ACL) del NSG. Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred. Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall instancias de máquina virtual de hello en esa subred.

## <a name="next-steps"></a>Pasos siguientes

- [Opciones de aislamiento de red para máquinas Windows en redes virtuales de Azure](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Esto incluye Hola clásico front-end y back-end escenario donde pueden permitir sólo las máquinas en una determinada red de back-end o subred ciertos clientes u otro equipos tooconnect tooa punto de conexión determinado en función de una lista blanca de direcciones IP.

- [Aislamiento de proceso](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure proporciona un servicios informáticos distintos en la nube que incluyen una amplia selección de instancias de proceso y servicios que se pueden escalar arriba y abajo automáticamente toomeet hello las necesidades de su aplicación o enterprise.

- [Aislamiento del almacenamiento](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure separa la computación basada en máquinas virtuales de cliente del almacenamiento. Esta separación permite cálculo y almacenamiento tooscale por separado, lo que sea más fácil tooprovide multiempresa y aislamiento. Por consiguiente, se ejecuta el almacenamiento de Azure en un equipo independiente con ningún tooAzure de conectividad de red se calcula excepto lógicamente. Todas las peticiones se ejecutan sobre HTTP o HTTPS, a elección del cliente.

