---
title: aaaOptions para migrar de RemoteApp de Azure | Documentos de Microsoft
description: "Obtenga información acerca de las opciones de Hola para migrar de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Opciones para realizar una migración desde Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.


Si se han dejado de usar Azure RemoteApp debido a hello [anuncio de retirada](https://go.microsoft.com/fwlink/?linkid=821148) o porque haya terminado la evaluación, necesitará toomigrate fuera de servicio de aplicaciones de Azure RemoteApp tooanother. Hay dos enfoques diferentes de migración: una implementación autoadministrada (también denominada "infraestructura como servicio" [IaaS]) o una oferta totalmente administrada (a menudo denominada "plataforma como servicio" o "software como servicio"·[PaaS y SaaS respectivamente]). 

El IaaS de autoservicio es una implementación donde el usuario es el responsable y quien se encarga de administrarla y realizarla en sistemas físicos o máquinas virtuales. En hello otro finalizar una completamente administrado PaaS/oferta de SaaS es más, como Azure RemoteApp: un socio proporciona un nivel de servicio por encima de una solución de acceso remoto que controla operativa y de mantenimiento, mientras el equipo, como cliente de hello, realice algunas administración de aplicaciones y de imagen.

[Ver seminarios Web de Azure RemoteApp hello en Opciones de migración](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), o siga leyendo para obtener más información (con ejemplos de hello diferente opciones de hospedaje).

## <a name="self-managed-iaas-solutions"></a>Soluciones autoadministradas (IaaS)
### <a name="rds-on-iaas"></a>**RDS en IaaS**
Puede implementar una implementación nativa basada en sesiones de Servicios de Escritorio remoto (en Windows Server) mediante RemoteApp o escritorios locales, o bien en un entorno hospedado (como en máquinas virtuales de Azure). La opción de RDS en implementaciones de IaaS es más adecuada para los clientes que ya están familiarizados con esta herramienta y que tienen experiencia técnica en implementaciones de RDS. 

> [!NOTE]
> Se necesita con Software Assurance (SA) de licencias por volumen para toouse de licencias de acceso de cliente RDS esta opción de implementación.

Implementar RDS en máquinas virtuales de Azure es más fácil que nunca cuando se utilizan plantillas de implementación y aplicación de revisiones (lea una [Introducción](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) y, luego, [descárguelas](https://aka.ms/rdautomation)). Puede obtener Hola mismas capacidades de escala elásticas con recursos de modelo de implementación clásico de Azure (no los recursos de modelo de recursos de Azure) en Azure RemoteApp mediante hello [Autoescala script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), aunque haya más las personalizaciones y configuraciones. Al implementar RDS en máquinas virtuales de Azure, se admiten a través de [Azure admite](https://azure.microsoft.com/support/plans/), Hola mismo profesionales de soporte técnico que es compatible con Azure RemoteApp. Se pueden obtener estimaciones de costos en función de su uso existente poniéndose en contacto [soporte técnico de Azure](https://azure.microsoft.com/support/plans/), o se pueden realizar cálculos mediante un poco toobe libera Calculadora de costo.  Además, con máquinas virtuales de serie N (actualmente en private preview), puede agregar vGPU - oír más acerca de cómo agregar vGPU y sobre cómo demasiado[aprovechar las mejoras de RDS en Windows Server 2016](https://myignite.microsoft.com/videos/2794) en nuestra sesión Ignite.   

Contamos con guías de implementación paso a paso de [Windows Server 2012 R2](http://aka.ms/rdsonazure) y [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist con la implementación. Extraer del repositorio hello [blog de escritorio remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para las últimas noticias de Hola.

### <a name="citrix-on-iaas"></a>**Citrix en IaaS**
Las implementaciones nativas de Citrix de las aplicaciones XenApp o XenDesktop basadas en sesiones pueden realizarse en entornos locales u hospedados (por ejemplo, en máquinas virtuales de Azure). 

Visite la Guía de implementación paso a paso de hello, [Citrix XA 7.6 en Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), para obtener más información. Consulte más detalles sobre [Citrix en Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), donde podrá utilizar también una calculadora de precios. También puede encontrar un [Citrix póngase en contacto con](http://citrix.com/English/contact/index.asp) toodiscuss las opciones con.

## <a name="fully-managed-paassaas-offerings"></a>Ofertas completamente administradas (PaaS y SaaS)

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (publicado en abril de 2017)
Está disponible ahora en hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials es servicio de virtualización de aplicaciones nueva hello, combinación de energía de Hola y Hola de flexibilidad de plataforma de nube de Citrix Hola simples, preceptivo, y fácil de consumir visión de Microsoft Azure RemoteApp. 

Los clientes de Azure RemoteApp existentes pueden [registrarse para obtener una evaluación gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Nota: Solo el gasto de servicio de usuario de Citrix es gratis. Se aplican costos de almacenamiento y proceso de Azure.

Más información:
- [Migrar de Azure RemoteApp tooCitrix XenApp Essentials](remoteapp-migrate-citrix.md)
- [Citrix y Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Presentación de Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Servicios Citrix Cloud XenApp y XenDesktop 

[Citrix XenApp servicio nube y XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) es Hola mejor solución para la entrega de Hola de las aplicaciones y escritorios, más avanzadas de administración y capacidades de supervisión. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (nombre de la plataforma: MyCloudIT)
[MyCloudIT](https://mycloudit.com) es una plataforma de automatización para toosimplify de empresas de TI, optimizar y escalar la migración de Hola y Hola de entrega de escritorios remotos, las aplicaciones remotas y la infraestructura de nube de Microsoft Azure. 

plataforma de Hello MyCloudIT reduce el tiempo de implementación al 95%, Azure costos al 30% y mueve toda infraestructura de TI de su cliente en la nube de hello en cuestión de unas pocas pulsaciones de teclas. Socios ahora pueden administrar los clientes de un panel global, los usuarios finales de servicio alrededor de Hola a todos como nunca antes y aumentar los ingresos sin tener que agregar una sobrecarga adicional o una amplia capacitación de Azure.  

> Ubicación principal: Dallas, Texas (Estados Unidos)
> 
> Región operativa: en todo el mundo
> 
> Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Proveedor de servicios en la nube de Microsoft: sí
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas
> 
> Soluciones de migración de Azure RemoteApp: sí [(más información)](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, vicepresidente de Desarrollo Empresarial
> 
> Teléfono: 972-218-0741
>   
> Correo electrónico: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Frame

Las organizaciones de TI en enterprise y gubernamentales, proveedores de servicios administrados y proveedores de software líderes elija marco toocreate y administración sus áreas de trabajo seguros y definidas por el software en la nube de Hola. De toolarge pequeñas organizaciones, marco hace toolet increíblemente fácil a los usuarios tener acceso a aplicaciones de Windows en cualquier explorador desde cualquier dispositivo. Hello plataforma marco incluye todo lo que un administrador necesidades toodeploy aplicaciones de nube Hola incluidos Hola infraestructura de Azure y las licencias RDS (volver a poner su propia cuenta de Azure y las licencias es opcional). 

Obtenga más información sobre [Frame en Azure](https://www.fra.me/ara). 

> Ubicación principal: San Mateo, California (Estados Unidos)
>
> Región operativa: en todo el mundo
>
> Asociado de Microsoft: Sí
> 
> Teléfono: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu proporciona una solución de área de trabajo en línea simple ejecutando aplicaciones heredadas, SaaS y documentos desde un explorador de html5. Por lo tanto, realizando todas las aplicaciones disponibles de forma segura en cualquier tipo de dispositivo. Para los servicios de SaaS, existe una amplia gama de opciones de inicio de sesión único de operaciones disponible. También los sistemas de archivos diferentes (nube) se pueden integrar totalmente en el área de trabajo. Movilidad de toofull siguiente, área de trabajo en línea del Awingu enriquecido le dará una seguridad óptima con controles granulares (por ejemplo, carga y descarga), uso completo de auditoría, la autenticación multifactor (p. ej., Azure MFA), la grabación de sesión y mucho más. La solución de Awingu, que se encuentra lista para usarse, permite el uso compartido de sesión de la aplicación y documento para la colaboración segura y optimizada.
Dicha solución es una API abierta de varios AD y de varios inquilinos. La usan pequeñas y grandes empresas, proveedores de servicio en la nube e [ISV](http://www.isv2saas.com). Estos clientes especialmente aprecian Hola fácil de usar, TCO de facilidad de instalación y bajo.

Es Awingu All-in-One [disponibles en Azure Marketplace hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) con 2 usuarios simultáneos integrados. Las licencias adicionales están disponibles a través de una [amplia gama de distribuidores y revendedores](http://www.awingu.com/reseller).

Obtenga más información sobre [Awingu en como alternativo tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Ubicación principal: Bélgica
> 
> Regiones de funcionamiento: EMEA, Norteamérica y Brasil
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas 
> 
> **Global**:
> 
> Arnaud Marlière, director de marketing
> 
> Correo electrónico: [arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Teléfono: +1 646 583 3025
> 
> **Sede de Bélgica**:
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> Correo electrónico: [info@awingu.com](mailto:info@awingu.com) 
> 
> Teléfono: +32 9 296 40 11
> 
> **EE. UU.**:
> 
> 7 floor, 1177 Ave de hello Americas,
> 
> Nueva York, NY 10036
> 
> Correo electrónico: [info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Proveedor de servicios hospedados de Microsoft
Socios de hospedaje normalmente ofrecen un completamente administrado hospeda el escritorio de Windows y Hola de servicio de aplicaciones, que puede incluir la administración de recursos de Azure, sistemas operativos, aplicaciones y departamento de soporte técnico con los socios de Hola de licencias de contratos con Microsoft y otros proveedores de software junto con que se va a un contrato de licencia de proveedor de servicio tooallow revender licencias de acceso de suscriptor (SAL). Hello siguiente información proporciona detalles e información de contacto para algunos de los proveedores de hospedaje de Hola que se especializan en ayudando a los clientes con su migración de Azure RemoteApp. Extraer del repositorio [lista actual de Hola de proveedores de servicios hospedados](http://aka.ms/rdsonazurecertified) que finalizaron Hola RDS en IaaS evaluación y la ruta de acceso de aprendizaje.  

### <a name="citrix-service-provider-program"></a>Programa de proveedor de servicios de Citrix
Hola Citrix el programa de proveedor de servicio facilita la sencillez de Hola de toodeliver de proveedores de servicio de virtual cloud computing tooSMBs, oferta de servicios de hello desean ver en un modelo de pago por uso, fácil. Proveedores de servicios de Citrix crecer sus negocios de Microsoft SPLA y ampliar sus inversiones en plataformas RDS con cualquier dispositivo, acceso desde cualquier lugar, Hola más amplia compatibilidad de aplicación, una rica experiencia, lograr una mayor seguridad y una mayor escalabilidad. A su vez, proveedores de servicios de Citrix atraen a más suscriptores, aumentan la satisfacción del cliente y reducen los costos operativos. [Obtenga más información](http://www.citrix.com/products/service-providers.html) o [busque un asociado](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) se especializa en proporcionar soluciones de escritorio hospedadas, entregar todo el escritorio y aplicaciones de ISV experiencias creadas en Microsoft tooa global cliente de la tecnología base de Azure y sus propios centros de datos.

> Ubicación principal: Londres, Reino Unido; Singapur; Houston, Texas
> 
> Región operativa: en todo el mundo
> 
> Estado de asociado: Gold
> 
> Proveedor de servicios en la nube de Microsoft: sí
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas
> 
> Soluciones de migración de Azure RemoteApp: sí [(más información)](http://www.acuutech.com/ara-migration/)
> 
> **Reino Unido**:
>   
> 5/6 York House, Langston Road,
>   
> Loughton, Essex IG10 3TQ
>   
> Teléfono: +44 (0) 20 8502 2155
> 
> **Singapur**:
>   
> 100 Cecil Street, #09-02, 
>   
> Hola mundo, Singapur 069532
> 
> Teléfono: +65 6709 4933
>   
> **Norteamérica**:
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, TX 77098
>   
> Teléfono: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) se especializa en ISV transición toohello en la nube y ISV' busca toooptimize sus configuraciones de nube actuales. ASPEX ofrece una amplia gama de servicios administrados, DevOps y servicios de consultoría.  

> Ubicación principal: Amberes, Bélgica
> 
> Región operativa: Europa Occidental
> 
> Estado de asociado: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Proveedor de servicios en la nube de Microsoft: sí
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas
> 
> Soluciones de migración de Azure RemoteApp: sí [(más información)](https://www.aspex.be/en/azure-remote-apps)
> 
> Teléfono: +3232202198
> 
> Correo electrónico: [info@aspex.be](mailto:info@aspex.be)
> 
> Sitio web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) ayuda a las empresas, gobiernos locales, cuerpos no gubernamentales e instituciones sanitarios con su viaje hacia una manera más inteligente de trabajo en Microsoft Cloud Hola. Sea productivo y esté protegido en cualquier lugar, con cualquier dispositivo y a un bajo costo de TI. Caase.com es un verdadero especialista en Microsoft Office365, Azure, Enterprise Mobility and Security y Windows. Con nuestra asesoría, servicios de migración, programas de adopción, aprendizaje, administración y respaldo, Caase.com crea una plataforma optimizada y segura de colaboración entre los proveedores, asociados y empleados de los clientes.
Caase.com es mastermind Hola de hello al área de trabajo Digital (sociales Intranet) y hello Azure remoto Workspace (área de trabajo móvil). Ambas soluciones: llevar a cabo con la adopción: son foundation Hola que garantiza que los usuarios de Hola de estas soluciones tienen experiencia más agradable, correcta y eficaz de hello en su toohello ruta Microsoft Cloud.
Aquí puede encontrar una traducción al neerlandés y una película de respaldo: http://caase.com/over-ons/

> Región de la operación: empresa neerlandesa con alcance mundial
> 
> Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Proveedor de servicios en la nube de Microsoft: sí
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas
> 
> Soluciones de migración de Azure RemoteApp: sí [(más información)](http://caase.com/diensten/microsoft-azure/)
> 
> 
> Países Bajos:
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Teléfono: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio para Azure](http://getnerdio.com/nfa/) es una plataforma de automatización de TI que ofrece provisioning demasiado simple, administración y optimización de los entornos de TI completos en hello nube de Microsoft. Optimice escritorios virtuales, aplicaciones remotas y servidores en un par de horas. Administrar el entorno de hello en tres clics o menor con Nerdio del Portal de administración. Usar inteligente la escala automática y guarde el 40% de too60 en recursos de IaaS de Azure.

> Ubicación principal: Chicago, IL Región de la operación: en todo el mundo Estado de asociado: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Proveedor de servicios en Microsoft Cloud: sí
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas
> 
> Soluciones de migración de Azure RemoteApp: sí
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> EE. UU.
> 
> (844) 4NERDIO ext. 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) ofrece las soluciones en la nube públicas y privadas (Azure) de la cartera completa de Microsoft Dynamics (NAV, AX, GP, SL y CRM).

> Ubicación principal: Países bajos
> 
> Región operativa: en todo el mundo
> 
> Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Proveedor de servicios en la nube de Microsoft: sí
> 
> Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas
> 
> **EMEA**:
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> Hola países bajos
> 
> Teléfono: + 31 20 547 8060 
> 
>  **América**:
> 
> 171 Saxony Road, Suite 105
> 
> Encinitas, CA 92024
> 
> San Diego
> 
> Estados Unidos
> 
> Teléfono: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil Street
>    
> \#11-08, Hola octágono
> 
> Singapur 069534
> 
> Singapur
>   
> Teléfono (Singapur): + 65 6222 6591
> 
> Teléfono (Australia): + 61 2 8310 5568 
>    
> Teléfono (Nueva Zelanda): + 64 4 488 0321
> 
## <a name="need-more-help"></a>¿Necesita más ayuda?
¿Todavía necesita ayuda para decidirse o tiene más preguntas? Utilice uno de hello siguiendo métodos tooget ayuda. 

1. Envíenos un correo electrónico a [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
2. Póngase en contacto con el equipo de [soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Comience abriendo un [caso de soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Llámenos. [Encuentre un número de ventas local](https://azure.microsoft.com/overview/sales-number/).

