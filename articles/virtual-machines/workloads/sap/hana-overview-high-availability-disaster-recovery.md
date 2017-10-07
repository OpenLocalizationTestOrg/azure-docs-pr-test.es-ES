---
title: "aaaHigh disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias de gran tamaño) | Documentos de Microsoft"
description: "En este documento se explica cómo establecer una estrategia de alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>Alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes) 

Los conceptos de alta disponibilidad y recuperación ante desastres son aspectos importantes de la ejecución de servidores importantes de SAP HANA en Azure (instancias grandes). Es importante toowork con SAP, el integrador de sistema, o arquitecto de tooproperly de Microsoft e implemente Hola estrategia derecha alta-disponibilidad/recuperación ante desastres. También es objetivo de punto de recuperación de tooconsider importante hello y objetivo de tiempo de recuperación, que son específicos tooyour entorno.

## <a name="high-availability"></a>Alta disponibilidad

Microsoft es compatible con métodos de alta disponibilidad de SAP HANA "fuera del cuadro de hello," que se incluyen:

- **Replicación de almacenamiento:** Hola tooreplicate de capacidad del sistema de almacenamiento de todas las ubicaciones de tooanother de datos (dentro de, o de forma independiente, Hola mismo centro de datos). SAP HANA funciona de forma independiente con respecto a este método.
- **Replicación del sistema de archivos de HANA:** Hola replicación de todos los datos en el sistema SAP HANA tooa de SAP HANA independiente. objetivo de tiempo de recuperación de Hola se minimiza a través de la replicación de datos a intervalos regulares. SAP HANA admite modos de en memoria, sincrónicos o asincrónicos, sincrónicos (solo se recomienda para SAP HANA sistemas que están dentro de Hola mismo centro de datos o menor que 100 KM alejados). En el diseño actual de Hola de sellos HANA instancia grande, la replicación del sistema de archivos de HANA puede usarse para lograr alta disponibilidad.
- **Conmutación automática por error de host:** un toouse de solución de recuperación de errores local como una replicación toosystem alternativo. Cuando el nodo principal de hello deja de estar disponible, uno o más nodos de SAP HANA en espera están configurados en modo de escalado horizontal y SAP HANA conmuta por error automáticamente tooanother nodo.

Para obtener más información acerca de alta disponibilidad de SAP HANA, vea Hola siguiendo la información de SAP:

- [SAP HANA High-Availability Whitepaper](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html) (Documento técnico sobre la alta disponibilidad de SAP HANA)
- [SAP HANA Administration Guide](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf) (Guía de administración de SAP HANA)
- [Vídeo de SAP sobre la replicación del sistema de SAP HANA](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [Nota de soporte técnico de SAP 1999880: preguntas más frecuentes sobre la replicación del sistema de SAP HANA](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [Nota de soporte técnico de SAP 2165547: copia de seguridad y restauración de SAP HANA en el entorno de replicación del sistema de SAP HANA](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [Nota de soporte técnico de SAP 1984882: uso de la replicación del sistema de SAP HANA para el cambio de hardware con el tiempo de inactividad mínimo o cero](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Recuperación ante desastres

SAP HANA en Azure (instancias grandes) se ofrece en dos regiones de Azure de una región geopolítica. Entre dos marcas de instancia grande Hola de dos regiones es una conectividad de red directa para la replicación de datos durante la recuperación ante desastres. replicación de Hola de datos de hello es en función de la infraestructura de almacenamiento. replicación de Hello no se realiza de forma predeterminada. Se realiza para las configuraciones de cliente de Hola que ordenadas de recuperación ante desastres de Hola. En el diseño actual de hello, replicación del sistema de archivos de HANA no se puede usar para la recuperación ante desastres.

Sin embargo, tootake ventaja de recuperación ante desastres de hello, necesita toostart toodesign Hola red conectividad toohello dos regiones de Azure. toodo por lo tanto, necesita una conexión de circuito de ExpressRoute de Azure desde el entorno local en su región Azure principal y otra conexión de circuito de región de recuperación ante desastres de tooyour local. Esta medida bastaría para cubrir una situación en la que hay un problema en toda una región de Azure, incluida la ubicación del enrutador perimetral de Microsoft Enterprise (MSEE).

Como una segunda medida, puede conectar todas las redes virtuales de Azure que se conectan tooSAP HANA en Azure (instancias de gran tamaño) en uno de hello regiones tooboth de los circuitos ExpressRoute. Esta medida resuelve un caso donde solo uno de ubicaciones de hello MSEE que se conecta a la ubicación local con Azure queda fuera de servicio.

Hello en la ilustración siguiente se muestra una configuración óptima hello para la recuperación ante desastres:

![Configuración óptima para la recuperación ante desastres](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Hello caso óptimo para una configuración de recuperación ante desastres de red de hello es toohave dos circuitos ExpressRoute de local toohello dos regiones de Azure. Un circuito va tooregion #1, donde se ejecuta una instancia de producción. circuito de ExpressRoute segundo Hola va tooregion #2, algunas instancias HANA no sea de producción en ejecución. (Esto es importante si una región de Azure completa, incluidos hello MSEE y marca de la instancia grande, se desconecta de la cuadrícula de hello).

Como una segunda medida Hola varias redes virtuales está conectada toohello varios circuitos ExpressRoute que están conectado tooSAP HANA en Azure (instancias de gran tamaño). Puede omitir la ubicación de Hola donde no se puede realizar un MSEE, o se pueden reducir el objetivo de punto de recuperación de Hola para recuperación ante desastres, tal y como se describe más adelante.

Hola siguientes requisitos para una instalación de recuperación ante desastres son:

- Debe ordenar SAP HANA en las SKU de hello mismo tamaño que el SKU de producción e implementarlos en la región de recuperación ante desastres de hello Azure (instancias de gran tamaño). Estas instancias pueden estar prueba toorun usado, espacio aislado o instancias de QA HANA.
- Debe solicitar un perfil de recuperación ante desastres para cada uno de sus SAP HANA en las SKU de Azure (instancias de gran tamaño) que desea que toorecover en el sitio de recuperación ante desastres de hello, si es necesario. Esta acción lleva toohello asignación de volúmenes de almacenamiento, que son destino de Hola de replicación de almacenamiento de hello de la región de producción en la región de recuperación ante desastres de Hola.

Después de cumplir Hola anterior de requisitos, es la replicación de almacenamiento de responsabilidad toostart Hola. En la infraestructura de almacenamiento de hello usa para SAP HANA en Azure (instancias grandes), base de Hola de replicación de almacenamiento es instantáneas de almacenamiento. replicación de recuperación ante desastres de hello toostart, necesita tooperform:

- Una instantánea del LUN de arranque que se describió anteriormente.
- Una instantánea de los volúmenes relacionados con HANA que se describieron anteriormente.

Después de ejecutar estas instantáneas, una réplica inicial de volúmenes de hello es visible en los volúmenes de Hola que están asociados con el perfil de recuperación ante desastres en la región de recuperación ante desastres de Hola.

Posteriormente, la instantánea más reciente de almacenamiento de Hola se usa cada hora los deltas de hello tooreplicate que desarrollan en volúmenes de almacenamiento de Hola.

objetivo de punto de recuperación de Hola que se logra con esta configuración es de 60 minutos de too90. tooachieve una recuperación mejor objetivo de punto de en caso de recuperación ante desastres de hello, Hola HANA transacciones registro copias de seguridad de SAP HANA en Azure (instancias de gran tamaño) toohello otra región de Azure. tooachieve este objetivo de punto de recuperación, Hola siguientes:

1. Realizar copias de seguridad Hola HANA transacción inicie sesión con tanta frecuencia como sea posible demasiado/hana/registro/copia de seguridad.
2. Copie las copias de seguridad del registro de transacciones de hello cuando están tooan termine de máquina virtual de Azure (VM), que se encuentra en una red virtual que se ha conectado toohello SAP HANA en servidor de Azure (instancias de gran tamaño).
3. De esa máquina virtual, copie tooa de copia de seguridad de hello VM que se encuentra en una red virtual en la región de recuperación ante desastres de Hola.
4. Mantener las copias de seguridad del registro de transacción de hello en esa región de hello VM.

En caso de desastre, después de que se ha implementado el perfil de recuperación ante desastres de hello en un servidor real, copie las copias de seguridad del registro de transacciones de Hola de hello VM toohello SAP HANA en Azure (instancias de gran tamaño) que es ahora Hola servidor principal en la región de recuperación ante desastres de hello, y Restaure las copias de seguridad. Esta recuperación es posible porque estado de Hola de HANA en discos de recuperación ante desastres de hello es una instantánea HANA. Se trata de punto de desplazamiento de Hola para restauraciones más de las copias de seguridad del registro de transacciones.

## <a name="backup-and-restore"></a>Copia de seguridad y restauración

Una de las bases de datos de toooperating de aspectos más importantes de hello es asegurarse de base de datos de hello puede protegerse desde diversos eventos catastróficos. Estos eventos pueden deberse a cualquier elemento de los errores de usuario de toosimple desastres naturales.

Realizar una copia de la base de datos, con hello capacidad toorestore tooany punto en el tiempo (como antes de que alguien elimina datos críticos), permite el estado de tooa de restauración que sea lo más parecida posible manera toohello que tenía antes de que se ha producido una interrupción Hola.

Para que el resultado sea óptimo, es preciso realizar dos tipos de copias de seguridad:

- Copias de seguridad de bases de datos
- Copias de seguridad del registro de transacciones

Además toofull las copias de seguridad realizadas en un nivel de aplicación, puede ser incluso más exhaustiva mediante la realización de copias de seguridad con instantáneas de almacenamiento. Realizar copias de seguridad de registro también es especialmente importante para restaurar la base de datos de hello (tooempty Hola registros y las transacciones confirmadas ya).

SAP HANA en Azure (instancias grandes) ofrece dos opciones de copia de seguridad y restauración:

- Opción personal (DIY, por las siglas de Do It Yourself). Una vez calculados tooensure suficiente espacio en disco, realizar copias de seguridad completas de base de datos y de registro mediante el uso de métodos de copia de seguridad de disco (discos de toothose). Con el tiempo, las copias de seguridad de hello copiado tooan cuenta de almacenamiento de Azure (después de configurar un servidor de archivos basado en Azure con almacenamiento prácticamente ilimitada), o utilizan un almacén de copia de seguridad de Azure o el almacenamiento de Azure frío. Otra opción es toouse una herramienta de protección de datos de terceros, como Commvault, toostore hello las copias de seguridad una vez que copia tooa cuenta de almacenamiento. Hola guía opción de copia de seguridad también podría ser necesario para los datos que necesita toobe almacenado durante periodos más largos para fines de auditoría y cumplimiento.
- Usar copia de seguridad de Hola y restaurar la funcionalidad que Hola infraestructura subyacente de SAP HANA en Azure (instancias de gran tamaño) proporciona. Esta opción satisface la necesidad de Hola para copias de seguridad y realiza copias de seguridad manuales casi obsoleta (excepto que las copias de seguridad de datos son necesarias para fines de cumplimiento). resto de Hola de direcciones de esta sección Hola copia de seguridad y restaurar la funcionalidad que se ofrece con HANA (instancias de gran tamaño).

> [!NOTE]
> tecnología de copia instantánea Hola utilizado por la infraestructura subyacente de Hola de HANA (instancias de gran tamaño) tiene una dependencia en las instantáneas de SAP HANA. Las instantáneas de SAP HANA no funcionan con los contenedores de base de datos multiinquilino de SAP HANA. Como resultado, este método de copia de seguridad no puede ser usado toodeploy SAP HANA para varios inquilinos base de datos de contenedores.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Uso de instantáneas de almacenamiento de SAP HANA en Azure (instancias grandes)

infraestructura de almacenamiento de Hello subyacente SAP HANA en Azure (instancias de gran tamaño) admite la noción de Hola de una instantánea de almacenamiento de los volúmenes. Se admiten copias de seguridad y restauración de un volumen en particular, con hello siguientes consideraciones:

- En lugar de las copias de seguridad de bases de datos, se toman instantáneas del volumen de almacenamiento con frecuencia.
- instantáneas de almacenamiento de Hello inicia una instantánea de SAP HANA antes de ejecutar instantáneas de almacenamiento de Hola. Esta instantánea de SAP HANA es punto de instalación de Hola para las restauraciones de registro final después de la recuperación de instantánea de almacenamiento de Hola.
- En el momento de Hola donde instantánea del almacenamiento de Hola se ejecuta correctamente, se elimina la instantánea de SAP HANA Hola.
- Las copias de seguridad de registros se realizan con frecuencia y se almacenan en el volumen de copia de seguridad de registro de Hola o en Azure.
- Si es necesario restaurar la base de datos de hello tooa determinado momento dado, se realiza una solicitud tooMicrosoft soporte técnico de Azure (interrupción de producción) o SAP HANA en administración de servicios de Azure toorestore tooa determinadas instantáneas de almacenamiento (por ejemplo, una planeada restauración de un sistema de espacio aislado estado de tooits original).
- instantánea de SAP HANA Hola que ha incluido en la instantánea de almacenamiento de hello es un punto de desplazamiento para aplicar las copias de seguridad de registro que se han ejecutado y almacenado después de que se tomó la instantánea del almacenamiento de Hola.
- Estas copias de seguridad de registros se realizan toorestore Hola base de datos back-tooa determinado momento dado.

Especificar copia de seguridad de hello\_nombre crea una instantánea de hello siguientes volúmenes:

- hana/data
- hana/log
- hana/log\_backup (montada como copia de seguridad en hana/log)
- hana/shared

### <a name="storage-snapshot-considerations"></a>Consideraciones de las instantáneas de almacenamiento

>[!NOTE]
>Las instantáneas de almacenamiento _no_ se proporcionan de forma gratuita, ya que se debe asignar espacio de almacenamiento adicional.

entre los mecanismos específicos de Hola de instantáneas de almacenamiento de SAP HANA en Azure (instancias de gran tamaño) se incluyen:

- Una instantánea de almacenamiento específico (en el momento de hello en el tiempo cuando se considera) consume muy poco almacenamiento.
- Como los cambios de contenido de datos y el contenido de hello en los datos de SAP HANA cambian archivos en el volumen de almacenamiento de hello, instantánea Hola debe bloquear el contenido original toostore Hola.
- instantáneas de almacenamiento de Hello aumenta de tamaño. existe Hello más Hola instantánea, Hola mayor Hola almacenamiento instantánea deje de ser.
- Hola más cambios realizados toohello volumen de base de datos de SAP HANA largo de duración de Hola de una instantánea de almacenamiento, se vuelve de instantánea de almacenamiento de hello de la mayor consumo de espacio Hola Hola.

SAP HANA en Azure (instancias de gran tamaño) incluye los tamaños de volumen fijo para el volumen de datos y de registro de SAP HANA Hola. Realizar instantáneas de estos volúmenes come en su espacio de volumen, por lo que las instantáneas de almacenamiento de responsabilidad tooschedule (dentro de Hola SAP HANA en proceso de Azure [instancias grandes]).

Hello secciones siguientes proporcionan información para llevar a cabo estas instantáneas, incluidas las recomendaciones generales:

- Aunque el hardware de hello puede admitir 255 instantáneas por volumen, se recomienda encarecidamente que está por debajo de este número.
- Antes de realizar instantáneas de almacenamiento, supervise y realice un seguimiento del espacio disponible.
- Menor número de Hola de instantáneas de almacenamiento en función del espacio libre. Tendrá que toolower número de Hola de instantáneas que mantienen o tendrá que los volúmenes de hello tooextend. (puede solicitar más almacenamiento en unidades de 1 TB).
- Durante actividades como mover datos a SAP HANA con herramientas de migración del sistema (con R3load o mediante la restauración de bases de datos de SAP HANA desde copias de seguridad), se recomienda encarecidamente no realizar instantáneas del almacenamiento (Si se realiza una migración del sistema en un nuevo sistema de SAP HANA, instantáneas de almacenamiento no necesitaría toobe realiza.)
- Durante reorganizaciones mayores de tablas de SAP HANA, debe evitarse realizar instantáneas de mantenimiento, siempre que sea posible.
- Las instantáneas de almacenamiento son un capacidades de recuperación ante desastres de hello tooengaging requisitos previos de SAP HANA en Azure (instancias de gran tamaño).

### <a name="setting-up-storage-snapshots"></a>Configuración de instantáneas del almacenamiento

1. Asegúrese de que Perl está instalado en el sistema de operativo Linux hello en servidor de hello HANA (instancias de gran tamaño).
2. Modificar/etcetera/ssh/ssh\_línea hello de configuración tooadd _Mac hmac-sha1_.
3. Cree una cuenta de usuario de copia de seguridad de SAP HANA en el nodo principal de Hola para cada instancia de SAP HANA que se está ejecutando (si procede).
4. cliente de SAP HANA HDB Hola debe instalarse en todos los servidores de SAP HANA (instancias de gran tamaño).
5. En hello primer SAP HANA (instancias de gran tamaño) servidor de cada región, una clave pública debe crearse hello tooaccess subyacente de la infraestructura de almacenamiento que controla la creación de instantáneas.
6. Copie el script de Hola azure\_hana\_backup.pl de ubicación de toohello/scripts de **hdbsql** de hello instalación de SAP HANA.
7. Hello HANABackupDetails.txt de copia de archivos de toohello/scripts misma ubicación como hello secuencia de comandos Perl.
8. Modificar hello HANABackupDetails.txt archivo según sea necesario para las especificaciones del cliente adecuado de Hola.

### <a name="step-1-install-sap-hana-hdbclient"></a>Paso 1: Instalar HDBClient de SAP HANA

Hola Linux instalado en SAP HANA en Azure (instancias de gran tamaño) incluye carpetas de Hola y scripts de instantáneas de almacenamiento de SAP HANA tooexecute necesarios para fines de copia de seguridad y recuperación ante desastres. Sin embargo, es su tooinstall responsabilidad SAP HANA HDBclient durante la instalación de SAP HANA. (Microsoft instala hello HDBclient ni SAP HANA).

### <a name="step-2-change-etcsshsshconfig"></a>Paso 2: Cambiar/etc/ssh/ssh\_config

Cambie /etc/ssh/ssh\_config agregando la línea _MACs hmac-sha1_, como se muestra a continuación:
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>Paso 3: Crear una clave pública

En hello primera SAP HANA en servidor de Azure (instancias grandes) en cada región de Azure, cree una infraestructura de almacenamiento de toobe de clave pública utiliza tooaccess Hola para que pueda crear instantáneas. clave pública de Hello garantiza que una contraseña no es necesario toosign en almacenamiento de toohello y que no se mantienen las credenciales de contraseña. En Linux en el servidor de SAP HANA (instancias de gran tamaño) hello, ejecute hello después de la clave pública de comando toogenerate hello:
```
  ssh-keygen –t dsa –b 1024
```
nueva ubicación de Hello es _/root/.ssh/id\_dsa.pub. No escriba una frase de contraseña real o, de lo contrario, será de frase de contraseña de hello tooenter necesario cada vez que inicie sesión. En su lugar, presione **ENTRAR** dos veces tooremove Hola especifique el requisito de frase de contraseña para iniciar sesión en.

Comprobar toomake seguro esa clave pública Hola corregida según lo previsto cambiar las carpetas too/root/.ssh/ y, a continuación, ejecutando hello **ls** comando. Si Hola clave está presente, puede copiarlo ejecutando Hola siguiente comando:

![Para copiar la clave pública, se ejecuta este comando](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

En este momento, póngase en contacto con SAP HANA en administración de servicios de Azure y proporcionar la clave de Hola. representante del servicio de Hello usa tooregister de clave pública de hello en hello infraestructura de almacenamiento subyacente.

### <a name="step-4-create-an-sap-hana-user-account"></a>Paso 4: Crear una cuenta de usuario de SAP HANA

Cree una cuenta de usuario de SAP HANA en SAP HANA Studio para realizar copias de seguridad. Esta cuenta debe tener Hola siguientes privilegios: _Administrador de copia de seguridad_ y _lectura de catálogo_. En este ejemplo, el nombre de usuario de hello SCADMIN se crea.

![Creación de un usuario en HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>Paso 5: Autorizar la cuenta de usuario de SAP HANA Hola

Autorizar la cuenta de usuario de SAP HANA hello (toobe usado por las secuencias de comandos de hello sin necesidad de autorización cada vez que se ejecuta el script de Hola). Hola comando SAP HANA `hdbuserstore` permite la creación de hello de una clave de usuario de SAP HANA, que se almacena en uno o más nodos de SAP HANA. clave de usuario de Hello también permite Hola usuario tooaccess SAP HANA sin tener contraseñas toomanage desde dentro de hello secuencias de comandos de proceso que se describe más adelante.

>[!IMPORTANT]
>Ejecución hello después del comando como `_root_`. En caso contrario, el script de Hola no puede funcionar correctamente.

Escriba hello `hdbuserstore` comando como sigue:

![Escriba el comando de hello hdbuserstore](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

En el siguiente ejemplo, donde hello usuario SCADMIN01 y nombre de host de hello es lhanad01, el Hola comando hello es:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Administre todo el scripting desde un único servidor para las instancias de HANA de escalado horizontal. En este ejemplo, la clave de SAP HANA hello SCADMIN01 debe modificarse para cada host de forma que refleje el host de Hola que es clave toohello relacionados. Es decir, se modificará Hola cuenta de copia de seguridad de SAP HANA con número de instancia de Hola de Hola DB HANA, **lhanad**. clave de Hello debe tener privilegios administrativos en el host de Hola se asigna a y usuario de copia de seguridad de hello para la implementación escalada debe tener instancias de SAP HANA de tooall de derechos de acceso.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>Paso 6: Copiar elementos de carpeta de Hola/scripts

Siguiente de hello copia elementos de Hola/secuencias de comandos de directorio de trabajo de carpeta (incluida en la imagen de hello gold de instalación de hello) toohello para **hdbsql**. En el caso de las instalaciones actuales de HANA, se trata de /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Copie Hola siguientes elementos si se están ejecutando escalado horizontal o OLAP:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
archivo de HANABackupCustomerDetails.txt Hello es modificable como se indica a continuación para una implementación de escalado vertical. Es archivo de control y la configuración de hello para el script de Hola que ejecuta las instantáneas de almacenamiento de Hola. Debe haber recibido hello _nombre de la copia de seguridad de almacenamiento_ y _dirección IP de almacenamiento_ de SAP HANA en administración de servicios de Azure cuando se implementaron las instancias. No se puede modificar la secuencia hello, ordenación o espaciado de cualquiera de las variables de hello, o el script de Hola no se ejecuta correctamente.

Para una implementación de escalado vertical, archivo de configuración de hello sería:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Para una configuración de escalado horizontal, hello HANABackupCustomerDetailsBW.txt archivo sería:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Actualmente, solamente los detalles de nodo 1 se usan en el script de Hola real HANA almacenamiento a la instantánea. Le recomendamos que pruebe tooor de acceso de todos los nodos HANA para que, si el nodo de copia de seguridad maestro Hola cambia en algún momento, ya se ha asegurado que cualquier otro nodo puede ocupar su lugar mediante la modificación de detalles de hello en el nodo 1.

toocheck para configuraciones correctas de hello en el archivo de configuración de Hola o instancias HANA toohello conectividad correcta, ejecute cualquiera de hello siguientes secuencias de comandos:
- Para una configuración de escalado vertical (independientemente de la carga de trabajo de SAP):

 ```
testHANAConnection.pl
```
- Para una configuración de escalado horizontal:

 ```
testHANAConnectionBW.pl
```

Asegúrese de que esa instancia HANA maestra hello tiene servidores de acceso de HANA tooall necesario. No hay ninguna secuencia de comandos de toohello de parámetros, pero debe completar Hola adecuado HANABackupCustomerDetails / HANABackupCustomerDetailsBW file para hello script toorun correctamente. Dado que se devuelven códigos de error sólo Hola el comando del shell, no es posible para hello script tooerror-comprobar todas las instancias. Aun así, el script de Hola proporcionar algunos comentarios útiles para toodouble comprobación.

script de Hola toorun:
```
 ./testHANAConnection.pl
```
 Si el script de Hola obtiene correctamente la estado Hola de instancia HANA hello, muestra un mensaje que conexión de HANA Hola se estableció correctamente.

Además, hay un segundo tipo de secuencia de comandos puede utilizar toosign de capacidad del servidor de las instancia HANA maestro de toocheck hello en el almacenamiento de toohello. Antes de ejecutar azure hello\_hana\_copia de seguridad (\_bw). pl script, debe ejecutar el siguiente script de Hola. Si un volumen contiene no hay instantáneas, es imposible toodetermine si el volumen de hello es simplemente vacía o no hay un ssh Hola de error tooobtain detalles de la instantánea. Por este motivo, el script de Hola ejecuta dos pasos:

- Comprueba que Hola storage console es accesible.
- Crea una instantánea de prueba, o ficticia, para cada volumen por instancia de HANA.

Por esta razón, instancia HANA Hola se incluye como un argumento. Nuevo, no es posible tooprovide comprobación de errores de conexión de almacenamiento de hello, pero el script de Hola proporciona sugerencias útiles si se produce un error en la ejecución de Hola.

script de Hola se ejecuta como:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
También se puede ejecutar como:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
script de Hola también muestra un mensaje que es capaz de toosign en adecuadamente inquilino de almacenamiento de tooyour implementado, que se organiza en torno a los números de unidad lógica hello (LUN) que se utilizan en instancias de servidor hello que usted es el propietario.

Antes de ejecutar Hola primeras almacenamiento basados en instantáneas copias de seguridad, ejecute toomake de secuencias de comandos siguiente de hello seguro de que la configuración de hello es correcta.

Después de ejecutar estos scripts, puede eliminar las instantáneas de hello ejecutando:
```
./removeTestStorageSnapshot.pl <hana instance>
```
O
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Paso 7: Realizar instantáneas a petición

Realice instantáneas a petición (así como programar instantáneas periódicas mediante cron) tal y como se describe aquí.

Las configuraciones de escalado vertical, ejecute hello siguiente secuencia de comandos:
```
./azure_hana_backup.pl lhanad01 customer 20
```
Las configuraciones de escalado horizontal, ejecute hello siguiente secuencia de comandos:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
script de escalado horizontal de Hello realiza algunas toomake comprobación adicional seguro de que pueden tener acceso a todos los servidores HANA y todas las instancias HANA devuelven el estado apropiado de instancia de hello antes de continuar con la creación de instantáneas de SAP HANA o almacenamiento.

Hola argumentos siguientes es necesario:

- copia de seguridad que requieren Hola HANA instancia.
- prefijo de instantánea de Hola para instantáneas de almacenamiento de Hola.
- número de Hola de toobe instantáneas conservado por prefijo concreto Hola.

```
./azure_hana_backup.pl lhanad01 customer 20
```

ejecución de Hola de script de Hola crea instantáneas de almacenamiento de hello en estas tres fases distintas:

- Ejecutar una instantánea de HANA.
- Ejecutar una instantánea del almacenamiento.
- Quitar instantáneas HANA Hola.

Ejecutar script de Hola llamarlo desde la carpeta ejecutable de hello HDB que se copió al. Se realiza una copia de al menos Hola después de volúmenes, pero también hace una copia de cualquier volumen que tiene el nombre de instancia de SAP HANA explícito de hello en nombre de volumen de Hola.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
período de retención de Hello estrictamente se administra con el número de Hola de instantáneas que se envían como un parámetro al ejecutar script de Hola (por ejemplo, 20, que se ha mostrado anteriormente). Por lo que la cantidad de Hola de tiempo es una función del período de Hola de hello y ejecución número de instantáneas en la llamada de Hola de script de Hola. Si número Hola de instantáneas que se mantienen supera número hello cuyos nombres como un parámetro en la llamada de Hola de secuencia de comandos de hello, Hola instantánea más antigua de almacenamiento de esta etiqueta (en nuestro caso anterior, _personalizado_) se elimina antes de que sea una instantánea nueva ejecutar. Esto significa número Hola que dar como último parámetro de llamada de hello hello es número Hola puede utilizar toocontrol Hola número de instantáneas.

>[!NOTE]
>Tan pronto como cambie la etiqueta de hello, contando Hola se inicia de nuevo.

Necesita tooinclude Hola HANA nombre de la instancia proporcionada por SAP HANA en administración de servicios de Azure como argumento si va a crear instantáneas en entornos de varios nodos. En entornos de nodo único, nombre de Hola de hello SAP HANA en la unidad de Azure (instancias de gran tamaño) es suficiente, pero todavía se recomienda el nombre de instancia HANA Hola.

Además, se puede realizar copias de seguridad volumes\LUNs de arranque mediante el uso de Hola mismo script. Debe hacer una copia de seguridad de su volumen de arranque, al menos, una vez la primera vez que se ejecute HANA, aunque se recomienda programar una copia de seguridad semanal o nocturna del arranque en cron. En su lugar de agregar un nombre de instancia de SAP HANA, insertar _arranque_ como Hola argumento en el script de Hola como sigue:
```
./azure_hana_backup boot customer 20
```
Hello misma política de retención que otorgue toohello también volumen de arranque. Usar instantáneas de petición, tal como se describe anteriormente, en los casos especiales, como durante una actualización del paquete (EHP) de mejora de SAP, o cuando sea necesario toocreate una instantánea de almacenamiento diferenciado.

Le recomendamos que tooperform programada de instantáneas de almacenamiento mediante cron y se recomienda usar el mismo script de Hola para todas las necesidades de recuperación ante desastres (modificación Hola script entradas toomatch Hola distintos habían solicitado tiempos de copia de seguridad) y las copias de seguridad. Todas ellas se programan de forma diferente en cron en función de su tiempo de ejecución: cada hora, cada 12 horas, a diario o semanalmente. programación de cron Hello es toocreate diseñada instantáneas de almacenamiento que coinciden con el etiquetado de retención de hello descrita anteriormente para copia de seguridad a largo plazo fuera del sitio. script de Hola incluye comandos tooback seguridad de todos los volúmenes de producción, según su frecuencia solicitado (archivos de datos y de registro se copian cada hora, mientras que el volumen de arranque de Hola se copia de seguridad diaria).

las entradas de Hola Hola siguiente secuencia de comandos de cron ejecutan cada hora en hello diez minutos, cada 12 horas en hello diez minutos y diariamente en hello diez minutos. cron Hola trabajos se crean de forma que sólo una instantánea del almacenamiento de SAP HANA tiene lugar durante las horas determinada, por lo que hello las copias de seguridad por horas y día no se producen en hello que mismo tiempo (12:10 A.M.). toohelp optimizar la creación de instantáneas y replicación, SAP HANA en administración de servicios de Azure proporciona Hola recomienda tiempo para toorun las copias de seguridad.

Hola predeterminado cron programar en /etc/crontab es como sigue:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
En instrucciones de cron anteriores hello, volúmenes HANA hello (sin el volumen de arranque) obtienen por horas de instantánea con la etiqueta de Hola. De todas estas instantáneas se conservan 66. Además, se conservan 14 instantáneas con etiqueta de hello 12 horas. Es posible que obtenga instantáneas cada hora durante 3 días, además de instantáneas cada 12 horas durante otros 4 días, por lo que estará recibiendo instantáneas durante toda una semana.

Programación dentro de cron puede ser complicada, porque solo una secuencia de comandos debe ejecutarse en un momento dado, a menos que las secuencias de comandos de Hola se escalonan por varios minutos. Si desea que las copias de seguridad diarias para la retención a largo plazo, una instantánea diaria se conserva junto con una instantánea de 12 horas (con un recuento de retención de cada siete) o instantánea por hora de hello es escalonada tootake lugar 10 minutos más tarde. Solo una instantánea diaria se conserva en el volumen de producción de hello.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
las frecuencias de Hello enumeradas aquí son sólo ejemplos. tooderive el número óptimo de instantáneas, siguiendo criterios de Hola de uso:

- Requisitos de objetivo de tiempo de recuperación para la recuperación a un momento dado.
- Uso del espacio.
- Requisitos de objetivos de punto de recuperación y de tiempo de recuperación para una posible recuperación ante desastres.
- Ejecución eventual de copias de seguridad completas de la base de datos de HANA en discos. Cada vez que una copia de seguridad completa de la base de datos en los discos, o _backint_ interfaz, es lleva a cabo, produce un error de ejecución de Hola de instantáneas de almacenamiento. Si tiene previsto tooexecute copias de seguridad completa de la base de datos sobre las instantáneas de almacenamiento, asegúrese de que la ejecución de Hola de instantáneas de almacenamiento está deshabilitada durante este tiempo.

>[!IMPORTANT]
> uso de Hola de instantáneas de almacenamiento para las copias de seguridad de SAP HANA sólo es válido cuando se realizan instantáneas Hola junto con las copias de seguridad del registro de SAP HANA. Las copias de seguridad necesario toobe toocover capaz de Hola estos registro de períodos de tiempo entre las instantáneas de almacenamiento de Hola. Si ha configurado un toousers de compromiso de una recuperación en el momento de 30 días, necesita Hola siguiente:

- Capacidad tooaccess una instantánea de almacenamiento es de 30 días de antigüedad.
- Copias de seguridad de registros contiguos en hello últimos 30 días.

Intervalo de Hola de copias de seguridad del registro, crear una instantánea del volumen de copia de seguridad del registro de hello también. No obstante, tener tooperform seguro de las copias de seguridad de registros periódicas para que pueda:

- Las copias de seguridad de registros contiguos de hello es recuperaciones de punto en el tiempo de tooperform tuviera.
- Impedir que quedarse sin espacio de volumen de registro de hello SAP HANA.

Uno de los últimos pasos de hello es tooschedule los registros de copia de seguridad de SAP HANA en SAP HANA Studio. destino de copia de seguridad del registro de SAP HANA de Hello es Hola creada especialmente hana/registro\_volumen de las copias de seguridad con un punto de montaje de Hola de /hana/log/backups.

![Programe los registros de copia de seguridad de SAP HANA en SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

Puede elegir que las copias de seguridad se realicen con una frecuencia superior a 15 minutos. Algunos usuarios incluso realizan copias de seguridad del registro cada minuto; sin embargo, no se recomienda _superar_ los 15 minutos.

Hola último paso es tooperform basado en un archivo de copia de seguridad (tras la instalación inicial de Hola de SAP HANA) toocreate una sola entrada de copia de seguridad que debe existir en el catálogo de copia de seguridad de Hola. En caso contrario, SAP HANA no podrá iniciar las copias de seguridad del registro especificadas.

![Realizar una sola entrada de copia de seguridad de un toocreate de copia de seguridad basada en archivos](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Supervisión de Hola de número y tamaño de las instantáneas de volumen de disco de Hola

En un volumen de almacenamiento en particular, puede supervisar el número de Hola de instantáneas y el consumo de almacenamiento de Hola de instantáneas. Hola `ls` comando no muestra hello instantánea directorio o los archivos. Sin embargo, Hola comando del sistema operativo Linux `du` realiza, con hello siguientes comandos:

- `du –sh .snapshot`Proporciona un total de todas las instantáneas en el directorio de instantáneas de Hola.
- `du –sh --max-depth=1`Enumera todas las instantáneas que se guardan en la carpeta de .snapshot de Hola y Hola de cada instantánea.
- `du –hc`proporciona el tamaño total de hello utilizado por todas las instantáneas.

Use estos toomake comandos seguro de que las instantáneas de Hola que se toman y almacenan no consumen todo el almacenamiento en volúmenes de Hola Hola.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Reducir el número de Hola de instantáneas en un servidor

Tal y como se ha explicado anteriormente, puede reducir el número Hola de determinadas etiquetas de instantáneas que se almacenan. Hola últimos dos parámetros de hello comando tooinitiate una instantánea son un número hello y etiqueta de instantáneas que desea tooretain.
```
./azure_hana_backup.pl lhanad01 customer 20
```
En el ejemplo anterior de hello, etiqueta de instantánea de hello es _cliente_ y número de Hola de instantáneas con este toobe etiqueta conservan es _20_. Como responder toodisk consumo de espacio, conviene tooreduce número de Hola de instantáneas almacenadas. número de hello tooreduce de instantáneas es el script de Hola de toorun con hello último parámetro conjunto too5 de manera sencilla de Hello:
```
./azure_hana_backup.pl lhanad01 customer 5
```
Como resultado de script en ejecución Hola con esta configuración, número de Hola de instantáneas, incluido el almacenamiento de hello nueva instantánea, es _5_.

 >[!NOTE]
 > Este script reduce el número de Hola de instantáneas solo si la instantánea anterior más reciente de hello tiene más de una hora de antigüedad. script de Hola no elimina las instantáneas que son menos de una hora de antigüedad.

Estas restricciones son la funcionalidad de recuperación ante desastres opcional toohello relacionados que ofrece.

Si ya no desea toomaintain un conjunto de instantáneas con el prefijo, puede ejecutar el script de Hola con _0_ como hello retención número tooremove todas las instantáneas de coincidencia de prefijo. Sin embargo, quitar todas las instantáneas puede afectar a las capacidades de Hola de recuperación ante desastres.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>Recuperación de la instantánea más reciente de HANA de toohello

En caso de Hola que experimenta un escenario de producción en profundidad, el proceso de Hola de recuperarse de una instantánea de almacenamiento se puede iniciar como un incidente de cliente con SAP HANA en administración de servicios de Azure. Un escenario de este tipo inesperado podría ser una cuestión de urgencia altos si se eliminarán los datos de producción hello y sistema sola forma datos de hello tooretrieve están la base de datos de producción de hello de toorestore.

En hello otra parte, una recuperación en un momento podría ser urgencia baja y planeado para días de antelación. Para planearlo, se puede usar SAP HANA en Azure Service Management, en lugar de generar un problema de prioridad alta. Por ejemplo, prepararse tootry una actualización de software SAP de hello aplicando un nuevo paquete de mejora y, a continuación, necesita toorevert hacer copia de instantánea tooa que representa el estado de hello antes de la actualización de hello EHP.

Antes de emitir la solicitud de hello, deberá toodo preparación. SAP HANA en el equipo de administración de servicios de Azure puede controlar la solicitud de Hola y proporcionar volúmenes de hello restaurar. A continuación, es la tooyou toorestore Hola HANA base de datos basándose en instantáneas de Hola. Le mostramos cómo solicitar tooprepare para hello:

>[!NOTE]
>La interfaz de usuario puede variar de hello siguientes capturas de pantalla, dependiendo de Hola versión de SAP HANA que usa.

1. Decidir qué toorestore de instantánea. Solo el volumen de datos/hana Hola se restauraría a menos que se indique lo contrario.

2. Cierre la instancia HANA Hola.

 ![Cerrar la instancia HANA Hola](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Desmonte los volúmenes de datos de hello en cada nodo de la base de datos HANA. se produce un error en la restauración de Hola de instantánea de Hola si no se desmontan volúmenes de datos de Hola.

 ![Desmonte los volúmenes de datos de hello en cada nodo de la base de datos HANA](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Abra una restauración de Hola de tooinstruct de solicitud de soporte técnico de Azure de una instantánea concreta.

 - Durante la restauración de hello: SAP HANA en administración de servicios de Azure podría pedirle que tooattend un tooensure de llamada de conferencia que no se pueden obtener perder ningún dato.

 - Después de la restauración de hello: SAP HANA en administración de servicios de Azure le avisa cuando se ha restaurado la instantánea de almacenamiento de Hola.

5. Una vez completado el proceso de restauración de hello, volver a montar todos los volúmenes de datos.

 ![Volver a montar todos los volúmenes de datos](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Seleccione las opciones de recuperación dentro de SAP HANA Studio, si no automáticamente iniciará cuando se vuelve a conectar tooHANA base de datos a través de SAP HANA Studio. Hello en el ejemplo siguiente se muestra una instantánea HANA última restauración toohello. Una instantánea de almacenamiento incrusta una instantánea HANA y si va a restaurar la instantánea más reciente de almacenamiento de toohello, debe ser instantánea más reciente de HANA de Hola. (Si va a restaurar instantáneas de almacenamiento tooolder, necesita toolocate se tomó Hola HANA instantánea según Hola tiempo Hola almacenamiento instantánea.)

 ![Seleccionar las opciones de recuperación en SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Seleccione **recuperar hello tooa datos específicos copia de seguridad o almacenamiento de instantánea de base**.

 ![ventana de "Seleccionar tipo de recuperación" Hello](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Seleccione **Specify backup without catalog** (Especificar copia de seguridad sin catálogo).

 ![ventana de "Especificar la ubicación de copia de seguridad" Hello](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. Hola **tipo de destino** lista, seleccione **instantánea**.

 ![ventana de "Especificar hello tooRecover de copia de seguridad" Hello](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Haga clic en **finalizar** proceso de recuperación de toostart Hola.

 ![Haga clic en "Finalizar" proceso de recuperación de hello toostart](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. base de datos HANA Hola se restaura y recupera la instantánea HANA toohello que se incluye en la instantánea de almacenamiento de Hola.

 ![Base de datos HANA es instantánea HANA toohello restaurados y recuperados](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Recuperación de estado más reciente de toohello

Hello siguiente proceso restaura la instantánea HANA Hola que se incluye en la instantánea de almacenamiento de Hola. A continuación, restaura Hola transacciones registro las copias de seguridad toohello estado más reciente de la base de datos de hello antes de restaurar instantáneas de almacenamiento de Hola.

>[!IMPORTANT]
>Antes de continuar, asegúrese de que dispone de una cadena completa y contigua de copias de seguridad del registro de transacciones. Sin estas copias de seguridad, no puede restaurar el estado actual de Hola de base de datos de Hola.

1. Complete los pasos 1 a 6 de hello precede el procedimiento de "Recuperación toohello instantánea más reciente HANA."

2. Seleccione **recuperar estado más reciente de la base de datos hello tooits**.

 ![Seleccione "Recuperar el estado más reciente de tooits de base de datos de hello"](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Especifique la ubicación de Hola de copias de seguridad del registro de hello más reciente HANA. ubicación de Hello necesita toocontain todas las copias de seguridad de registro de transacciones de HANA de estado más reciente de hello HANA instantánea toohello.

 ![Especificar ubicación de Hola de copias de seguridad del registro de hello más reciente HANA](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Seleccione una copia de seguridad como base de la base de datos de hello toorecover. En nuestro ejemplo, se trata de instantánea HANA Hola que se incluyó en la instantánea de almacenamiento de Hola. (Solo una instantánea aparece en la siguiente captura de pantalla de Hola.)

 ![Seleccione una copia de seguridad como base de la base de datos de hello toorecover](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Desactive hello **usar copias de seguridad diferencial** casilla de verificación si no existen diferencias entre tiempo Hola de instantánea HANA Hola y el estado más reciente de Hola.

 ![Casilla de verificación de hello desactive "Usar copias de seguridad de diferencias" Si no hay diferencias existe](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. En la pantalla de resumen de bienvenida, haga clic en **finalizar** procedimiento de restauración de toostart Hola.

 ![Haga clic en "Finalizar" en la pantalla de resumen de bienvenida](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Punto de recuperación tooanother en el tiempo
toorecover tooa punto en el tiempo entre la instantánea HANA hello (incluidas en la instantánea de almacenamiento de hello) y otro que es posterior a la de hello HANA instantánea tiempo de punto de recuperación, Hola siguientes:

1. Asegúrese de que dispone de todas las copias de seguridad de registro de transacciones de hello HANA instantánea toohello tiempo que desea toorecover.
2. Comenzar Hola procedimiento bajo "Recovering toohello más reciente estado".
3. En el paso 2 del procedimiento de hello, Hola **Seleccionar tipo de recuperación** ventana, seleccione **siguiente de toohello de base de datos de Hola de recuperación al momento dado**especificar Hola momento y, a continuación, complete los pasos del 3 al 6.

## <a name="monitoring-hello-execution-of-snapshots"></a>Supervisión de la ejecución de Hola de instantáneas

Necesita toomonitor ejecución de Hola de instantáneas de almacenamiento. script de Hola que ejecute una instantánea de almacenamiento escribe el archivo de salida tooa y, a continuación, lo guarda toohello misma ubicación que las secuencias de comandos Perl de Hola. Se escribe un archivo independiente para cada instantánea. salida de Hello de cada archivo de muestra claramente Hola diversas fases que se ejecuta la secuencia de comandos de hello instantánea:

- Buscar una instantánea de volúmenes de Hola que necesitan toocreate
- Buscar las instantáneas de hello tomadas de estos volúmenes
- Eliminar eventual existente instantáneas toomatch Hola número de instantáneas especificada
- Creación de una instantánea de HANA
- Crear instantáneas de almacenamiento de hello sobre volúmenes de Hola
- La eliminación de instantánea HANA Hola
- Cambiar el nombre hello más reciente de instantánea demasiado**.0**

parte más importante de Hola de script de Hola es esta:
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
De este ejemplo puede ver cómo los registros de script de Hola Hola creación de instantánea HANA Hola. En caso de escalado horizontal de hello, este proceso se inicia en el nodo principal de Hola. nodo maestro Hola inicia la creación sincrónico Hola de instantáneas de hello en cada uno de los nodos de trabajador de Hola. A continuación, se toma la instantánea de almacenamiento de Hola. Tras la ejecución correcta de Hola de instantáneas de almacenamiento de hello, se elimina la instantánea HANA Hola.
