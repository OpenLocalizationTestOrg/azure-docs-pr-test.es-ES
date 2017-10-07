---
title: aaaRun Casandra con Linux en Azure | Documentos de Microsoft
description: "Cómo toorun una Casandra de Cluster Server en Linux en máquinas virtuales de Azure desde una aplicación Node.js."
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Ejecución de Cassandra con Linux en Azure y acceso desde Node.js
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Consulte las plantillas de Resource Manager para [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) y el [clúster de Spark y Cassandra en CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Información general
Microsoft Azure es una plataforma de nube abierta que ejecuta tanto software de Microsoft como ajeno a Microsoft que incluye sistemas operativos, servidores de aplicaciones, middleware de mensajería, así como bases de datos SQL y NoSQL tanto de modelos comerciales como de código abierto. Crear servicios resistentes en nubes públicas, incluido Azure, requiere una cuidadosa planeación y una arquitectura deliberada para ambos servidores de aplicaciones, así como capas de almacenamiento. La arquitectura de almacenamiento distribuido de Cassandra ayuda naturalmente a crear sistemas de alta disponibilidad que son tolerantes a errores de clúster. Cassandra es una base de datos NoSQL de escala de nube mantenida por Apache Software Foundation en cassandra.apache.org; Cassandra está escrita en Java y, por tanto, se ejecuta tanto en plataformas Windows como Linux.

enfoque Hola de este artículo es la implementación de Casandra tooshow en Ubuntu, ejecute como un clúster único y múltiples data center aprovechar las máquinas virtuales de Microsoft Azure y redes virtuales. Hello para cargas de trabajo de producción con optimización para la implementación del clúster se fuera del ámbito de este artículo porque requiere la configuración de disco de múltiples nodos, diseño de la topología de anillo adecuado y toosupport Hola de modelado de datos necesitan replicación, la coherencia de los datos, rendimiento y requisitos de alta disponibilidad.

Esta forma de artículo un tooshow enfoque fundamentales las implicaciones de creación Hola clúster Casandra en comparación con Docker, Chef o Puppet lo que puede hacer Hola mucho más fácil de implementación de la infraestructura.  

## <a name="hello-deployment-models"></a>Hola modelos de implementación
Redes de Microsoft Azure permiten la implementación de Hola de clústeres privados aislados, acceso Hola de los cuales puede ser tooattain restringido seguridad de un problema de red específica.  Puesto que este artículo trata sobre la que muestra la implementación de Casandra hello en un nivel fundamental, no nos centraremos en nivel de coherencia de Hola y el diseño de almacenamiento sean óptimos de hello para el rendimiento. Esta es Hola lista de requisitos de red para nuestro clúster hipotético:

* Los sistemas externos no tienen acceso a la base de datos Cassandra desde dentro o fuera de Azure
* Clúster de Casandra tiene toobe detrás de un equilibrador de carga para el tráfico de thrift
* Implemente nodos de Cassandra en dos grupos en cada centro de datos para una disponibilidad mejorada
* Bloquear clúster Hola así solo el conjunto de servidores de aplicación tiene base de datos de access toohello directamente
* Ningún extremo de red pública distinto a SSH
* Cada nodo de Cassandra necesita una dirección IP interna fija

Casandra puede ser implementado tooa sola región de Azure o las regiones de toomultiple según su naturaleza distribuida de Hola de carga de trabajo de Hola. Modelo de implementación de varias regiones puede ser aprovechado tooserve a los usuarios finales más cerca de tooa determinado geography a través de hello misma infraestructura de Casandra. La replicación se encarga de Casandra nodo integrado de sincronización de Hola de varios maestros escribe procedentes de varios centros de datos y presenta una vista coherente de hello tooapplications de datos. Implementación de varias regiones también puede ayudar con la mitigación de riesgos de Hola Hola más amplio Azure interrupción del servicio. La coherencia ajustable de Cassandra y la topología de la replicación le ayudará a satisfacer distintas necesidades RPO de aplicaciones.

### <a name="single-region-deployment"></a>Implementación de una sola región
Empezaremos con una implementación única región y cosecha Hola basándonos en la creación de un modelo de varias regiones. Red virtual de Azure será usado toocreate aislada subredes para que se puedan cumplir requisitos de seguridad de red de hello mencionados anteriormente.  proceso de Hello descrito en la creación de la implementación de una única región hello usa Ubuntu 14.04 LTS y Casandra 2.08; Sin embargo, el proceso de hello puede fácilmente ser toohello adoptado otras variantes de Linux. siguiente Hola es algunas características sistémicas de Hola de implementación en una sola región Hola.  

**Alta disponibilidad:** Hola nodos Casandra se muestra en la figura 1 se implementan de Hola tootwo disponibilidad se establece para que los nodos de hello están repartidos entre varios dominios de error para lograr alta disponibilidad. Máquinas virtuales que se anota con cada conjunto de disponibilidad es too2 asignado los dominios de error.  Microsoft Azure usa Hola concepto de toomanage de dominio de error no planeada hacia abajo de tiempo (por ejemplo, los errores de hardware o software) al concepto de Hola de dominio de actualización (por ejemplo, host o invitado aplicación de revisiones y actualizaciones de sistema operativo, las actualizaciones de aplicaciones) se utiliza para administrar programado tiempo de inactividad. Vea [recuperación ante desastres y alta disponibilidad para aplicaciones de Azure](http://msdn.microsoft.com/library/dn251004.aspx) para rol de Hola de dominios de error y de actualización para alcanzar la alta disponibilidad.

![Implementación de una sola región](./media/cassandra-nodejs/cassandra-linux1.png)

Ilustración 1: Implementación de una sola región

Tenga en cuenta que en tiempo de Hola de redactar este artículo, Azure no permite una asignación explícita de un grupo de dominio de error concreto de máquinas virtuales tooa; Hola por lo tanto, incluso con el modelo de implementación de Hola que se muestra en la figura 1, es estadísticamente probable que todas las máquinas virtuales de hello puede ser tootwo asignado los dominios de error en lugar de cuatro.

**Tráfico de Thrift de equilibrio de carga:** bibliotecas de cliente de Thrift dentro de hello web server conectan el clúster de toohello a través de un equilibrador de carga interno. Esto requiere el proceso de Hola de Agregar subred de datos"toohello de equilibrador de carga interno de saludo" (consulte la figura 1) en el contexto de hello del servicio de nube de hello hospeda hello Casandra clúster. Una vez definido el equilibrador de carga interno de hello, cada nodo requiere toobe de extremo con equilibrio de carga de hello agregado con anotaciones de Hola de un conjunto de carga equilibrada con los nombre del equilibrador de carga definidos. Consulte [Equilibrio de carga interno de Azure ](../../../load-balancer/load-balancer-internal-overview.md)para obtener más detalles.

**Valores de inicialización de clúster:** es importante tooselect Hola nodos de alta disponibilidad de la mayoría de valores de inicialización como Hola nuevos nodos se comunicarán con topología de Hola de toodiscover inicialización nodos de clúster de Hola. Un nodo de cada conjunto de disponibilidad se designa como valor de inicialización nodos tooavoid punto de error único.

**Factor de replicación y el nivel de coherencia:** compilación de alta disponibilidad y datos durabilidad de Casandra se caracteriza por hello Factor de replicación (RF - número de copias de cada fila almacenada en el clúster de hello) y el nivel de coherencia (número de réplicas toobe leídos/escritos antes de devolver el autor de llamada de hello resultado toohello). Factor de replicación se especifica durante Hola creación KEYSPACE (base de datos relacional de similar tooa), mientras que se especifica el nivel de coherencia de hello al emitir consultas CRUD Hola. Consulte la documentación de Casandra en [configurar para mantener la coherencia](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obtener detalles de la coherencia y fórmula hello para el cálculo de quórum.

Casandra admite dos tipos de modelos de integridad de datos: coherencia y coherencia definitiva; Hola Factor de replicación y el nivel de coherencia juntos determinará si los datos de hello serán coherentes tan pronto como se ha completado una operación de escritura o será coherente. Por ejemplo, especificar QUÓRUM ya Hola que usarán el nivel de coherencia garantiza datos coherencia durante cualquier nivel de coherencia, debajo de número de Hola de toobe de réplicas que se escribe como sea necesario tooattain resultados QUÓRUM (por ejemplo, uno) de datos es coherente.

clúster de 8 nodos de Hello mostrado anteriormente, con un factor de replicación de QUÓRUM y 3 (2 nodos se leen o escritos por motivos de coherencia) nivel de coherencia de lectura/escritura, puede sobrevivir a la pérdida teórico de Hola de en hello mayoría 1 nodo por replicación grupo antes de iniciar la aplicación hello teniendo en cuenta el error de Hola. Se supone que todos los espacios de clave de hello también han equilibra las solicitudes de lectura/escritura.  siguiente Hola es parámetros de Hola que se usará para el clúster de hello implementado:

Configuración de clúster de Cassandra de una sola región:

| Parámetro de clúster | Valor | Comentarios |
| --- | --- | --- |
| Número de nodos (N) |8 |Número total de nodos de clúster de Hola |
| Factor de replicación (RF) |3 |Número de réplicas de una fila determinada |
| Nivel de coherencia (escritura) |QUORUM[(RF/2) +1) = 2] Hola result de hello fórmula se redondea hacia abajo |Escribe en hello mayoría 2 réplicas antes de enviar respuesta hello toohello llamador; réplica 3rd se escribe de forma coherente. |
| Nivel de coherencia (lectura) |QUÓRUM [(RF/2) + 1 = 2] se redondea el resultado de hello de fórmula de Hola |Lee 2 réplicas antes de enviar el autor de llamada de respuesta toohello. |
| Estrategia de replicación |NetworkTopologyStrategy vea la [replicación de datos](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) en la documentación de Cassandra para obtener más información |Entiende la topología de implementación de Hola y coloca las réplicas en los nodos para que todas las réplicas de hello no terminan en hello mismo bastidor |
| Snitch |GossipingPropertyFileSnitch. Vea [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) en la documentación de Cassandra para más información |NetworkTopologyStrategy utiliza un concepto de topología de snitch toounderstand Hola. GossipingPropertyFileSnitch ofrece un mejor control de asignación de cada centro de toodata de nodo y bastidor. clúster de Hello, a continuación, usa cotilleos toopropagate esta información. Esto es mucho más fácil en tooPropertyFileSnitch relativa de configuración de IP dinámica |

**Consideraciones de Azure para el clúster de Cassandra**: La funcionalidad Microsoft Azure Virtual Machines usa Azure Blob Storage para la persistencia de disco; Azure Storage guarda tres réplicas de cada disco que proporcionan gran durabilidad. Esto significa que cada fila de datos insertados en una tabla de Casandra ya está almacenada en 3 réplicas y, por tanto, coherencia de los datos es ya controlada aunque Hola Factor de replicación (RF) es 1. Hola principal problema con el Factor de replicación que se va a 1 es aplicación hello experimentarán tiempo de inactividad incluso si se produce un error en un único nodo Casandra. Sin embargo, si un nodo está inactivo para problemas de hello (p. ej., hardware, errores de software del sistema) reconocidos por el controlador de tejido de Azure, proporcionará un nuevo nodo en su lugar con hello las mismas unidades de almacenamiento. Aprovisionamiento de un nuevo nodo tooreplace Hola antiguo uno puede tardar unos minutos.  De forma similar para las actividades de mantenimiento planificado como los cambios del sistema operativo invitado, Casandra actualiza y cambios en la aplicación controlador de tejido de Azure lleva a cabo actualizaciones sucesivas de nodos de hello en clúster de Hola.  Actualizaciones sucesivas también pueden dar de baja varios nodos a la vez y, por tanto, clúster de hello puede experimentar breve período de inactividad para algunas particiones. Sin embargo, no se perderán debido redundancia de almacenamiento de Azure integrada toohello Hola datos.  

Para los sistemas implementaron tooAzure que no necesita una alta disponibilidad (por ejemplo, 99,9 aproximadamente que es equivalente too8.76 horas/año; vea [alta disponibilidad](http://en.wikipedia.org/wiki/High_availability) para obtener más información) puede ser capaz de toorun con RF = 1 y nivel de coherencia = uno.  Para las aplicaciones con requisitos de alta disponibilidad, RF = 3 y el nivel de coherencia = QUÓRUM tolerarán Hola tiempo de inactividad de uno de hello nodos de réplicas de Hola. RF = 1 en las implementaciones tradicionales (por ejemplo, local) no se puede usar debido toohello posible pérdida de datos resultantes de los problemas como errores de disco.   

## <a name="multi-region-deployment"></a>Implementación en varias regiones
Replicación center-orientadas a datos y el modelo de coherencia se ha descrito anteriormente ayuda con la implementación de varias regiones de hello fuera del cuadro de hello sin Hola de Casandra necesitan para las herramientas externas. Esto es bastante diferente de bases de datos relacionales Hola tradicional donde el programa de instalación de hello para la creación de reflejo de base de datos de varios maestros escribe puede ser bastante compleja. Puede ayudar Casandra en una región múltiples configurar con escenarios de uso de hello incluidos Hola siguientes:

**Implementación basada en proximidad:** aplicaciones de varios inquilinos, con borrar la asignación de usuarios del inquilino-a-región, se puede beneficiado por las latencias baja del clúster de hello varias regiones. Por ejemplo un aprendizaje de administración de sistemas para instituciones educativas pueden implementar un clúster distribuido en UU y oeste de Estados Unidos regiones tooserve Hola respectivo campus para transaccional, así como análisis. datos de Hello puede estar localmente coherentes en hello tiempo lecturas y escrituras y pueden ser coherentes entre ambas regiones Hola. Hay otros ejemplos como la distribución de medios, el comercio electrónico y todo lo que sirva a una base de usuario concentrada geográficamente es un buen caso de uso para este modelo de implementación.

**Alta disponibilidad:** La redundancia es un factor clave para lograr una alta disponibilidad de software y hardware; consulte Creación de sistemas en nube confiables en Microsoft Azure para obtener más información. En Microsoft Azure, Hola única manera confiable de lograr redundancia true es mediante la implementación de un clúster de varias regiones. Las aplicaciones pueden implementarse en un modo activo / activo o activo / pasivo y si una de las regiones de hello está inactivo, Azure Traffic Manager puede redirigir la región activa de tráfico toohello.  Con la implementación de una única región hello, si la disponibilidad de hello es 99,9, una implementación en una región de dos puede alcanzar una disponibilidad de 99,9999 calculada mediante la fórmula de hello: (1-(1-0.999) * (1-0,999)) * 100); vea Hola anteriormente para obtener más información.

**Recuperación ante desastres:** El clúster de Cassandra de varias regiones, si está correctamente diseñado, puede resistir interrupciones del centro de datos por catástrofes. Si una región está inactivo, pueden iniciar Hola aplicación implementada tooother regiones que atienden a los usuarios finales de Hola. Al igual que cualquier otra implementación de continuidad empresarial, aplicación hello tiene toobe tolerante a errores de pérdida de datos resultantes de los datos de hello en canalización asincrónica Hola. Sin embargo, Casandra hace recuperación hello swifter mucho más tiempo del Hola realizada por los procesos de recuperación de base de datos tradicional. Figura 2 muestra el modelo de implementación típica de varias regiones de hello con ocho nodos en cada región. Ambas regiones son imágenes reflejadas entre sí para hello mismo de simetría; diseños de mundo real dependen del tipo de carga de trabajo de hello (p. ej., transaccional o analítico), RPO, RTO, coherencia de los datos y requisitos de disponibilidad.

![Implementación de varias regiones](./media/cassandra-nodejs/cassandra-linux2.png)

Ilustración 2: Implementación de Cassandra en varias regiones

### <a name="network-integration"></a>Integración de red
Conjuntos de máquinas virtuales de redes de implementada tooprivate ubicadas en dos regiones se comunica entre sí mediante un túnel VPN. túnel VPN de Hello conecta dos puertas de enlace de software aprovisionados durante el proceso de implementación de red de Hola. Ambas regiones tienen una arquitectura de red similar en cuanto a subredes "web" y "datos"; Las redes de Azure permite la creación de hello de subredes tantos según sea necesario y aplique las ACL según sea necesario por la seguridad de red. Al diseñar la topología de clúster de hello entre datos center comunicación hello y latencia impacto económico de tráfico de red de hello necesidad toobe considerada.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Coherencia de los datos para la implementación de varios centros de datos
Distribuye las implementaciones necesidad toobe tenga en cuenta el impacto de topología de clúster de hello en rendimiento y alta disponibilidad. Hola RF y nivel de coherencia toobe necesidad seleccionado de modo que Hola quórum no depende de disponibilidad de Hola de todos los centros de datos de Hola.
Para un sistema que necesita consistencia alta, un LOCAL_QUORUM de nivel de coherencia (para las lecturas y escrituras) asegurará que Hola local lee y escribe se satisface desde Hola local nodos mientras los datos están replican de forma asincrónica toohello centros de datos remotos.  Tabla 2 se resume la configuración Hola detalles de clúster de varias regiones de Hola que se describen más adelante en hello escribir una.

**Configuración del clúster de Cassandra de dos regiones**

| Parámetro de clúster | Valor | Comentarios |
| --- | --- | --- |
| Número de nodos (N) |8 + 8 |Número total de nodos de clúster de Hola |
| Factor de replicación (RF) |3 |Número de réplicas de una fila determinada |
| Nivel de coherencia (escritura) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] resultado de hello de fórmula de saludo se redondea hacia abajo |2 nodos se escribirán toohello primer centro de datos de forma sincrónica; Hola 2 nodos adicionales necesarios para el quórum se escribirán asincrónicamente toohello 2nd centro de datos. |
| Nivel de coherencia (lectura) |LOCAL_QUORUM ((RF/2) + 1) = 2 resultado de hello de fórmula de saludo se redondea hacia abajo |Las solicitudes de lectura se satisfacen desde sólo una región; 2 nodos se leen antes de respuesta de hello enviar a atrás toohello cliente. |
| Estrategia de replicación |NetworkTopologyStrategy vea la [replicación de datos](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) en la documentación de Cassandra para obtener más información |Entiende la topología de implementación de Hola y coloca las réplicas en los nodos para que todas las réplicas de hello no terminan en hello mismo bastidor |
| Snitch |GossipingPropertyFileSnitch. Vea [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) en la documentación de Cassandra para más información |NetworkTopologyStrategy utiliza un concepto de topología de snitch toounderstand Hola. GossipingPropertyFileSnitch ofrece un mejor control de asignación de cada centro de toodata de nodo y bastidor. clúster de Hello, a continuación, usa cotilleos toopropagate esta información. Esto es mucho más fácil en tooPropertyFileSnitch relativa de configuración de IP dinámica |

## <a name="hello-software-configuration"></a>Hola una configuración de SOFTWARE
Hola después de las versiones de software se utiliza durante la implementación de hello:

<table>
<tr><th>Software</th><th>Origen</th><th>Versión</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Puesto que la descarga de JRE requiere manual aceptación de licencia de Oracle, implementación de hello toosimplify, descarga que todas Hola escritorio toohello de software necesarias para cargar más adelante en la imagen de la plantilla de Ubuntu Hola que se crearán como un clúster de toohello precursor implementación.

Descargue Hola por encima de software en un directorio de descarga conocido (por ejemplo, %TEMP%/downloads en Windows o ~/Downloads en la mayoría de las distribuciones de Linux o Mac) en el equipo local de Hola.

### <a name="create-ubuntu-vm"></a>CREAR LA MÁQUINA VIRTUAL DE UBUNTU
En este paso del proceso de Hola crearemos Ubuntu imagen con software de requisito previo de Hola para que hello imagen se puede reutilizar para el aprovisionamiento de varios nodos de Casandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>PASO 1: Generación de par de claves de SSH
Azure necesita una clave pública PEM o DER codificado a Hola tiempo de aprovisionamiento de X509. Generar un par de claves pública/privada mediante instrucciones de hello ubicadas en cómo tooUse SSH con Linux en Azure. Si tiene previsto toouse putty.exe como un cliente de SSH en Windows o Linux, tendrá que tooconvert Hola PEM codificado formato de tooPPK clave privada RSA con puttygen.exe; instrucciones de Hola para esto pueden encontrarse en hello por encima de la página web.

#### <a name="step-2-create-ubuntu-template-vm"></a>PASO 2: Creación de la máquina virtual de la plantilla de Ubuntu
plantilla de hello toocreate máquina virtual, inicie sesión en hello Azure Hola de portal y el uso clásico sigue secuencia: haga clic en nuevo, proceso, máquina VIRTUAL, de la galería, UBUNTU, Ubuntu Server 14.04 LTS y, a continuación, haga clic en la flecha derecha Hola. Para obtener un tutorial que describe cómo toocreate una VM de Linux, consulte Crear una máquina Virtual ejecuta Linux.

Escriba Hola siga la información en pantalla de "configuración de máquina Virtual" hello #1:

<table>
<tr><th>NOMBRE DEL CAMPO              </td><td>       VALOR DEL CAMPO               </td><td>         COMENTARIOS                </td><tr>
<tr><td>FECHA DE LANZAMIENTO DE LA VERSIÓN    </td><td> Seleccione una fecha en la lista desplegable de Hola</td><td></td><tr>
<tr><td>NOMBRE DE MÁQUINA VIRTUAL    </td><td> cass-template                   </td><td> Este es el nombre de host de Hola de hello VM </td><tr>
<tr><td>NIVEL                     </td><td> ESTÁNDAR                           </td><td> Deje Hola predeterminado              </td><tr>
<tr><td>TAMAÑO                     </td><td> A1                              </td><td>Seleccione Hola que VM en función de hello E/S necesita; para este propósito deje el valor predeterminado de Hola </td><tr>
<tr><td> NOMBRE DE USUARIO NUEVO             </td><td> localadmin                       </td><td> "admin" es un nombre de usuario reservado en Ubuntu 12.xx y versiones posteriores</td><tr>
<tr><td> AUTENTICACIÓN         </td><td> Haga clic en la casilla                 </td><td>Actívelo si desea toosecure con una clave SSH </td><tr>
<tr><td> CERTIFICADO             </td><td> nombre de archivo del certificado de clave pública de Hola </td><td> Usar Hola clave pública generado anteriormente</td><tr>
<tr><td> New Password    </td><td> contraseña segura </td><td> </td><tr>
<tr><td> Confirm Password    </td><td> contraseña segura </td><td></td><tr>
</table>

Escriba Hola siga la información en pantalla de "configuración de máquina Virtual" hello #2:

<table>
<tr><th>NOMBRE DEL CAMPO             </th><th> VALOR DEL CAMPO                       </th><th> COMENTARIOS                                 </th></tr>
<tr><td> SERVICIO EN LA NUBE    </td><td> Crear un nuevo servicio en la nube    </td><td>El servicio de nube es un recurso de proceso de contenedor como máquinas virtuales</td></tr>
<tr><td> NOMBRE DE DNS DEL SERVICIO EN LA NUBE    </td><td>ubuntu-template.cloudapp.net    </td><td>Defina un nombre de equilibrador de carga independiente de la máquina</td></tr>
<tr><td> REGION/GRUPO DE AFINIDAD/RED VIRTUAL </td><td>    Oeste de EE. UU.    </td><td> Seleccione una región desde la que las aplicaciones web acceso clúster de hello Casandra</td></tr>
<tr><td>STORAGE ACCOUNT </td><td>    Use el valor predeterminado    </td><td>Usar cuenta de almacenamiento predeterminada de Hola o una cuenta de almacenamiento creada previamente en una región determinada</td></tr>
<tr><td>El conjunto de disponibilidad </td><td>    None </td><td>    Deje este parámetro en blanco</td></tr>
<tr><td>EXTREMOS    </td><td>Use el valor predeterminado </td><td>    Utilizar la configuración de SSH de hello predeterminada </td></tr>
</table>

Haga clic en la flecha derecha, deje los valores predeterminados de hello en pantalla de bienvenida #3 y haga clic en hello "comprobación" botón toocomplete Hola VM proceso de aprovisionamiento. Después de unos minutos, Hola VM con hello nombre "ubuntu-template" debe estar en un estado "en ejecución".

### <a name="install-hello-necessary-software"></a>INSTALAR el SOFTWARE necesario de Hola
#### <a name="step-1-upload-tarballs"></a>PASO 1: Carga de tarballs
Uso de scp o pscp, Hola copia descargaron software demasiado ~ / directorio de descargas con hello siguiendo el formato de comando:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Repita Hola por encima de comando para JRE, así como para los bits de Casandra Hola.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>PASO 2: Preparar la estructura de directorios de Hola y extraer archivos Hola
Inicie sesión en hello VM y crear la estructura de directorios de Hola y extraer software como un superusuario mediante Hola intensiva de script siguiente:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Si pega este script en la ventana de vim, asegúrese de carro de hello tooremove seguro de valor devuelto ('\r ") con el siguiente comando de hello:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Paso 3: Edición de perfil/etc.
Anexar siguiente Hola final hello:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Paso 4: Instalación de JNA para sistemas de producción
Secuencia de comandos siguiente Hola de uso: siguiente Hola comando install jna-3.2.7.jar y 3.2.7.jar de plataforma de jna too/usr/share.java directory sudo apt-get instalará libjna java

Cree vínculos simbólicos en el directorio de $CASS_HOME/lib para que el script de inicio de Cassandra pueda encontrar estos JAR:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Paso 5: Configuración de cassandra.yaml
Editar cassandra.yaml en cada configuración de tooreflect de máquina virtual necesaria para todas las máquinas virtuales de hello [se se Retocar durante el aprovisionamiento real de hello]:

<table>
<tr><th>Nombre del campo   </th><th> Valor  </th><th>    Comentarios </th></tr>
<tr><td>cluster_name </td><td>    "CustomerService"    </td><td> Usar el nombre de Hola que refleja la implementación</td></tr>
<tr><td>listen_address    </td><td>[deje este parámetro en blanco]    </td><td> Elimine "localhost" </td></tr>
<tr><td>rpc_addres   </td><td>[deje este parámetro en blanco]    </td><td> Elimine "localhost" </td></tr>
<tr><td>seeds    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Lista de todas las direcciones IP de Hola que están designados como valores de inicialización.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Se utiliza por hello NetworkTopologyStrateg deducir Hola centro de datos y bastidor Hola de hello VM</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Paso 6: Capturar imagen de máquina virtual de Hola
Inicie sesión en la máquina virtual de hello mediante Hola hostname (hk-CA-template.cloudapp.net) y clave privada de hello SSH creado anteriormente. Vea cómo tooUse SSH con Linux en Azure para detalles sobre cómo toolog en uso Hola comando ssh o putty.exe.

Ejecute hello sigue la secuencia de imagen de hello toocapture de acciones:

##### <a name="1-deprovision"></a>1. Desaprovisionamiento
Use el comando de Hola "sudo waagent – desaprovisionamiento + user" tooremove información específica de la instancia de máquina Virtual. Puede encontrar [cómo tooCapture una máquina Virtual Linux](capture-image.md) tooUse como una plantilla ofrecen más detalles en el proceso de captura de imagen de Hola.

##### <a name="2-shutdown-hello-vm"></a>2: Hola apagar VM
Asegúrese de que la máquina virtual Hola se resalta y haga clic en el vínculo de cierre de Hola de barra de comandos de hello inferior.

##### <a name="3-capture-hello-image"></a>3: captura de imagen de Hola
Asegúrese de que la máquina virtual Hola se resalta y haga clic en el vínculo de captura de Hola de barra de comandos de hello inferior. En la siguiente pantalla de bienvenida, asigne un nombre de imagen (por ejemplo, hk-cas-2-08-ub-14-04-2014071), caso descripción de la imagen y haga clic en proceso de captura de Hola "comprobación" marca toofinish Hola.

Este proceso tardará unos segundos e imagen Hola debe estar disponible en la sección Mis imágenes de galería de imágenes de Hola. una VM de origen Hola se eliminarán automáticamente tras captura imagen de Hola correctamente. 

## <a name="single-region-deployment-process"></a>Proceso de implementación en una sola región
**Paso 1: Crear red Virtual de hello** sesión en hello portal de Azure y crear una red virtual (clásica) con atributos de Hola se muestra en hello en la tabla siguiente. Vea [crear una red virtual (clásica) mediante el portal de Azure de hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) para obtener pasos detallados del proceso de Hola.      

<table>
<tr><th>Nombre del atributo de VM</th><th>Valor</th><th>Comentarios</th></tr>
<tr><td>Nombre</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>Region</td><td>Oeste de EE. UU.</td><td></td></tr>
<tr><td>Servidores DNS</td><td>None</td><td>Ignore esto, ya que no estamos usando un servidor DNS</td></tr>
<tr><td>Espacio de direcciones</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>IP inicial:</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Agregue Hola siguientes:

<table>
<tr><th>Nombre</th><th>IP inicial:</th><th>CIDR</th><th>Comentarios</th></tr>
<tr><td>web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Subred para la granja de servidores de hello web</td></tr>
<tr><td>data</td><td>10.1.2.0</td><td>/24 (251)</td><td>Subred para los nodos de la base de datos de Hola</td></tr>
</table>

Subredes de Web y los datos se pueden proteger a través de grupos de seguridad de red cobertura Hola de los cuales está fuera del ámbito de este artículo.  

**Paso 2: Aprovisionar máquinas de virtuales** con imagen Hola creado anteriormente, crearemos Hola después de máquinas virtuales en la nube de hello server "hk-c-svc-west" y enlazarlas toohello respectivas subredes tal y como se muestra a continuación:

<table>
<tr><th>Nombre de máquina    </th><th>Subred    </th><th>Dirección IP    </th><th>El conjunto de disponibilidad</th><th>Controlador de dominio/bastidor</th><th>¿Valor de inicialización?</th></tr>
<tr><td>hk-c1-west-us    </td><td>data    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1 </td><td>Sí</td></tr>
<tr><td>hk-c2-west-us    </td><td>data    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1    </td><td>No </td></tr>
<tr><td>hk-c3-west-us    </td><td>data    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Sí</td></tr>
<tr><td>hk-c4-west-us    </td><td>data    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>No </td></tr>
<tr><td>hk-c5-west-us    </td><td>data    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Sí</td></tr>
<tr><td>hk-c6-west-us    </td><td>data    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>No </td></tr>
<tr><td>hk-c7-west-us    </td><td>data    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Sí</td></tr>
<tr><td>hk-c8-west-us    </td><td>data    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>No </td></tr>
<tr><td>hk-w1-west-us    </td><td>web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
<tr><td>hk-w2-west-us    </td><td>web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
</table>

Creación de hello por encima de la lista de máquinas virtuales requiere Hola siguiendo el proceso:

1. Crear un servicio de nube vacía en una región determinada
2. Crear una máquina virtual de hello capturados anteriormente imagen y adjuntarlo toohello red virtual creado anteriormente; Repita este paso para todas las máquinas virtuales de Hola
3. Agregar un servicio de nube toohello del equilibrador de carga interno y adjuntarlo subred toohello "datos"
4. Para cada máquina virtual creado anteriormente, agregue un extremo con equilibrio de carga para tráfico de thrift a través de un equilibrador de carga interno de carga equilibrada conjunto conectado toohello creado anteriormente

Hola por encima de proceso se puede ejecutar con el portal de Azure clásico; usar una máquina de Windows (utilice una máquina virtual de Azure si no dispone de máquina de Windows tooa de acceso), usar hello después tooprovision de secuencia de comandos de PowerShell todas las máquinas 8 virtuales automáticamente.

**Lista 1: script de PowerShell para el aprovisionamiento de máquinas virtuales**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Paso 3: Configuración de Cassandra en cada máquina virtual**

Inicie sesión en hello VM y realizar Hola siguientes:

* Editar $CASS_HOME/conf/cassandra-rackdc.properties toospecify Hola center y el bastidor de propiedades de datos:
  
       dc =EASTUS, rack =rack1
* Editar nodos de valor de inicialización de cassandra.yaml tooconfigure como sigue:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Paso 4: Iniciar las máquinas virtuales de Hola y probar Hola del clúster**

Inicie sesión en uno de los nodos de hello (p. ej. hk-c1-oeste-us) y ejecución Hola siguiendo el estado del comando toosee Hola de clúster de hello:

       nodetool –h 10.1.2.4 –p 7199 status

Debería ver Hola presentación similar toohello uno por debajo de un clúster de 8 nodos:

<table>
<tr><th>Estado</th><th>Dirección    </th><th>Carga    </th><th>Tokens    </th><th>Propiedad </th><th>Identificador de host    </th><th>Bastidor</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87,81 KB    </td><td>256    </td><td>38,0 %    </td><td>GUID (eliminado)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41,08 KB    </td><td>256    </td><td>68,9 %    </td><td>GUID (eliminado)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55,29 KB    </td><td>256    </td><td>68,8 %    </td><td>GUID (eliminado)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55,29 KB    </td><td>256    </td><td>68,8 %    </td><td>GUID (eliminado)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55,29 KB    </td><td>256    </td><td>68,8 %    </td><td>GUID (eliminado)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55,29 KB    </td><td>256    </td><td>68,8 %    </td><td>GUID (eliminado)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55,29 KB    </td><td>256    </td><td>68,8 %    </td><td>GUID (eliminado)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55,29 KB    </td><td>256    </td><td>68,8 %    </td><td>GUID (eliminado)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Hola de prueba único clúster de región
Usar hello después de clúster de hello tootest de pasos:

1. Mediante el commandlet de Get-AzureInternalLoadbalancer de comandos de Powershell de hello, obtener dirección IP de hello del equilibrador de carga interno de hello (p. ej.  10.1.2.101). a continuación se muestran la sintaxis de Hello del comando de hello: Get-AzureLoadbalancer – ServiceName "hk-c-svc-oeste-us" [muestra los detalles de Hola de equilibrador de carga interno de hello junto con su dirección IP]
2. Inicie sesión en la granja de servidores web de hello VM (p. ej. hk-w1-oeste-us) mediante Putty o ssh
3. Ejecute $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Usar hello después CQL comandos tooverify si Hola clúster funciona:
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');
   
     SELECT * FROM Customers;

Debería ver una presentación como Hola a continuación:

<table>
  <tr><th> customer_id </th><th> firstname </th><th> Lastname </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Julia </td><td> Doe </td></tr>
</table>

Tenga en cuenta que keyspace Hola creado en el paso 4 utiliza SimpleStrategy con un replication_factor de 3. SimpleStrategy se recomienda para las implementaciones de un solo centro de datos, mientras que NetworkTopologyStrategy para implementaciones de varios centros de datos. Un replication_factor de 3 proporcionará tolerancia a errores de nodo.

## <a id="tworegion"></a>Proceso de implementación de varias regiones
Se aprovechan la implementación en una única región Hola completado y repita Hola mismo proceso para la instalación de la segunda región de Hola. Hola principal diferencia entre hello único y varios implementación en una región es configuración de túnel VPN de hello para la comunicación entre región; comenzar con la instalación de red de hello, aprovisionar máquinas virtuales de Hola y configurar a Casandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Paso 1: Crear red Virtual de hello en hello 2nd región
Inicie sesión en el portal de Azure clásico de Hola y crear una red Virtual con el programa de atributos de hello en la tabla de Hola. Vea [configurar una red Virtual solo en el portal de Azure clásico hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) para obtener pasos detallados del proceso de Hola.      

<table>
<tr><th>Nombre del atributo    </th><th>Valor    </th><th>Comentarios</th></tr>
<tr><td>Nombre    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>Region    </td><td>Este de EE. UU.</td><td></td></tr>
<tr><td>Servidores DNS        </td><td></td><td>Ignore esto, ya que no estamos usando un servidor DNS</td></tr>
<tr><td>Configurar una VPN de punto a sitio</td><td></td><td>        Ignore esto</td></tr>
<tr><td>Configurar una VPN de sitio a sitio</td><td></td><td>        Ignore esto</td></tr>
<tr><td>Espacio de direcciones    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>IP inicial:    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Agregue Hola siguientes:

<table>
<tr><th>Nombre    </th><th>IP inicial:    </th><th>CIDR    </th><th>Comentarios</th></tr>
<tr><td>web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Subred para la granja de servidores de hello web</td></tr>
<tr><td>data    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Subred para los nodos de la base de datos de Hola</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Paso 2: Creación de redes locales
Una red Local en la red virtual de Azure es un espacio de direcciones de proxy que se asigna el sitio remoto tooa como una nube privada u otra región de Azure. Este espacio de direcciones de proxy es tooa enlazado puerta de enlace remota para enrutamiento de red de toohello derecha destinos de red. Vea [configurar una conexión de red virtual tooVNet](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) para obtener instrucciones acerca de cómo establecer la conexión de red virtual a red virtual Hola.

Cree dos redes locales por hello detalles siguientes:

| Nombre de red | Dirección de puerta de enlace VPN | Espacio de direcciones | Comentarios |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |Durante la creación de hello red Local proporcionan un marcador de posición de la dirección de puerta de enlace. dirección de puerta de enlace real de Hola se rellena una vez creada la puerta de enlace de Hola. Libere espacio de dirección de hello seguro coincide exactamente con Hola respectivo red virtual remota; en este caso hello red virtual creados en hello región Este de EE.. |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |Durante la creación de hello red Local proporcionan un marcador de posición de la dirección de puerta de enlace. dirección de puerta de enlace real de Hola se rellena una vez creada la puerta de enlace de Hola. Libere espacio de dirección de hello seguro coincide exactamente con Hola respectivo red virtual remota; en este caso hello red virtual creados en hello región Oeste de Estados Unidos. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Paso 3: Mapa "red"Local"toohello respectivas redes virtuales
De hello portal de Azure clásico, seleccione cada red virtual, haga clic en "Configurar", compruebe "Conectar toohello red local" y seleccione Hola redes locales por hello detalles siguientes:

| Virtual Network | Red local |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Paso 4: Creación de puertas de enlace en VNET1 y VNET2
En el panel de Hola de ambas redes virtuales hello, haga clic en crear puerta de enlace que se desencadenará el proceso de aprovisionamiento de puerta de enlace VPN Hola. Después de unos minutos Hola panel de cada red virtual debe mostrar la dirección de puerta de enlace real de Hola.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Paso 5: Actualización "Local" las redes con direcciones de respectivos "Gateway" hello
Editar ambos Hola redes locales tooreplace Hola marcador de posición puerta de enlace IP dirección con la dirección IP real de Hola de hello simplemente aprovisionado puertas de enlace. Usar hello después de asignación:

<table>
<tr><th>Red local    </th><th>Puerta de enlace de red virtual</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>Puerta de enlace de hk-vnet-west-us</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>Puerta de enlace de hk-vnet-east-us</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Paso 6: Actualizar la clave compartida de Hola
Hola de uso después de la clave IPSec Hola de tooupdate de script de Powershell de cada puerta de enlace VPN [usar Hola simplificar clave para las puertas de enlace de hello]: hk-lnet-map-to-west-us - LocalNetworkSiteName de Set-AzureVNetGatewayKey - VNetName hk-red virtual-este-us - SharedKey D9E76BKK Set-AzureVNetGatewayKey VNetName - hk-red virtual-oeste-us - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Paso 7: Establecer la conexión de red virtual a red virtual de Hola
En hello portal de Azure clásico, use el menú de "Panel" de Hola de ambos conexión de puerta de enlace a puerta de enlace hello tooestablish de redes virtuales. Usar elementos de menú de Hola "Conectar" en la barra de herramientas de hello inferior. Después de unos minutos panel Hola debe mostrar detalles de la conexión de hello gráficamente.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Paso 8: Crear máquinas virtuales de hello en la región #2
Crear imagen de Ubuntu Hola según se describió en la implementación de una región #1 siguiente Hola mismo pasos o copiar Hola imagen VHD toohello almacenamiento de Azure cuenta archivos ubicado en la región #2 y crear imagen de Hola. Use esta imagen y crear Hola siguiendo la lista de máquinas virtuales en un nuevo servicio de nube hk-c-svc-este-us:

| Nombre de máquina | Subred | Dirección IP | El conjunto de disponibilidad | Controlador de dominio/bastidor | ¿Valor de inicialización? |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |data |10.2.2.4 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Sí |
| hk-c2-east-us |data |10.2.2.5 |hk-c-aset-1 |dc =EASTUS rack =rack1 |No |
| hk-c3-east-us |data |10.2.2.6 |hk-c-aset-1 |dc =EASTUS rack =rack2 |Sí |
| hk-c5-east-us |data |10.2.2.8 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Sí |
| hk-c6-east-us |data |10.2.2.9 |hk-c-aset-2 |dc =EASTUS rack =rack3 |No |
| hk-c7-east-us |data |10.2.2.10 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Sí |
| hk-c8-east-us |data |10.2.2.11 |hk-c-aset-2 |dc =EASTUS rack =rack4 |No |
| hk-w1-east-us |web |10.2.1.4 |hk-w-aset-1 |N/D |N/D |
| hk-w2-east-us |web |10.2.1.5 |hk-w-aset-1 |N/D |N/D |

Seguimiento Hola mismo instrucciones como región #1 pero usan el espacio de direcciones de 10.2.xxx.xxx.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Paso 9: Configuración de Cassandra en cada máquina virtual
Inicie sesión en hello VM y realizar Hola siguientes:

1. Editar $CASS_HOME/conf/cassandra-rackdc.properties toospecify Hola center y el bastidor de propiedades de datos en formato de hello: dc = bastidor EASTUS = bastidor1
2. Editar los nodos de valor de inicialización de cassandra.yaml tooconfigure: inicializaciones: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>Paso 10: Inicio de Cassandra
Inicie sesión en cada máquina virtual e iniciar Casandra en segundo plano de Hola ejecutando el siguiente comando de hello: $CASS_HOME/bin/Casandra

## <a name="test-hello-multi-region-cluster"></a>Hola clúster consta de varias regiones de prueba
Por ahora Casandra ha sido implementado too16 nodos con 8 nodos en cada región de Azure. Estos nodos están en hello mismo clúster en virtud de nombre de clúster común de Hola y la configuración de nodos de valor de inicialización de Hola. Usar hello después de clúster de proceso tootest hello:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Paso 1: Obtener IP de equilibrador de carga interno de Hola para ambas regiones de hello mediante PowerShell
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-west-us"
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-east-us"  
  
    Tenga en cuenta las direcciones IP hello (por ejemplo, oeste - 10.1.2.101, este - 10.2.2.101) muestra.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Paso 2: Ejecutar siguiente hello en la región del Oeste Hola tras iniciar sesión en hk-w1-oeste-us
1. Ejecute $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Ejecute hello seguir CQL comandos:
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { 'class' : 'NetworkToplogyStrategy', 'WESTUS' : 3, 'EASTUS' : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Debería ver una presentación como Hola a continuación:

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Julia |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Paso 3: Ejecutar siguiente hello en la región Este de hello tras iniciar sesión en hk-w1-este-us:
1. Ejecute $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Ejecute hello seguir CQL comandos:
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Debería ver Hola mismo mostrar tal como se muestra para la región del Oeste hello:

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Julia |Doe |

Ejecutar unas inserciones más y vea que las que se pueden obtener replicada toowest-us parte del clúster de Hola.

## <a name="test-cassandra-cluster-from-nodejs"></a>Probar el clúster de Cassandra desde Node.js
Utilizando una de las máquinas virtuales de Linux de hello crearán previamente en el nivel de "web" Hola, ejecutamos una simples datos Hola insertada previamente de Node.js script tooread

**Paso 1: Instalación de Node.js y del cliente de Cassandra**

1. Instalar Node.js y NPM
2. Instalar el paquete de nodo "cassandra-client" con NPM
3. Ejecute hello siguiente secuencia de comandos en símbolo del sistema de hello shell que muestra la cadena de json de Hola de hello recuperar datos:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Conclusión
Microsoft Azure es una plataforma flexible que permite la ejecución de Hola de Microsoft así como software de código abierto como se muestra en este ejercicio. Clústeres de alta disponibilidad Casandra pueden implementarse en un solo centro de datos a través de hello repartir Hola nodos de clúster entre varios dominios de error. También se pueden implementar clústeres Cassandra en varias regiones de Azure geográficamente distantes para sistemas de prueba ante desastres. Azure y permite juntos Casandra Hola construcción de altamente escalable, de alta disponibilidad y servicios en la nube recuperable ante desastres necesitan por internet de hoy en día escalar los servicios.  

## <a name="references"></a>Referencias
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

