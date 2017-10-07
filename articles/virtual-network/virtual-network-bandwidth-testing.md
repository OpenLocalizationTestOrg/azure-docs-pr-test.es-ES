---
title: "rendimiento de red de máquina virtual de Azure aaaTesting | Documentos de Microsoft"
description: "Obtenga información acerca de cómo el rendimiento de la red de tootest máquina virtual de Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Pruebas de ancho de banda y rendimiento (NTTTCP)

Al probar el rendimiento de la red en Azure, es mejor toouse una herramienta que tenga como destino de red de Hola para pruebas y minimiza el uso de Hola de otros recursos que puede afectar al rendimiento. Se recomienda NTTTCP.

Copiar Hola herramienta tootwo máquinas virtuales de Azure de hello mismo tamaño. Una máquina virtual funciona como hello otro como receptor y remitente.

#### <a name="deploying-vms-for-testing"></a>Implementación de máquinas virtuales para pruebas
Para fines de Hola de esta prueba, Hola dos máquinas virtuales deben estar en Hola mismo servicio en la nube u Hola el mismo conjunto de disponibilidad para que podamos usar su direcciones IP internas y excluir Hola equilibradores de carga de la prueba de Hola. Es posible tootest con hello VIP, pero este tipo de pruebas está fuera de ámbito de Hola de este documento.
 
Tome nota de la dirección IP del destinatario Hola. Vamos a llamar a esa dirección IP "a.b.c.r".

Tome nota del número de Hola de núcleos en hello máquina virtual. Llamémoslo "\#num\_cores".
 
Ejecute hello NTTTCP comprobar 300 segundos (o 5 minutos) en hello remitente VM y el receptor máquina virtual.

Sugerencia: Al configurar esta prueba para hello primera vez, puede intentar antes una menor comentarios tooget período de prueba. Una vez que la herramienta de hello funciona según lo esperado, extender a segundos de too300 período de prueba de Hola para obtener resultados más precisos Hola.

> [!NOTE]
> remitente de Hello **y** receptor debe especificar **Hola mismo** parámetro de duración de la prueba (-t).

tootest un único flujo TCP durante 10 segundos:

Parámetros de receptor: ntttcp -r -t 10 -P 1

Parámetros de remitente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> Hola anterior ejemplo solo deben tooconfirm usa la configuración. Más adelante en este documento se ofrecen ejemplos válidos de pruebas.

## <a name="testing-vms-running-windows"></a>Pruebas de máquinas virtuales que ejecutan WINDOWS:

#### <a name="get-ntttcp-onto-hello-vms"></a>Obtener NTTTCP en hello las máquinas virtuales.

Descargar la versión más reciente de hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Si no se encuentra en esa página, realice esta búsqueda <https://www.bing.com/search?q=ntttcp+download>\< (debe ser el primer resultado).

Considere la colocar NTTTCP en una carpeta independiente, como c:\\tools.

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Permitir NTTTCP a través de firewall de Windows hello
En hello receptor, cree una regla de permiso en tooallow de Firewall de Windows hello el tooarrive de tráfico NTTTCP. Resulta más fácil tooallow Hola todo NTTTCP programa por su nombre en lugar de puertos TCP específicos de tooallow de entrada.

Permitir ntttcp a través de hello Firewall de Windows como el siguiente:

netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Por ejemplo, si ha copiado ntttcp.exe toohello "c:\\herramientas" carpeta, esto sería el comando hello: 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Ejecución de pruebas de NTTTCP

Iniciar NTTTCP en hello receptor (**ejecutar desde CMD**, no de PowerShell):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Si Hola VM tiene cuatro núcleos y una dirección IP de 10.0.0.4, sería similar al siguiente:

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Iniciar NTTTCP en hello remitente (**ejecutar desde CMD**, no de PowerShell):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Esperar los resultados de Hola.


## <a name="testing-vms-running-linux"></a>Pruebas de máquinas virtuales que ejecutan LINUX:

Use nttcp-for-linux. Está disponible en <https://github.com/Microsoft/ntttcp-for-linux>.

En hello máquinas virtuales de Linux (remitente y receptor), ejecute estos comandos para preparar ntttcp para linux en las máquinas virtuales:

CentOS: instalación de Git:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu: instalación de Git:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Cree e instale en ambas:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Como en el ejemplo de Windows hello, suponemos que IP del receptor de hello Linux es 10.0.0.4

Iniciar NTTTCP para Linux en hello receptor:

``` bash
ntttcp -r -t 300
```

Y en hello remitente, ejecute:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Se proporciona too60 segundos si ningún parámetro de tiempo de prueba longitud valores predeterminados

## <a name="testing-between-vms-running-windows-and-linux"></a>Pruebas entre máquinas virtuales que ejecutan Windows y Linux:

En escenarios de esta se deberíamos habilite el modo de sincronización no Hola por lo que puede ejecutar la prueba de Hola. Esto se realiza mediante hello **-N marca** para Linux, y **marca -ns** para Windows.

#### <a name="from-linux-toowindows"></a>Desde tooWindows de Linux:

Receptor<Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Remitente<Linux> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Desde Windows tooLinux:

Receptor<Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Remitente<Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Pasos siguientes
* Dependiendo de los resultados, puede haber espacio demasiado[optimizar máquinas de rendimiento de red](virtual-network-optimize-network-bandwidth.md) para su escenario.
* Más información sobre [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network](virtual-networks-faq.md)
