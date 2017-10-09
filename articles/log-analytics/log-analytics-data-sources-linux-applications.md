---
title: "rendimiento de la aplicación de Linux en OMS Log Analytics aaaCollect | Documentos de Microsoft"
description: "Este artículo proporciona detalles para configurar hello agente de OMS para Linux toocollect los contadores de rendimiento para el servidor HTTP Apache y MySQL."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Recopilar los contadores de rendimiento para aplicaciones de Linux en Log Analytics 
Este artículo proporciona detalles para configurar hello [agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect los contadores de rendimiento para aplicaciones específicas.  las aplicaciones de Hello incluidas en este artículo son:  

- [MySQL](#MySQL)
- [Servidor HTTP de Apache](#apache-http-server)

## <a name="mysql"></a>MySQL
Si el servidor MySQL o MariaDB se detecta en el equipo de hello cuando se instala el agente de OMS hello, se instalará automáticamente un proveedor de MySQL Server de supervisión de rendimiento. Este proveedor conecta el estadísticas de rendimiento para tooexpose el local servidor MySQL/MariaDB toohello. Las credenciales de usuario de MySQL deben configurarse para que hello proveedor pueda acceder Hola MySQL Server.

### <a name="configure-mysql-credentials"></a>Configurar las credenciales de MySQL
Hola proveedor de OMI de MySQL necesita un usuario de MySQL preconfigurado e instala las bibliotecas de cliente de MySQL en orden tooquery Hola información de rendimiento y mantenimiento de la instancia de MySQL Hola.  Estas credenciales se almacenan en un archivo de autenticación que se almacena en el agente de Linux Hola.  archivo de autenticación de Hello especifica la dirección de enlace y puerto Hola está escuchando instancia de MySQL, así como las credenciales toouse toogather métricas.  

Durante la instalación del programa Hola a agente de OMS para Linux hello OMI de MySQL proveedor examinará los archivos de configuración my.cnf de MySQL (ubicaciones predeterminadas) para la dirección de enlace y puerto parcialmente conjunto hello y archivo de autenticación de OMI de MySQL.

archivo de autenticación de MySQL Hola se almacena en `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Formato del archivo de autenticación
Aquí te mostramos formato Hola Hola archivo de autenticación de OMI de MySQL

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

en hello en la tabla siguiente se describen las entradas de Hello en el archivo de autenticación de hello.

| Propiedad | Descripción |
|:--|:--|
| Port | Representa Hola Hola de puerto actual instancia de MySQL está escuchando. Puerto 0 especifica que se usan las propiedades de hello siguientes para la instancia predeterminada. |
| Dirección de enlace| Dirección de enlace actual de MySQL. |
| nombre de usuario| Usuario de MySQL usa la instancia del servidor de MySQL de toouse toomonitor Hola. |
| Contraseña codificada en Base64| Contraseña del usuario supervisión de MySQL Hola codificada en Base64. |
| Actualización automática| Especifica si se toorescan para los cambios en el archivo my.cnf de hello y sobrescribir el archivo de autenticación de OMI de MySQL de hello cuando hello proveedor de OMI de MySQL se actualiza. |

### <a name="default-instance"></a>Instancia predeterminada
Hola archivo de autenticación de OMI de MySQL puede definir una instancia predeterminada y toomake de número de puerto administrar varias instancias de MySQL en un host Linux.  instancia predeterminada de Hola se indica mediante una instancia con el puerto 0. Todas las instancias adicionales heredarán propiedades establecidas en la instancia predeterminada de Hola a menos que especifiquen valores diferentes. Por ejemplo, si se agrega la instancia de MySQL que escucha en el puerto '3308', dirección de enlace, nombre de usuario y contraseña codificada en Base64 de instancia predeterminada de Hola se puede tootry usado y supervisar la instancia de hello escucha en 3308. Si la instancia de hello en 3308 está enlazada tooanother dirección y usa Hola el mismo nombre de usuario de MySQL y se necesita contraseña par solo Hola dirección de enlace y hello otras propiedades se heredarán.

Hello en la tabla siguiente tiene una configuración de la instancia de ejemplo 

| Descripción | Archivo |
|:--|:--|
| Instancia predeterminada e instancia con el puerto 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Instancia predeterminada e instancia con el puerto 3308 y nombre de usuario y contraseña diferentes. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Programa del archivo de autenticación de MySQL para OMI
Instalación de Hola de hello OMI de MySQL proveedor incluye un programa de archivo de autenticación de OMI de MySQL que puede ser el archivo de autenticación de OMI de MySQL de hello tooedit usado. programa Hello del archivo de autenticación se puede encontrar en hello ubicación siguiente.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> archivo de credenciales de Hello debe ser legible por cuenta de hello omsagent. Se recomienda ejecutar comando de hello mycimprovauth como omsgent.

Hello tabla siguiente proporciona detalles acerca de la sintaxis de hello para el uso de mycimprovauth.

| Operación | Ejemplo | Descripción
|:--|:--|:--|
| actualización automática *false\|true* | mycimprovauth autoupdate false | Conjuntos de archivo de autenticación de Hola o no se actualizarán automáticamente en reiniciar o actualizar. |
| *nombre de usuario y contraseña de la dirección de enlace* predeterminada | mycimprovauth default 127.0.0.1 root pwd | Conjuntos de Hola instancia predeterminada en el archivo de autenticación de OMI de MySQL Hola.<br>campo de contraseña de Hola se debe escribir en texto sin formato: contraseña de hello en el archivo de autenticación de OMI de MySQL Hola será codificada en Base 64. |
| eliminar *valor predeterminado\|número de puerto* | mycimprovauth 3308 | Elimina la instancia especificada de hello ya sea predeterminada o por número de puerto. |
| help | mycimprov help | Imprime una lista de comandos toouse. |
| imprimir | mycimprov print | Imprime una fácil tooread archivo de autenticación de OMI de MySQL. |
| actualizar *nombre de usuario y contraseña de la dirección de enlace* del número de puerto | mycimprov update 3307 127.0.0.1 root pwd | Actualiza la instancia especificada de Hola o agrega la instancia de hello si no existe. |

Hello comandos de ejemplo siguiente definen una cuenta de usuario predeterminada para el servidor de MySQL de hello en localhost.  campo de contraseña de Hola se debe escribir en texto sin formato: contraseña de hello en el archivo de autenticación de OMI de MySQL Hola será codificada en Base 64

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Permisos necesarios de la base de datos para los contadores de rendimiento de MySQL
Hola usuario de MySQL requiere toohello de acceso después de las consultas toocollect datos de rendimiento del servidor MySQL. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


usuario de MySQL de Hello también requiere toohello acceso exclusivo siguientes tablas de forma predeterminada.

- information_schema
- mysql. 

Estos privilegios se pueden conceder ejecutando Hola siguientes comandos de concesión.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant permisos tooa MySQL supervisión Hola usuario conceder el usuario debe tener Hola privilegio 'GRANT option', así como tener concedido el privilegio de Hola.

### <a name="define-performance-counters"></a>Definir contadores de rendimiento

Una vez que configure hello agente de OMS para Linux toosend datos tooLog análisis, debe configurar toocollect de contadores de rendimiento de Hola.  Utilice el procedimiento de hello en [orígenes de datos de rendimiento de Windows y Linux en análisis de registros](log-analytics-data-sources-windows-events.md) con contadores de hello en hello en la tabla siguiente.

| Nombre de objeto | Nombre del contador |
|:--|:--|
| Base de datos MySQL | Espacio en disco en bytes |
| Base de datos MySQL | Tablas |
| MySQL Server | Porcentaje de conexiones anuladas |
| MySQL Server | Porcentaje de uso de conexión |
| MySQL Server | Uso de espacio en disco en bytes |
| MySQL Server | Porcentaje de análisis de tabla completa |
| MySQL Server | Porcentaje de aciertos del grupo de búferes InnoDB |
| MySQL Server | Porcentaje de uso del grupo de búferes InnoDB |
| MySQL Server | Porcentaje de uso del grupo de búferes InnoDB |
| MySQL Server | Porcentaje de aciertos de la caché de claves |
| MySQL Server | Porcentaje de uso de la caché de claves |
| MySQL Server | Porcentaje de escritura de la caché de claves |
| MySQL Server | Porcentaje de aciertos de la caché de consultas |
| MySQL Server | Porcentaje de eliminaciones de la caché de consultas |
| MySQL Server | Porcentaje de uso de la caché de consultas |
| MySQL Server | Porcentaje de aciertos de la caché de tablas |
| MySQL Server | Porcentaje de uso de la caché de tablas |
| MySQL Server | Porcentaje de contención de bloqueo de tablas |

## <a name="apache-http-server"></a>Servidor HTTP de Apache 
Si se detecta servidor HTTP Apache en el equipo de hello cuando se instala el paquete de hello omsagent, se instalará automáticamente un proveedor para el servidor HTTP Apache de supervisión de rendimiento. Este proveedor se basa en un módulo de Apache que se debe cargar en hello servidor HTTP Apache orden tooaccess los datos de rendimiento. Hola módulo se puede cargar con hello siguiente comando:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload Hola supervisión módulo Apache, ejecute el siguiente comando de hello:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Definir contadores de rendimiento

Una vez que configure hello agente de OMS para Linux toosend datos tooLog análisis, debe configurar toocollect de contadores de rendimiento de Hola.  Utilice el procedimiento de hello en [orígenes de datos de rendimiento de Windows y Linux en análisis de registros](log-analytics-data-sources-windows-events.md) con contadores de hello en hello en la tabla siguiente.

| Nombre de objeto | Nombre del contador |
|:--|:--|
| Servidor HTTP de Apache | Trabajadores ocupados |
| Servidor HTTP de Apache | Trabajadores inactivos |
| Servidor HTTP de Apache | Porcentaje de trabajadores ocupados |
| Servidor HTTP de Apache | Porcentaje total de CPU |
| Host virtual de Apache | Errores por minuto, cliente |
| Host virtual de Apache | Errores por minuto, servidor |
| Host virtual de Apache | KB por solicitud |
| Host virtual de Apache | KB de solicitudes por segundo |
| Host virtual de Apache | Solicitudes por segundo |



## <a name="next-steps"></a>Pasos siguientes
* [Recopilar contadores de rendimiento](log-analytics-data-sources-performance-counters.md) en agentes de Linux.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones. 
