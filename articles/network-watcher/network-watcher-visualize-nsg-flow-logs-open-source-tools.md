---
title: "registros de aaaVisualize flujo NSG de Monitor de red de Azure con herramientas de código abierto | Documentos de Microsoft"
description: "Esta página describe cómo toouse abrir registros de flujo de origen herramientas toovisualize NSG."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Visualización de registros de flujo de grupo de seguridad de red de Azure Network Watcher con herramientas de código abierto

Los registros de flujo de grupo de seguridad de red proporcionan información que sirve para comprender el tráfico IP de entrada y salida en grupos de seguridad de red. Estos registros de flujo muestran salientes y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, información de tupla 5 acerca del flujo de hello (origen/destino IP, puerto de origen/destino, protocolo), y si el tráfico de Hola se permitirá o denegará.

Estos registros de flujo pueden ser difícil toomanually análisis y obtener información de. Sin embargo, hay varias herramientas de código abierto que pueden ayudar a visualizar estos datos. Este artículo proporcionará una solución toovisualize estos registros mediante Hola pila elástica, que le permiten tooquickly índice y visualizar los registros de flujo en un panel de Kibana.

## <a name="scenario"></a>Escenario

En este artículo, se configurará una solución que le permitirá registros de flujo de grupo de seguridad de red toovisualize con hello pila elástico.  Un complemento de entrada Logstash obtendrá los registros de flujo de hello directamente desde el blob de almacenamiento de hello configurado para que contenga los registros de flujo de Hola. A continuación, con hello pila elástica, se indizarán y utilizan toocreate una información de hello toovisualize del panel de Kibana de registros de flujo de Hola.

![escenario][scenario]

## <a name="steps"></a>Pasos

### <a name="enable-network-security-group-flow-logging"></a>Habilitación de los registros de flujo de grupo de seguridad de red
En este escenario, debe tener el registro de flujo de grupo de seguridad de red habilitado en al menos un grupo de seguridad de red de su cuenta. Para obtener instrucciones acerca de cómo habilitar los registros de flujo de seguridad de red, consulte toohello artículo siguiente [registro tooflow de introducción para grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Configurar Hola pila elástica
Mediante la conexión NSG flujo registros con hello pila elástica, podemos crear un panel de Kibana lo que nos permite toosearch, gráfico, analizar y obtener la percepción de nuestros registros.

#### <a name="install-elasticsearch"></a>Instalación de Elasticsearch

1. Hola pila elástico desde la versión 5.0 y versiones posteriores requiere Java 8. Ejecute el comando de hello `java -version` toocheck su versión. Si no tiene java de instalación, consulte toodocumentation en [sitio Web de Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Descargue el paquete binario correcto de hello para el sistema:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Puede encontrar otros métodos de instalación en [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Instalación de Elasticsearch).

1. Compruebe que se está ejecutando con el comando Hola Elasticsearch:

    ```
    curl http://127.0.0.1:9200
    ```

    Debería ver un toothis similar de respuesta:

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Para obtener más instrucciones sobre instalación búsqueda elástica, consulte toohello página [instalación](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Instalación de Logstash

1. tooinstall Logstash ejecute hello siguientes comandos:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. A continuación se necesita tooconfigure Logstash tooaccess y analicen los registros de flujo de Hola. Cree un archivo logstash.conf mediante:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Agregue hello toohello contenido el archivo siguiente:

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Para obtener más instrucciones acerca de cómo instalar Logstash, consulte toohello [documentación oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Instalar el complemento de entrada de Logstash hello para el almacenamiento de blobs de Azure

Este complemento Logstash le permitirá los registros de flujo Hola acceso toodirectly desde su cuenta de almacenamiento designadas. tooinstall este complemento, desde el directorio de instalación predeterminado de hello Logstash (en este caso /usr/share/logstash/bin) ejecute hello comando:

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash ejecutar comando hello:

```
sudo /etc/init.d/logstash start
```

Para obtener más información sobre este complemento, consulte toodocumentation [aquí](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

### <a name="install-kibana"></a>Instalación de Kibana

1. Ejecute hello después comandos tooinstall Kibana:

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. toorun Kibana use comandos de hello:

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. tooview web Kibana interfaz, vaya demasiado`http://localhost:5601`
1. En este escenario, el patrón de índice de hello utilizado para los registros de flujo de hello es "registros de flujo de nsg". Puede cambiar el patrón de índice de hello en la sección de "resultado" hello del archivo logstash.conf.

1. Si desea Kibana panel de tooview Hola remotamente, cree una regla de NSG entrada permitir el acceso demasiado**puerto 5601**.

### <a name="create-a-kibana-dashboard"></a>Creación de un panel de Kibana

Para este artículo, proporcionamos un panel de ejemplo para que tooview tendencias y los detalles de las alertas.

![Figura 1][1]

1. Descargar archivo de panel de hello [aquí](https://aka.ms/networkwatchernsgflowlogdashboard), archivo de visualización de hello [aquí](https://aka.ms/networkwatchernsgflowlogvisualizations)y el archivo de búsqueda de hello guarda [aquí](https://aka.ms/networkwatchernsgflowlogsearch).

1. En hello **administración** ficha de Kibana, navegue demasiado**objetos guardados** e importar los tres archivos. A continuación en hello **panel** ficha puede abrir y carga Hola panel de ejemplo.

También puede crear visualizaciones y paneles propios que se adapten a las métricas que le interesen. Puede leer más sobre la creación de visualizaciones de Kibana en la [documentación oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana.

### <a name="visualize-nsg-flow-logs"></a>Visualización de registros de flujo de grupo de seguridad de red

panel de ejemplo de Hola proporciona varias visualizaciones de registros de flujo de hello:

1. Los flujos por decisión/dirección de un período - gráficos de series de tiempo que muestra el número de Hola de flujos en hello período de tiempo. Puede editar unidad Hola de tiempo y tramo de ambos estas visualizaciones. Flujos por decisión muestra hello proporción de permiten o denegación las decisiones tomadas, mientras que fluye por dirección muestra hello proporción de tráfico entrante y saliente. Con estos objetos visuales, puede examinar las tendencias del tráfico a lo largo del tiempo y buscar picos o patrones poco habituales.

  ![Figura 2][2]

1. Flujos de puerto de origen/destino: gráficos circulares que desglosan Hola flujos tootheir respectivos puertos. En esta vista se ven los puertos de uso más frecuente. Si hace clic en un puerto específico dentro de un gráfico circular hello, rest Hola de panel de hello filtrará hacia abajo tooflows de ese puerto.

  ![Figura 3][3]

1. Número de flujos y la hora de registro más antiguo: métricas muestran qué Hola número de flujos que se registraron y fecha de Hola de registro más antiguo de hello capturado.

  ![Figura 4][4]

1. Flujos de NSG y regla: un gráfico de barras que muestra la distribución de Hola de flujos dentro de cada NSG, así como la distribución de Hola de reglas en cada NSG. Desde aquí puede ver qué NSG y las reglas que genera Hola mayor cantidad de tráfico.

  ![Figura 5][5]

1. Top 10 origen/destino IP: gráficos de barras que muestra hello 10 mejores origen e IP de destino. Puede ajustar estos tooshow gráficos más o menos superior direcciones IP. Desde aquí puede vea Hola normalmente está produciendo direcciones IP, así como Hola decisión de tráfico (permitir o denegar) que se va a realizar en cada IP.

  ![Figura 6][6]

1. Tuplas de flujo: esta tabla muestra Hola información contenida en cada tupla flujo, así como sus NGS correspondiente y la regla.

  ![Figura 7][7]

Using barra de consulta de Hola Hola principio del panel de hello, puede filtrar hacia abajo el panel de hello basado en cualquier parámetro de flujos de hello, por ejemplo, Id. de suscripción, grupos de recursos, regla o cualquier otra variable de interés. Para obtener más información sobre las consultas y los filtros del Kibana, consulte toohello [documentación oficial](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Conclusión

Mediante la combinación de registros de flujo de grupo de seguridad de red de hello con hello pila elástica, hemos creado con toovisualize de forma eficaz y puede personalizar el tráfico de red. Estos paneles permiten ganancia tooquickly y compartan información sobre el tráfico de red, así como filtro hacia abajo e investigar en cualquier posibles anomalías. Kibana puede personalizar estos paneles y crear visualizaciones específico toomeet las necesidades de seguridad, cumplimiento y auditoría.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
