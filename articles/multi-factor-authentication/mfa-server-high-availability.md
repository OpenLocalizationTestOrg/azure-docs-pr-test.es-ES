---
title: aaaConfigure servidor Azure MFA para lograr alta disponibilidad | Documentos de Microsoft
description: Implemente varias instancias del Servidor Microsoft Azure Multi-Factor Authentication en configuraciones que proporcionan alta disponibilidad.
services: multi-factor-authentication
keywords: Azure MFA
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Configuración del Servidor Microsoft Azure Multi-Factor Authentication para la alta disponibilidad

tooachieve alta disponibilidad con la implementación de servidor de Azure MFA, necesita toodeploy varios servidores MFA. Esta sección proporciona información sobre un diseño de equilibrio de carga tooachieve los objetivos de alta disponibilidad en el que la implementación de servidor de Azure MFS.

## <a name="mfa-server-overview"></a>Introducción al Servidor MFA

Hola arquitectura del servicio servidor de MFA de Azure consta de varios componentes como se muestra en hello siguiente diagrama:

 ![Arquitectura del Servidor MFA](./media/mfa-server-high-availability/mfa-ha-architecture.png)

Un servidor de MFA es un servidor de Windows que tenga instalado el software de la autenticación multifactor Azure Hola. instancia del servidor de MFA de Hello debe activarse Hola servicio MFA en Azure toofunction. Se puede instalar más de una instancia del Servidor MFA en el entorno local.

Hola es el primer servidor de MFA que se instala Hola servidor MFA principal tras la activación por hello servicio MFA de Azure de forma predeterminada. servidor MFA maestro de Hello tiene una copia de escritura de base de datos de hello PhoneFactor.pfdata. Las instalaciones posteriores de instancias del Servidor MFA se conocen como subordinadas. esclavos MFA de Hello tienen una copia replicada de solo lectura de base de datos de hello PhoneFactor.pfdata. Las instancias del Servidor MFA replican información mediante la llamada a procedimiento remoto (RPC). Todos los servidores de MFA deben colectivamente ser Unidos a un dominio o información de tooreplicate independiente.

MFA maestro y subordinado servidores MFA que comunican Hola servicio MFA cuando se requiere autenticación de dos factores. Por ejemplo, cuando un usuario intenta aplicación tooan de toogain access que requiere autenticación en dos fases, usuario Hola se autenticarán en primer lugar por un proveedor de identidad, como Active Directory (AD).

Tras la autenticación correcta con AD, Hola servidor MFA se comunicará con hello servicio MFA. Hola servidor MFA espera para recibir la notificación Hola servicio MFA tooallow o denegar la aplicación de toohello de acceso de usuario de hello.

Si el servidor maestro de hello MFA se queda sin conexión, las autenticaciones todavía pueden ser procesadas, pero no se puede procesar las operaciones que requieren la base de datos de cambios toohello MFA. (Algunos ejemplos son: Hola adición de usuarios, autoservicio cambios de PIN y cambiar la información de usuario)

## <a name="deployment"></a>Implementación

Considere la posibilidad de hello siguientes puntos son importantes para el servidor de MFA de Azure y sus componentes relacionados de equilibrio de carga.

* **Con alta disponibilidad RADIUS estándar tooachieve**. Si usa instancias del Servidor Azure MFA como servidores RADIUS, puede configurar un Servidor MFA como un destino de autenticación de RADIUS principal y otras instancias del Servidor Azure MFA como destinos de autenticación secundarios. Sin embargo, esta disponibilidad alta de método tooachieve puede no resultar práctica porque debe esperar un toooccur de período de tiempo de espera si falla la autenticación en el destino de autenticación principal Hola antes de que se pueda autenticar con la autenticación secundaria Hola destino. Resulta más eficaz tooload saldo Hola RADIUS del tráfico entre el cliente RADIUS de Hola y servidores RADIUS de hello (en este caso, hello Azure MFA servidores que actúan como servidores RADIUS) para que pueda configurar los clientes RADIUS de hello con una sola dirección URL que señalan a.
* **Necesita toomanually promover esclavos MFA**. Si el servidor principal de Azure MFA de Hola se queda sin conexión, hello Azure MFA servidores secundarios continúan tooprocess MFA solicitudes. Sin embargo, hasta que un servidor maestro de MFA está disponible, administradores no pueden agregar usuarios o modificar la configuración de MFA, y los usuarios no pueden realizar cambios mediante el portal de usuarios de Hola. Promoción de una función de maestro de MFA esclavo toohello siempre es un proceso manual.
* **Separación de los componentes**. Hola servidor MFA de Azure consta de varios componentes que se pueden instalar en Hola misma instancia del servidor de Windows o en varias instancias. Estos componentes incluyen hello Portal de usuarios, el servicio Web de aplicación móvil y el adaptador de AD FS hello (agente). Esta cláusula de salvedad hace posible toouse Hola Proxy de aplicación Web toopublish Hola Portal de usuarios móviles servidor y aplicación Web desde la red perimetral de Hola. Este tipo de configuración agrega toohello seguridad global del diseño, como se muestra en hello siguiente diagrama. Hola Portal de usuarios de MFA y el servidor de Web de aplicación móvil también pueden implementarse en configuraciones de alta disponibilidad con equilibrio de carga

   ![Servidor MFA con una red perimetral](./media/mfa-server-high-availability/mfasecurity.png)

* **Contraseña temporal (OTP) a través de SMS (también conocido como SMS unidireccionales) requiere el uso de Hola de sesiones permanentes si es de tráfico con equilibrio de carga**. SMS unidireccional es una opción de autenticación que provoca que los usuarios de Hola de hello servidor MFA toosend un mensaje de texto que contiene una OTP. usuario de Hello escribe Hola OTP en un hello toocomplete de ventana de símbolo del sistema desafío MFA. Si los servidores de MFA de Azure equilibra la carga, hello mismo servidor que atienden solicitudes de autenticación inicial de hello debe ser Hola servidor que recibe el mensaje de bienvenida de OTP de usuario Hola; Si otro servidor MFA recibe Hola respuesta OTP, se produce un error de desafío de autenticación de Hola. Para obtener más información, consulte [contraseña temporal a través de SMS agrega tooAzure servidor MFA](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **Las implementaciones de equilibrio de carga del Portal de usuarios de Hola y de servicio de la aplicación Web móvil requieren sesiones permanentes**. Si es el equilibrio de carga Hola Portal de usuarios de MFA y Hola servicio de Web de aplicación móvil, cada sesión debe toostay en hello mismo servidor.

## <a name="high-availability-deployment"></a>Implementación de alta disponibilidad

Hello siguiente diagrama muestra una implementación de equilibrio de carga de alta disponibilidad completa de MFA de Azure y sus componentes, junto con ADFS como referencia.

 ![Implementación de alta disponibilidad del Servidor Azure MFA](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Tenga en cuenta Hola siguientes elementos para el área de hello numerado según corresponda de hello anterior diagrama.

1. Hola son dos servidores de MFA de Azure (MFA1 y MFA2) (mfaapp.contoso.com) con equilibrio de carga y está configurado toouse una base de datos de puerto estático (4443) tooreplicate hello PhoneFactor.pfdata. Hola SDK del servicio Web está instalado en cada uno de comunicación de hello servidor MFA tooenable en el puerto TCP 443 con servidores ADFS de Hola. servidores MFA de Hola se implementan en una configuración con equilibrio de carga sin estado. Sin embargo, si deseara toouse OTP a través de SMS, debe usar el equilibrio de carga con estado.
   ![Servidor Azure MFA: alta disponibilidad del servidor de aplicaciones](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > Dado que utiliza puertos dinámicos de RPC, no se recomienda firewalls tooopen seguridad toohello intervalo de puertos dinámicos que potencialmente pueden usar RPC. Si tiene un firewall **entre** los servidores de aplicaciones de MFA, debe configurar Hola servidor MFA toocommunicate en un puerto estático para el tráfico de replicación Hola entre servidores esclavo y maestro y abrir ese puerto en el firewall. Puede forzar el puerto estático de hello mediante la creación de un valor de Registro DWORD en ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` denominado ```Pfsvc_ncan_ip_tcp_port``` y establecer valor de hello tooan puerto disponible. Las conexiones se inicien siempre maestro de hello esclavo servidores MFA toohello, puerto estático de hello solo es necesario en el patrón de hello, pero puesto que puede promocionar a un patrón de hello toobe esclavo en cualquier momento, debe establecer puerto estático de hello en todos los servidores de MFA.

2. Hola dos de los servidores de aplicación móvil MFA del Portal de usuario (MFA-UP-MAS1 y MFA-UP-MAS2) son equilibrada de carga en un **stateful** configuración (mfa.contoso.com). Recuerde que las sesiones permanentes son un requisito para equilibrio de carga Hola Portal de usuarios de MFA y el servicio de aplicación móvil.
   ![Servidor Azure MFA: alta disponibilidad del servicio de aplicación móvil y del Portal de usuarios](./media/mfa-server-high-availability/mfaportal.png)
3. granja de servidores de AD FS de Hello es equilibrio de carga y publicado toohello Internet a través de servidores proxy ADFS con equilibrio de carga en la red perimetral de Hola. Cada servidor de AD FS usa Hola ADFS agente toocommunicate con hello servidores de MFA de Azure con una URL única con equilibrio de carga (mfaapp.contoso.com) en el puerto TCP 443.

## <a name="next-steps"></a>Pasos siguientes

* [Instalación y configuración del Servidor Azure MFA](multi-factor-authentication-get-started-server.md)
