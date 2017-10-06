---
title: aaaUse Phoenix Apache y ardilla con basados en Windows Azure HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Phoenix Apache en HDInsight y cómo tooinstall y configurar ardilla en el clúster de estación de trabajo tooconnect tooan HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Uso de Apache Phoenix y SQuirreL con clústeres de HBase basados en Windows en HDinsight
Obtenga información acerca de cómo toouse [Apache Phoenix](http://phoenix.apache.org/) en HDInsight y cómo tooinstall y configurar ardilla en el clúster de estación de trabajo tooconnect tooan HBase en HDInsight. Para obtener más información acerca de Phoenix, consulte [Phoenix en 15 minutos o menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Hola gramática de Phoenix, encontrará [gramática de Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Para obtener información de versión de Phoenix en HDInsight de hello, consulte [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Hola pasos de este trabajo sólo de documento para clústeres de HDInsight basados en Windows. HDInsight solo está disponible en Windows en versiones inferiores a la 3.4. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para más información sobre el uso de Phoenix en HDInsight basado en Linux, consulte [Use Apache Phoenix with Linux-based HBase clusters in HDinsight](hdinsight-hbase-phoenix-squirrel-linux.md)(Uso de Apache Phoenix con clústeres de HBase basados en Linux en HDinsight).
>



## <a name="use-sqlline"></a>Uso de SQLLine
[SQLLine](http://sqlline.sourceforge.net/) es un tooexecute de utilidad de línea de comandos SQL.

### <a name="prerequisites"></a>Requisitos previos
Para poder usar SQLLine, debe tener el siguiente hello:

* **Un clúster de HBase en HDInsight**. Para obtener información sobre el aprovisionamiento del clúster de HBase, consulte [Introducción a HBase Apache en HDInsight][hdinsight-hbase-get-started].
* **Conectar el clúster de HBase toohello a través del protocolo de escritorio remoto de hello**. Para obtener instrucciones, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de hello Portal clásico de Azure][hdinsight-manage-portal].

**toofind el nombre de host de Hola**

1. Abra **línea de comandos de Hadoop** de escritorio de Hola.
2. Ejecute hello después de sufijo DNS de comando tooget hello:

        ipconfig

    Escriba el **sufijo DNS específico de la conexión**. Por ejemplo, *myhbasecluster.f5.internal.cloudapp.net*. Cuando se conecta el clúster de HBase tooan, necesitará tooconnect tooone de Zookeepers hello mediante FQDN. Cada clúster de HDInsight tiene 3 Zookeepers. Son *zookeeper0*, *zookeeper1* y *zookeeper2*. Hello FQDN será similar a *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Abra **línea de comandos de Hadoop** de escritorio de Hola.
2. Ejecute hello después comandos tooopen SQLLine:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    comandos de Hola que se usan en el ejemplo hello:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Para más información, consulte el [manual de SQLLine](http://sqlline.sourceforge.net/#manual) y la [gramática de Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>Uso de SQuirreL
[Ardilla SQL Client](http://squirrel-sql.sourceforge.net/) es un programa Java gráfico que le permiten tooview estructura de Hola de una base de datos compatible con JDBC, examinar los datos de hello en tablas, emitir comandos SQL etcetera. Puede ser usado tooconnect tooApache Phoenix en HDInsight.

Esta sección muestra cómo tooinstall y configurar ardilla en su estación de trabajo tooconnect tooan clúster de HBase en HDInsight a través de VPN.

### <a name="prerequisites"></a>Requisitos previos
Antes de seguir los procedimientos de hello, debe tener el siguiente hello:

* Un clúster de HBase implementa tooan red virtual de Azure con una máquina virtual DNS.  Para obtener instrucciones, consulte [Creación de clústeres de HBase en Azure Virtual Network][hdinsight-hbase-provision-vnet].

* Obtiene el sufijo DNS específico de la conexión de hello HBase clúster clúster. tooget lo, RDP en clúster de hello, y, a continuación, ejecutar IPConfig.  sufijo DNS de Hello es similar a:

        myhbase.b7.internal.cloudapp.net
* Descargue e instale [Microsoft Visual Studio Express para escritorio de Windows](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) en la estación de trabajo. Necesitará makecert de hello paquete toocreate su certificado.  
* Descargue e instale [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) en su estación de trabajo.  La versión de cliente SQL SQuirreL 3.0 y superiores requieren la versión 1.6 o superior de JRE.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Configurar una toohello de conexión de Point-to-Site VPN red virtual de Azure
Hay tres pasos implicados en la configuración de una conexión VPN de punto a sitio:

1. [Configuración de una red virtual y una puerta de enlace de enrutamiento dinámico](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Creación de certificados](#Create-your-certificates)
3. [Configuración del cliente VPN](#Configure-your-VPN-client)

Vea [configurar una tooan de conexión de Point-to-Site VPN red Virtual de Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obtener más información.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Configuración de una red virtual y una puerta de enlace de enrutamiento dinámico
Asegurarse de haber aprovisionado un clúster de HBase en una red virtual de Azure (consulte requisitos previos de Hola de esta sección). Hola siguiente paso es tooconfigure una conexión punto a sitio.

**conectividad de punto a sitio hello tooconfigure**

1. Inicie sesión en toohello [Portal clásico de Azure][azure-portal].
2. Hola izquierda, haga clic en **redes**.
3. Haga clic en la red virtual de Hola que ha creado (consulte [HBase aprovisionar clústeres en la red Virtual de Azure][hdinsight-hbase-provision-vnet]).
4. Haga clic en **configurar** desde la parte superior de Hola.
5. Hola **conectividad punto a sitio** sección, seleccione **configurar la conectividad punto a sitio**.
6. Configurar **IP de inicio** y **CIDR** intervalo de direcciones IP toospecify Hola desde el que los clientes VPN recibirán una dirección IP de direcciones cuando se conecta. intervalo de Hello no puede solaparse con cualquiera de hello intervalos en sus instalaciones de red y Hola red virtual de Azure que se conectará a. Por ejemplo. Si seleccionó 10.0.0.0/20 para la red virtual de hello, puede seleccionar 10.1.0.0/24 de espacios de direcciones de cliente de Hola. Vea hello [conectividadpuntoasitiode] [ vnet-point-to-site-connectivity] página para obtener más información.
7. En la sección de espacios de direcciones de red virtual de hello, haga clic en **Agregar subred de puerta de enlace**.
8. Haga clic en **guardar** en parte inferior de Hola de página de Hola.
9. Haga clic en **Sí** cambio de hello tooconfirm. Espere hasta que Hola sistema haya terminado de realizar cambios antes de continuar el procedimiento siguiente toohello de Hola.

**toocreate una puerta de enlace de enrutamiento dinámico**

1. En hello Portal de Azure clásico, haga clic en **panel** de arriba Hola de página Hola.
2. Haga clic en **crear puerta de enlace** desde el final Hola Hola.
3. Haga clic en **Sí** tooconfirm. Espere hasta que se cree la puerta de enlace de Hola.
4. Haga clic en **panel** desde la parte superior de Hola.  Verá un diagrama visual de la red virtual de hello:

    ![Diagrama virtual de punto a sitio de red virtual de Azure][img-vnet-diagram]

    diagrama de Hello muestra 0 conexiones de cliente. Después de realizar una red virtual de toohello de conexión, el número de hello será tooone actualizada.

#### <a name="create-your-certificates"></a>Creación de certificados
Una manera de toocreate está usando un certificado X.509 Hola herramienta de creación de certificados (makecert.exe) que se incluye con [Microsoft Visual Studio Express para Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**toocreate un certificado raíz autofirmado**

1. Abra la ventana del símbolo del sistema desde la estación de trabajo.
2. Desplazarse por las carpetas de herramientas de Visual Studio toohello.
3. Hola siguiente comando en el siguiente ejemplo de Hola creará e instalar un certificado raíz en el almacén de certificados personales de hello en la estación de trabajo y crear un archivo .cer correspondiente más adelante cargará toohello Portal clásico de Azure.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Cambie el directorio de toohello que desea Hola toobe de archivo .cer ubicado en, donde HBaseVnetVPNRootCertificate es el nombre de Hola que deseas toouse certificado Hola.

    No cierre el símbolo del sistema Hola.  Lo necesitará en el procedimiento siguiente Hola.

   > [!NOTE]
   > Como ha creado un certificado de raíz desde el que se generará certificados de cliente, puede desea tooexport este certificado junto con su clave privada y guardarlo tooa ubicación segura donde se pueda recuperar.
   >
   >

**toocreate un certificado de cliente**

* De hello mismo símbolo (tiene toobe en hello mismo equipo donde se creó el certificado de raíz de Hola. certificado de cliente de Hello debe generarse de certificado de raíz de hello), ejecución hello comando siguiente:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate es el nombre de certificado de raíz de Hola.  Tiene el nombre del certificado de raíz de toomatch Hola.  

    Certificado de raíz de Hola y el certificado de cliente de Hola se almacenan en el almacén de certificados personales en el equipo. Utilice certmgr.msc tooverify.

    ![Certificado VPN de punto a sitio de red virtual de Azure][img-certificate]

    Un certificado de cliente debe instalarse en cada equipo que desea que la red virtual de tooconnect toohello. Le recomendamos que cree a cliente único certificados para cada equipo que desea que la red virtual de tooconnect toohello. los certificados de cliente hello tooexport, utilice certmgr.msc.

**tooupload Hola raíz certificado toohello Portal clásico de Azure**

1. En hello Portal de Azure clásico, haga clic en **red** de hello izquierda.
2. Haga clic en la red virtual de Hola donde se implementa el clúster de HBase en.
3. Haga clic en **certificados** desde la parte superior de Hola.
4. Haga clic en **cargar** de hello abajo y especifique el archivo de certificado raíz de hello ha creado en el procedimiento de hello penúltimo. Espere hasta que se obtuvo importar el certificado de Hola.
5. Haga clic en **panel** en la parte superior de Hola.  diagrama de Hello virtual muestra el estado de Hola.

#### <a name="configure-your-vpn-client"></a>Configuración del cliente VPN
**paquete de VPN de cliente hello toodownload e instalar**

1. Desde la página del panel Hola de red virtual de hello, en la sección de vista rápida de hello, haga clic en **descarga Hola paquete de VPN de cliente de 64 bits** o **descarga Hola paquete de VPN de cliente de 32 bits** en función de su versión de sistema operativo de la estación de trabajo.
2. Haga clic en **ejecutar** tooinstall paquetes de saludo.
3. En el símbolo del sistema de seguridad hello, haga clic en **obtener más información**y, a continuación, haga clic en **ejecutar de todas maneras**.
4. Haga clic en **Sí**

**tooconnect tooVPN**

1. En el escritorio de saludo de la estación de trabajo, haga clic en el icono de redes de hello en la barra de tareas de Hola. Verá una conexión VPN con el nombre de red virtual.
2. Haga clic en el nombre de la conexión VPN Hola.
3. Haga clic en **Conectar**.

**Hola tootest resolución de nombres de dominio y de conexión VPN**

* Desde la estación de trabajo de hello, abra un símbolo del sistema y ping de hello siguiendo los nombres de sufijo DNS del clúster de HBase hello es myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Instalación y configuración de SQuirreL en su estación de trabajo
**tooinstall ardilla**

1. Descargar archivo de hello ardilla SQL cliente jar de [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Archivo jar de hello abrir o ejecutar. Requiere hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Haga clic en **Siguiente** dos veces.
4. Especifique una ruta de acceso donde haya Hola permiso de escritura y, a continuación, haga clic en **siguiente**.

  > [!NOTE]
  > carpeta de instalación predeterminada de Hello está en la carpeta C:\Program Files\squirrel-sql-3.6 de Hola.  En orden toowrite toothis ruta de acceso instalador Hola debe tener privilegios de administrador de Hola. Puede abrir un símbolo del sistema como administrador, desplazarse por las carpetas de la Papelera de tooJava y, a continuación, ejecute:
  >
  >     Java.exe-jar [ruta de acceso de hello del archivo jar de hello ardilla]
5. Haga clic en **Aceptar** tooconfirm crear el directorio de destino de Hola.
6. saludo predeterminado es tooinstall Hola Base y los paquetes estándares.  Haga clic en **Siguiente**.
7. Haga clic en **Siguiente** dos veces y, a continuación, en **Hecho**.

**controlador de Phoenix hello tooinstall**

archivo jar de Hello phoenix controlador se encuentra en clúster de HBase Hola. ruta de acceso de Hello es similar toohello siguiente basados en versiones de hello:

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Necesita toocopy, estación de trabajo de tooyour en hello [carpeta de instalación de ardilla] / ruta de acceso de lib.  Hello más sencillo es tooRDP en clúster de hello y, a continuación, utilice Copiar y pegar (CTRL+C y CTRL+V) toocopy del archivo se tooyour estación de trabajo.

**tooadd un tooSQuirreL de controlador de Phoenix**

1. Abra el cliente SQL SQuirreL desde la estación de trabajo.
2. Haga clic en hello **controlador** ficha Hola izquierda.
3. De hello **controladores** menú, haga clic en **nuevo controlador**.
4. Escriba Hola siguiente información:

   * **Nombre**: Phoenix
   * **Dirección URL de ejemplo**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Nombre de la clase**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Usuario todas las minúsculas en la dirección URL de ejemplo de Hola. Puede usar el cuórum de zookeeper completo en caso de que uno de ellos esté inactivo.  los nombres de host de Hello son zookeeper0, zookeeper1 y zookeeper2.
     >
     >

     ![Controlador SQuirreL de HBase Phoenix para HDInsight][img-squirrel-driver]
5. Haga clic en **Aceptar**.

**toocreate un clúster de HBase de toohello de alias**

1. En ardilla, haga clic en hello **alias** ficha Hola izquierda.
2. De hello **alias** menú, haga clic en **nuevo Alias**.
3. Escriba Hola siguiente información:

   * **Nombre**: nombre de Hola de clúster de HBase de Hola o cualquier nombre que prefiera.
   * **Controlador**: Phoenix.  Esto debe coincidir con el nombre del controlador de Hola que creó en el último procedimiento de Hola.
   * **Dirección URL**: Hola se copia la dirección URL de la configuración del controlador. Poner en toouser seguro todas las minúsculas.
   * **Nombre de usuario**: puede ser cualquier texto.  Dado que usa aquí conectividad VPN, nombre de usuario de hello no se utiliza en absoluto.
   * **Contraseña**: puede ser cualquier texto.

     ![Controlador SQuirreL de HBase Phoenix para HDInsight][img-squirrel-alias]
4. Haga clic en **Probar**.
5. Haga clic en **Conectar**. Cuando realiza la conexión de hello, ardilla tendrá este aspecto:

    ![SQuirreL de Phoenix HBase][img-squirrel]

**toorun una prueba**

1. Haga clic en hello **SQL** pestaña derecha siguiente toohello **objetos** ficha.
2. Copie y pegue el siguiente código de hello:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Haga clic en el botón de ejecución de Hola.

    ![SQuirreL de Phoenix HBase][img-squirrel-sql]
4. Cambiar atrás toohello **objetos** ficha.
5. Expanda el nombre de alias de hello y, a continuación, expanda **tabla**.  Verá la nueva tabla de hello aparecen en.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo toouse Phoenix Apache en HDInsight.  toolearn más información, vea

* [Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.
* [Aprovisionar clústeres de HBase en red Virtual de Azure][hdinsight-hbase-provision-vnet]: con la integración de red virtual, clústeres de HBase pueden ser implementado toohello mismo virtual de red así como las aplicaciones que las aplicaciones pueden comunicarse con HBase directamente.
* [Configurar la replicación de HBase en HDInsight](hdinsight-hbase-replication.md): Obtenga información acerca de cómo tooconfigure HBase replicación entre dos centros de datos de Azure.
* [Analizar la opinión de Twitter con HBase en HDInsight][hbase-twitter-sentiment]: Obtenga información acerca de cómo toodo en tiempo real [análisis de opiniones](http://en.wikipedia.org/wiki/Sentiment_analysis) de grandes cantidades de datos mediante el uso de HBase en un clúster de Hadoop en HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
