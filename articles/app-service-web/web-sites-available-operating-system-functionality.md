---
title: funciones del sistema aaaOperating en el servicio de aplicaciones de Azure
description: "Obtenga información acerca de hello SO funcionalidad disponible tooweb aplicaciones back-ends de aplicaciones móviles y aplicaciones de API de servicio de aplicaciones de Azure"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Funcionalidad del sistema operativo en el Servicio de aplicaciones de Azure
Hola comunes previsto funciones del sistema operativo que está disponible tooall aplicaciones que se ejecutan este artículo describen [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Esta funcionalidad incluye archivo, red, acceso de registro, registros de diagnóstico y eventos. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>Niveles de plan del Servicio de aplicaciones
El Servicio de aplicaciones ejecuta aplicaciones cliente en un entorno de hospedaje multiempresa. Aplicaciones implementadas en hello **libre** y **Shared** niveles se ejecutan en procesos de trabajo en máquinas virtuales compartidas, mientras las aplicaciones implementadas en hello **estándar** y  **Premium** niveles que se ejecutan en máquinas virtuales dedicados específicamente para aplicaciones de hello asociadas con un solo cliente.

Dado que el servicio de aplicación admite una experiencia perfecta con escala entre los diferentes niveles, configuración de seguridad de hello exige para los Hola de sigue siendo de aplicaciones de servicio de aplicaciones igual. Esto garantiza que las aplicaciones no repentinamente comportan de manera diferente, errores inesperados, cuando cambia el plan de servicio de aplicaciones de tooanother de un nivel.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Marcos de desarrollo
Servicio de aplicaciones precios cantidad de Hola de control de los niveles de recursos de proceso (CPU, almacenamiento en disco, memoria y salida de red) tooapps disponibles. Sin embargo, amplitud de Hola de framework funcionalidad disponible tooapps permanece Hola que mismo con independencia de Hola niveles de ajuste de escala.

El Servicio de aplicaciones es compatible con una gran variedad de marcos de desarrollo, incluidos ASP.NET, ASP clásico, node.js, PHP y Python (todos se ejecutan como extensiones en IIS). En orden toosimplify y normalizar la configuración de seguridad, aplicaciones de servicio de aplicaciones suelen ejecutan Hola diversos marcos de desarrollo con su configuración predeterminada. Un enfoque tooconfiguring aplicaciones podrían haber resultado área expuesta de toocustomize Hola API y la funcionalidad para cada marco de trabajo de desarrollo individuales. Por el contrario, el Servicio de aplicaciones adopta un enfoque más genérico mediante la habilitación de una línea base común de la funcionalidad del sistema operativo independientemente de un marco de desarrollo de la aplicación.

Hello las secciones siguientes resumen tipos generales de Hola de aplicaciones de servicio de sistema operativo funcionalidad tooApp disponible.

<a id="FileAccess"></a>

## <a name="file-access"></a>Acceso a archivos
Existen varias unidades en el Servicio de aplicaciones, incluidas las unidades locales y las unidades de red.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Unidades locales
En esencia, servicio de aplicaciones es un servicio que se ejecuta sobre infraestructura de hello Azure PaaS (plataforma como servicio). Como consecuencia, las unidades locales Hola que "había conectado" máquina virtual de tooa hello mismo rol de trabajo de tooany disponibles de los tipos de unidad ejecutan en Azure. Esto incluye una unidad de sistema operativo (Hola unidad D:\), una unidad de aplicación que contiene los archivos de cspkg de paquete de Azure de uso exclusivo por el servicio de aplicaciones (y toocustomers inaccesible) y una unidad de "usuario" (Hola unidad C:\), cuyo tamaño varía según el tamaño de Hola Hola máquina virtual.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Unidades de red (también conocidas como recursos compartidos UNC)
Uno de los aspectos exclusivos de Hola de servicio de aplicaciones que facilita la implementación de aplicación y mantenimiento es que todo el contenido de usuario se almacena en un conjunto de recursos compartidos de UNC. Este modelo asigna muy bien toohello patrón común de almacenamiento de contenido usa web local entornos que tienen varios servidores con equilibrio de carga de hospedaje. 

En el Servicio de aplicaciones existen varios recursos compartidos UNC creados en cada centro de datos. Porcentaje del contenido de usuario de Hola para todos los clientes en cada centro de datos se asigna tooeach recurso compartido UNC. Además, todo el contenido del archivo de Hola para una única suscripción de cliente de se sitúa siempre en hello comparten el mismo UNC. 

Tenga en cuenta que debido a los servicios de nube toohow funcionan, Hola determinada máquina virtual responsable de hospedaje de un recurso compartido UNC cambiará con el tiempo. Se garantiza que los recursos compartidos de UNC se montará por distintas máquinas virtuales tal y como se ponen de arriba y abajo durante el curso normal de Hola de las operaciones de nube. Por esta razón, aplicaciones nunca deben realizar suposiciones codificado de forma rígida que información de la máquina de hello en una ruta de acceso de archivo UNC permanecerá estable con el tiempo. En su lugar, deben usar Hola cómoda *falsa* ruta de acceso absoluta **D:\home\site** que proporciona el servicio de aplicaciones. Esta ruta de acceso absoluta falsa proporciona un método portátil, independiente de aplicación y usuario para hacer referencia a aplicación del tooone. Mediante el uso de **D:\home\site**, uno puede transferir archivos compartidos de aplicación tooapp sin necesidad de tooconfigure una nueva ruta de acceso absoluta para cada transferencia.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Tipos de acceso a archivos conceden tooan aplicación
Cada suscripción de cliente tiene una estructura de directorio reservada en un recurso compartido UNC específico dentro de un centro de datos. Un cliente puede tener varias aplicaciones que se crean dentro de un centro de datos específicos, por lo que todos los directorios de Hola que pertenece la suscripción de cliente único de tooa se crean en hello mismo recurso compartido UNC. recurso compartido de Hello puede incluir directorios como los relativos a contenido, error y registros de diagnóstico y las versiones anteriores de la aplicación hello creados por el control de código fuente. Según lo esperado, los directorios de la aplicación de un cliente están disponibles para acceso de lectura y escritura en tiempo de ejecución mediante código de aplicación de la aplicación hello.

En hello las unidades locales habían adjuntado toohello máquina que ejecuta una aplicación, servicio de aplicaciones se reserva un fragmento de espacio en la unidad C:\ para el almacenamiento local temporal de específico de la aplicación hello. Aunque una aplicación tiene acceso completo de lectura/escritura tooits propietario temporal almacenamiento local, que el almacenamiento no es en realidad toobe previsto usar directamente el código de la aplicación hello. En su lugar, la intención de hello es almacenar archivos temporales de tooprovide para marcos de aplicaciones de IIS y web. Servicio de aplicaciones también limita la cantidad de Hola de almacenamiento local temporal disponible tooeach aplicación tooprevent aplicaciones individuales de consumen una gran cantidad de almacenamiento de archivos local.

Dos ejemplos de cómo el servicio de aplicaciones usa almacenamiento local temporal son directory Hola para archivos temporales de ASP.NET y los archivos comprimidos de directorio de Hola para IIS. Hola sistema de compilación de ASP.NET utiliza directorio "Archivos temporales de ASP.NET" de hello como una ubicación de caché de compilación temporales. IIS utiliza la salida de respuesta de Hola "IIS Temporary Compressed Files" directorio toostore comprimido. Estos dos tipos de archivo uso (así como otros usuarios) se reasignan en almacenamiento local de servicio de aplicaciones tooper aplicación temporal. Esta reasignación garantiza que la funcionalidad continúa según lo esperado.

Cada aplicación de servicio de aplicaciones se ejecuta como una identidad del proceso aleatorio trabajo con pocos privilegios único llamado hello "aplicación identidad del grupo", se describe más adelante aquí: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Código de la aplicación usa esta identidad para la unidad del sistema operativo de acceso de solo lectura básico toohello (Hola unidad D:\). Esto significa que el código de aplicación puede enumerar estructuras de directorio comunes y leer archivos comunes en la unidad del sistema operativo. Aunque esto podría aparecer toobe un nivel ligeramente más amplio de acceso, Hola mismos directorios y archivos son accesibles cuando se aprovisiona un rol de trabajo en un Azure servicio hospedado y lee el contenido de la unidad de Hola. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Acceso al archivo en varias instancias
directorio particular de Hello contiene contenido de una aplicación y código de la aplicación puede escribir tooit. Si una aplicación se ejecuta en varias instancias, directorio particular de Hola se comparte entre todas las instancias para que todas las instancias ver Hola mismo directorio. Por ejemplo, si una aplicación guarda directorio particular de los archivos cargados toohello, esos archivos son instancias de tooall disponible de inmediato. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Acceso de red
Código de la aplicación puede usar TCP/IP y UDP según protocolos toomake saliente de red conexiones tooInternet accesibles los extremos que exponen servicios externos. Aplicaciones pueden usar estos mismos tooservices tooconnect de protocolos dentro de Azure &#151; por ejemplo, mediante el establecimiento de conexiones de HTTPS tooSQL base de datos.

También hay una capacidad limitada para conexión aplicaciones tooestablish un bucle invertido local, y tiene una aplicación escuche en ese socket de bucle invertido local. Esta característica existe principalmente aplicaciones tooenable que escuchen en sockets de bucle invertido local como parte de su funcionalidad. Tenga en cuenta que cada aplicación ve una conexión de bucle invertido "privada"; aplicación "A" no puede escuchar el socket de bucle invertido local tooa establecido por la aplicación "B".

Las canalizaciones con nombre también son compatibles como un mecanismo de comunicación entre procesos (IPC) entre los distintos procesos que ejecutan conjuntamente una aplicación. Por ejemplo, módulo de FastCGI de IIS de Hola basa en las canalizaciones con nombre toocoordinate Hola los procesos individuales que se ejecutan las páginas PHP.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>Memoria, procesos y ejecución de código
Como se indicó anteriormente, las aplicaciones se ejecutan dentro de los procesos de trabajo con privilegios reducidos mediante una identidad aleatoria de grupo de aplicaciones. Código de la aplicación dispone de espacio de memoria de acceso toohello asociado con el proceso de trabajo de hello, así como los procesos secundarios que pueden ser creados por los procesos CGI u otras aplicaciones. Sin embargo, una aplicación no puede obtener acceso a memoria de Hola o datos de otra aplicación incluso si se trata de Hola misma máquina virtual.

Las aplicaciones pueden ejecutar scripts o páginas escritas con marcos de desarrollo web compatibles. Servicio de aplicaciones no configura los modos de web framework configuración toomore restringido. Por ejemplo, aplicaciones ASP.NET que se ejecutan en el servicio de aplicaciones se ejecutan en confianza "completa" como modo de confianza opuestos tooa más restringido. Marcos de trabajo Web, como ASP clásico y ASP.NET, pueden llamar a componentes COM en proceso (pero no fuera de los componentes de COM de proceso), como ADO (ActiveX Data Objects) que se registran de forma predeterminada en el sistema operativo de Windows hello.

Las aplicaciones pueden dividir y ejecutar código arbitrario. Es permitida para un cosas toodo de aplicación como generar un shell de comandos o ejecutar un script de PowerShell. Sin embargo, aunque se puede generar procesos y código arbitrario desde una aplicación, programas ejecutables y secuencias de comandos son toohello restringirán privilegios concedidos toohello primarios grupo de aplicaciones. Por ejemplo, una aplicación puede generar un archivo ejecutable que realiza una llamada HTTP saliente, pero ese mismo ejecutable no puede intentar toounbind dirección IP de Hola de una máquina virtual desde su equipo de NIC. Realizar una llamada de red saliente se permite el código con privilegios toolow, pero intentar tooreconfigure configuración de red en una máquina virtual requiere privilegios administrativos.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Eventos y registros de diagnóstico
Información de registro es otro conjunto de datos que algunas aplicaciones intentan tooaccess. tipos de Hola de toocode disponible en la información de registro ejecuta en el servicio de aplicaciones incluye diagnóstico y registrar información generada por una aplicación que también es aplicación toohello fácilmente accesibles. 

Por ejemplo, los registros de W3C HTTP generados por una aplicación active están disponibles en un directorio de registro en la red de hello ubicación del recurso compartido creado para la aplicación hello o disponible en almacenamiento de blobs, si un cliente ha configurado la toostorage de registro de W3C. Hola última opción permite grandes cantidades de toobe registros recopilados sin riesgo de Hola de exceder el límite de almacenamiento de archivo hello asociado a un recurso compartido de red.

En un modo similar, los diagnósticos en tiempo real también se puede registrar información desde las aplicaciones de .NET mediante la infraestructura de seguimiento y diagnóstico de .NET de hello, con opciones toowrite Hola recurso compartido de red de la aplicación de seguimiento información tooeither Hola o, alternativamente, el almacenamiento de blobs de tooa ubicación.

Áreas de diagnósticos de registro y seguimiento que no están disponibles tooapps son los eventos ETW de Windows y registros de eventos comunes de Windows (por ejemplo, sistema, aplicación y seguridad de registros de eventos). Puesto que la información de seguimiento ETW potencialmente puede verse eventos de todo el equipo (con el derecho de hello ACL), acceso de lectura y escritura tooETW se bloquean. Pueden observar los desarrolladores esa API llama tooread y escritura de los eventos ETW y registros de eventos de Windows comunes aparecen toowork, pero eso es porque el servicio de aplicación es "falsificación de" hello llamadas para que aparezcan toosucceed. En realidad, código de la aplicación hello no tiene ningún dato de eventos de acceso toothis.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Acceso al registro
Las aplicaciones tienen acceso de sólo lectura toomuch (aunque no todos) del registro de hello de máquina virtual de Hola se ejecutan en. En la práctica, esto significa que las claves del registro que permiten al grupo local de usuarios de acceso de solo lectura toohello son accesibles para las aplicaciones. Un área de registro de hello que no se admite actualmente para lectura o acceso de escritura es hello HKEY\_actual\_subárbol del usuario.

Registro de acceso de escritura toohello está bloqueado, incluidas las claves del registro de acceso tooany por usuario. Desde la perspectiva de la aplicación hello, acceso de escritura toohello registro nunca se debería confiar en Hola entorno de Azure ya que las aplicaciones pueden (y hacer) se pueden migrar entre diferentes máquinas virtuales. Hola solo puede escribir el almacenamiento persistente que puede depender de una aplicación es la estructura de directorio de contenido por aplicación Hola almacenado en recursos compartidos de UNC de servicio de aplicación de Hola. 

## <a name="more-information"></a>Más información

[Espacio aislado de aplicación Web Azure](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -Hola mayoría de la información actualizada sobre el entorno de ejecución de Hola de servicio de aplicaciones. Esta página se mantiene directamente por Hola, equipo de desarrollo de servicio de aplicaciones.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 


