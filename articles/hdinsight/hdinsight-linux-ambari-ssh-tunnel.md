---
title: "aaaUse SSH túnel tooaccess HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse una toosecurely de túnel SSH examinar recursos de web hospedados en los nodos de HDInsight basados en Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>Usar la interfaz de usuario de tooaccess Ambari web túnel SSH, JobHistory, NameNode, Oozie y otra interfaces de usuario web

Clústeres de HDInsight basados en Linux proporcionan acceso tooAmbari interfaz de usuario web a través de Internet de hello, pero algunas características de interfaz de usuario de hello no están. Por ejemplo, hello interfaz de usuario web para otros servicios que se exponen a través de Ambari. Para todas las funcionalidades de la interfaz de usuario de web de hello Ambari, debe utilizar un encabezado de clúster de toohello de túnel SSH.

## <a name="why-use-an-ssh-tunnel"></a>¿Por qué usar un túnel SSH?

Algunos de los menús de hello en Ambari solo funcionan a través de un túnel SSH. Estos menús se basan en sitios web y servicios que se ejecutan en otros tipos de nodo, como nodos de trabajo. A menudo, estos sitios web no están protegidos, por lo que no es seguro toodirectly exponen Hola a ellos en internet.

Hola siguientes interfaces de usuario Web requiere un túnel SSH:

* Historial de trabajos
* NameNode
* Pilas de subprocesos
* Interfaz de usuario web de Oozie
* Interfaz de usuario de registros y maestro de HBase

Si utiliza acciones de Script toocustomize el clúster, todos los servicios o utilidades que se instalación que exponen una interfaz de usuario web requieren un túnel SSH. Por ejemplo, si instala matiz mediante una acción de secuencia de comandos, debe utilizar un SSH túnel tooaccess Hola matiz interfaz de usuario web.

> [!IMPORTANT]
> Si tiene acceso directo tooHDInsight a través de una red virtual, no es necesario toouse SSH túneles. Para obtener un ejemplo de obtener acceso directamente a HDInsight a través de una red virtual, vea hello [red local de HDInsight conectar tooyour](connect-on-premises-network.md) documento.

## <a name="what-is-an-ssh-tunnel"></a>¿Qué es un túnel SSH?

[Secure Shell (SSH) túnel](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) enruta el tráfico enviado tooa puerto en la estación de trabajo local. Hola tráfico se enruta a través de un SSH conexión tooyour HDInsight nodo principal del clúster. solicitud de saludo se resuelve como si se originó en el nodo principal de Hola. respuesta de Hello, a continuación, se enruta a través de estación de trabajo de hello túnel tooyour.

## <a name="prerequisites"></a>Requisitos previos

* Un cliente SSH. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Un explorador web que se puede configura un proxy SOCKS5 toouse.

    > [!WARNING]
    > compatibilidad de proxy SOCKS Hola integrada en Windows no admite SOCKS5 y no funciona con los pasos de hello en este documento. Hello exploradores siguientes se basan en la configuración de proxy de Windows y actualmente no realizar trabajo con pasos de hello en este documento:
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome también se basa en la configuración de proxy de Windows hello. Sin embargo, se pueden instalar extensiones que admiten SOCKS5. Se recomienda [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Crear un túnel con el comando de hello SSH

Comando de uso Hola siguiente toocreate un túnel SSH con hello `ssh` comando. Reemplace **nombre de usuario** con un usuario SSH para el clúster de HDInsight y reemplazar **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Este comando crea una conexión que enruta los clúster de tráfico toolocal puerto 9876 toohello mediante SSH. Hola opciones son:

* **D 9876** -Hola puerto local que enruta el tráfico a través de túnel de Hola.
* **C** : comprimir todos los datos, debido a que el tráfico web es principalmente texto.
* **2** -force SSH tootry versión 2 del protocolo solo.
* **q** : modo silencioso.
* **T** : deshabilitar la asignación seudotty, debido a que solo estamos desviando un puerto.
* **n** : evitar la lectura de STDIN, debido a que solo estamos desviando un puerto.
* **N** : no ejecutar un comando remoto, debido a que solo estamos desviando un puerto.
* **f** -ejecutar en segundo plano de Hola.

Una vez que finaliza el comando de hello, el tráfico enviado tooport 9876 en equipo local hello es toohello enrutado nodo principal del clúster.

## <a name="useputty"></a>Creación de un túnel mediante PuTTY

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) es un cliente SSH gráfico para Windows. Usar hello siguiendo los pasos toocreate un túnel SSH mediante PuTTY:

1. Abra PuTTY y escriba la información de conexión. Si no está familiarizado con PuTTY, vea hello [PuTTY documentación (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. Hola **categoría** toohello de la sección izquierda del cuadro de diálogo de hello, expanda **conexión**, expanda **SSH**y, a continuación, seleccione **túneles**.

3. Proporcionar Hola siguiente información en hello **reenvío de puerto de opciones que controlan SSH** formulario:
   
   * **Puerto de origen** -Hola puerto en el cliente de Hola que desea tooforward. Por ejemplo, **9876**.

   * **Destino** -Hola dirección SSH para clúster de HDInsight basados en Linux de Hola. Por ejemplo, **mycluster-ssh.azurehdinsight.net**.

   * **Dynamic** : habilita el enrutamiento dinámico del proxy SOCKS.
     
     ![imagen de las opciones de tunelización](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Haga clic en **agregar** tooadd Hola configuración y, a continuación, haga clic en **abiertos** tooopen una conexión SSH.

5. Cuando se le solicite, inicie sesión en el servidor de toohello.

## <a name="use-hello-tunnel-from-your-browser"></a>Usar túnel Hola desde el explorador

> [!IMPORTANT]
> Hola pasos de este Hola de uso de la sección explorador Mozilla FireFox, ya que proporciona Hola misma configuración de proxy para todas las plataformas. Otros exploradores modernos, como Google Chrome, pueden requerir una extensión como FoxyProxy toowork con túnel Hola.

1. Configurar Hola explorador toouse **localhost** y puerto de Hola que ha utilizado al crear túnel Hola como un **SOCKS v5** proxy. Este es el aspecto de configuración de Firefox Hola. Si utiliza un puerto diferente 9876, cambiar hello toohello de puerto que utiliza:
   
    ![imagen de la configuración de Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > Seleccionar **DNS remoto** resuelve las solicitudes de sistema de nombres de dominio (DNS) mediante el uso de clúster de HDInsight Hola. Esta configuración resuelve DNS con la del nodo principal del clúster de Hola Hola.

2. Compruebe que túnel Hola funciona al visitar un sitio como [http://www.whatismyip.com/](http://www.whatismyip.com/). Hola IP devuelve uno se utilizará en centros de datos de Microsoft Azure Hola.

## <a name="verify-with-ambari-web-ui"></a>Compruebe con la interfaz de usuario web de Ambari

Una vez que se ha establecido el clúster de hello, utilice Hola después tooverify de pasos que puede tener acceso a interfaces de usuario web del servicio de hello Ambari Web:

1. En el explorador, vaya toohttp://headnodehost:8080. Hola `headnodehost` dirección se envía a través de clústeres de toohello de túnel de Hola y resolver el nodo principal de toohello Ambari se ejecuta en. Cuando se le solicite, escriba el nombre de usuario de administrador de hello (admin) y la contraseña para el clúster. Se le pedirá una segunda vez mediante la interfaz de usuario de web de hello Ambari. Si es así, vuelva a especificar información de Hola.

   > [!NOTE]
   > Cuando utiliza hello http://headnodehost:8080 dirección tooconnect toohello clúster, se conecta a través de túnel de Hola. La comunicación está protegida mediante túnel SSH de hello en lugar de HTTPS. tooconnect más Hola a internet a través de HTTPS, use https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre del clúster de Hola.

2. En hello Ambari Web UI, seleccione HDFS en lista de hello de la izquierda de Hola de página de Hola.

    ![Imagen con HDFS seleccionado](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Cuando se muestra la información del servicio HDFS hello, seleccione **vínculos rápidos**. Aparece una lista de nodos principales del clúster Hola. Seleccione uno de los nodos principales de hello y, a continuación, seleccione **NameNode UI**.

    ![Imagen con menú de vínculos rápidos de hello expandido](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Al seleccionar __Vínculos rápidos__, es posible que obtenga un indicador de espera. Esta condición puede ocurrir si tiene una conexión lenta a Internet. Espere un minuto o dos para hello datos toobe recibido del servidor de hello, vuelva a intentarlo lista Hola.
   >
   > Algunas entradas de hello **vínculos rápidos** menú puede quedar cortado por hello derecha de la pantalla de bienvenida. Si es así, expanda menú hello mediante el mouse y utilice Hola flecha derecha tooscroll clave Hola pantalla toohello toosee derecho Hola resto del menú de Hola.

4. Se muestra un toohello similar de página después de la imagen:

    ![Imagen de hello NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Observe la dirección URL de Hola para esta página; debe ser similar demasiado**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/clúster**. Este identificador URI está usando el nombre de dominio completo interno de hello (FQDN) del nodo de Hola y solo está disponible cuando se usa un túnel SSH.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toocreate y use un túnel SSH, vea Hola después de documento para otro toouse formas Ambari:

* [Administración de clústeres de HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md)

Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

