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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="3d9e9-103">Visualización de registros de flujo de grupo de seguridad de red de Azure Network Watcher con herramientas de código abierto</span><span class="sxs-lookup"><span data-stu-id="3d9e9-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="3d9e9-104">Los registros de flujo de grupo de seguridad de red proporcionan información que sirve para comprender el tráfico IP de entrada y salida en grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="3d9e9-105">Estos registros de flujo muestran salientes y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, información de tupla 5 acerca del flujo de hello (origen/destino IP, puerto de origen/destino, protocolo), y si el tráfico de Hola se permitirá o denegará.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="3d9e9-106">Estos registros de flujo pueden ser difícil toomanually análisis y obtener información de.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="3d9e9-107">Sin embargo, hay varias herramientas de código abierto que pueden ayudar a visualizar estos datos.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="3d9e9-108">Este artículo proporcionará una solución toovisualize estos registros mediante Hola pila elástica, que le permiten tooquickly índice y visualizar los registros de flujo en un panel de Kibana.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="3d9e9-109">Escenario</span><span class="sxs-lookup"><span data-stu-id="3d9e9-109">Scenario</span></span>

<span data-ttu-id="3d9e9-110">En este artículo, se configurará una solución que le permitirá registros de flujo de grupo de seguridad de red toovisualize con hello pila elástico.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="3d9e9-111">Un complemento de entrada Logstash obtendrá los registros de flujo de hello directamente desde el blob de almacenamiento de hello configurado para que contenga los registros de flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="3d9e9-112">A continuación, con hello pila elástica, se indizarán y utilizan toocreate una información de hello toovisualize del panel de Kibana de registros de flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![escenario][scenario]

## <a name="steps"></a><span data-ttu-id="3d9e9-114">Pasos</span><span class="sxs-lookup"><span data-stu-id="3d9e9-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="3d9e9-115">Habilitación de los registros de flujo de grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="3d9e9-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="3d9e9-116">En este escenario, debe tener el registro de flujo de grupo de seguridad de red habilitado en al menos un grupo de seguridad de red de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="3d9e9-117">Para obtener instrucciones acerca de cómo habilitar los registros de flujo de seguridad de red, consulte toohello artículo siguiente [registro tooflow de introducción para grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d9e9-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="3d9e9-118">Configurar Hola pila elástica</span><span class="sxs-lookup"><span data-stu-id="3d9e9-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="3d9e9-119">Mediante la conexión NSG flujo registros con hello pila elástica, podemos crear un panel de Kibana lo que nos permite toosearch, gráfico, analizar y obtener la percepción de nuestros registros.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="3d9e9-120">Instalación de Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="3d9e9-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="3d9e9-121">Hola pila elástico desde la versión 5.0 y versiones posteriores requiere Java 8.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="3d9e9-122">Ejecute el comando de hello `java -version` toocheck su versión.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="3d9e9-123">Si no tiene java de instalación, consulte toodocumentation en [sitio Web de Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="3d9e9-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="3d9e9-124">Descargue el paquete binario correcto de hello para el sistema:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="3d9e9-125">Puede encontrar otros métodos de instalación en [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Instalación de Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="3d9e9-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="3d9e9-126">Compruebe que se está ejecutando con el comando Hola Elasticsearch:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="3d9e9-127">Debería ver un toothis similar de respuesta:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="3d9e9-128">Para obtener más instrucciones sobre instalación búsqueda elástica, consulte toohello página [instalación](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="3d9e9-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="3d9e9-129">Instalación de Logstash</span><span class="sxs-lookup"><span data-stu-id="3d9e9-129">Install Logstash</span></span>

1. <span data-ttu-id="3d9e9-130">tooinstall Logstash ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="3d9e9-131">A continuación se necesita tooconfigure Logstash tooaccess y analicen los registros de flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="3d9e9-132">Cree un archivo logstash.conf mediante:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="3d9e9-133">Agregue hello toohello contenido el archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="3d9e9-134">Para obtener más instrucciones acerca de cómo instalar Logstash, consulte toohello [documentación oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="3d9e9-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="3d9e9-135">Instalar el complemento de entrada de Logstash hello para el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="3d9e9-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="3d9e9-136">Este complemento Logstash le permitirá los registros de flujo Hola acceso toodirectly desde su cuenta de almacenamiento designadas.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="3d9e9-137">tooinstall este complemento, desde el directorio de instalación predeterminado de hello Logstash (en este caso /usr/share/logstash/bin) ejecute hello comando:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="3d9e9-138">toostart Logstash ejecutar comando hello:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="3d9e9-139">Para obtener más información sobre este complemento, consulte toodocumentation [aquí](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="3d9e9-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="3d9e9-140">Instalación de Kibana</span><span class="sxs-lookup"><span data-stu-id="3d9e9-140">Install Kibana</span></span>

1. <span data-ttu-id="3d9e9-141">Ejecute hello después comandos tooinstall Kibana:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="3d9e9-142">toorun Kibana use comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="3d9e9-143">tooview web Kibana interfaz, vaya demasiado`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="3d9e9-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="3d9e9-144">En este escenario, el patrón de índice de hello utilizado para los registros de flujo de hello es "registros de flujo de nsg".</span><span class="sxs-lookup"><span data-stu-id="3d9e9-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="3d9e9-145">Puede cambiar el patrón de índice de hello en la sección de "resultado" hello del archivo logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="3d9e9-146">Si desea Kibana panel de tooview Hola remotamente, cree una regla de NSG entrada permitir el acceso demasiado**puerto 5601**.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="3d9e9-147">Creación de un panel de Kibana</span><span class="sxs-lookup"><span data-stu-id="3d9e9-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="3d9e9-148">Para este artículo, proporcionamos un panel de ejemplo para que tooview tendencias y los detalles de las alertas.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![Figura 1][1]

1. <span data-ttu-id="3d9e9-150">Descargar archivo de panel de hello [aquí](https://aka.ms/networkwatchernsgflowlogdashboard), archivo de visualización de hello [aquí](https://aka.ms/networkwatchernsgflowlogvisualizations)y el archivo de búsqueda de hello guarda [aquí](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="3d9e9-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="3d9e9-151">En hello **administración** ficha de Kibana, navegue demasiado**objetos guardados** e importar los tres archivos.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="3d9e9-152">A continuación en hello **panel** ficha puede abrir y carga Hola panel de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="3d9e9-153">También puede crear visualizaciones y paneles propios que se adapten a las métricas que le interesen.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="3d9e9-154">Puede leer más sobre la creación de visualizaciones de Kibana en la [documentación oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="3d9e9-155">Visualización de registros de flujo de grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="3d9e9-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="3d9e9-156">panel de ejemplo de Hola proporciona varias visualizaciones de registros de flujo de hello:</span><span class="sxs-lookup"><span data-stu-id="3d9e9-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="3d9e9-157">Los flujos por decisión/dirección de un período - gráficos de series de tiempo que muestra el número de Hola de flujos en hello período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="3d9e9-158">Puede editar unidad Hola de tiempo y tramo de ambos estas visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="3d9e9-159">Flujos por decisión muestra hello proporción de permiten o denegación las decisiones tomadas, mientras que fluye por dirección muestra hello proporción de tráfico entrante y saliente.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="3d9e9-160">Con estos objetos visuales, puede examinar las tendencias del tráfico a lo largo del tiempo y buscar picos o patrones poco habituales.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Figura 2][2]

1. <span data-ttu-id="3d9e9-162">Flujos de puerto de origen/destino: gráficos circulares que desglosan Hola flujos tootheir respectivos puertos.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="3d9e9-163">En esta vista se ven los puertos de uso más frecuente.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="3d9e9-164">Si hace clic en un puerto específico dentro de un gráfico circular hello, rest Hola de panel de hello filtrará hacia abajo tooflows de ese puerto.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![Figura 3][3]

1. <span data-ttu-id="3d9e9-166">Número de flujos y la hora de registro más antiguo: métricas muestran qué Hola número de flujos que se registraron y fecha de Hola de registro más antiguo de hello capturado.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![Figura 4][4]

1. <span data-ttu-id="3d9e9-168">Flujos de NSG y regla: un gráfico de barras que muestra la distribución de Hola de flujos dentro de cada NSG, así como la distribución de Hola de reglas en cada NSG.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="3d9e9-169">Desde aquí puede ver qué NSG y las reglas que genera Hola mayor cantidad de tráfico.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![Figura 5][5]

1. <span data-ttu-id="3d9e9-171">Top 10 origen/destino IP: gráficos de barras que muestra hello 10 mejores origen e IP de destino.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="3d9e9-172">Puede ajustar estos tooshow gráficos más o menos superior direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="3d9e9-173">Desde aquí puede vea Hola normalmente está produciendo direcciones IP, así como Hola decisión de tráfico (permitir o denegar) que se va a realizar en cada IP.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![Figura 6][6]

1. <span data-ttu-id="3d9e9-175">Tuplas de flujo: esta tabla muestra Hola información contenida en cada tupla flujo, así como sus NGS correspondiente y la regla.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![Figura 7][7]

<span data-ttu-id="3d9e9-177">Using barra de consulta de Hola Hola principio del panel de hello, puede filtrar hacia abajo el panel de hello basado en cualquier parámetro de flujos de hello, por ejemplo, Id. de suscripción, grupos de recursos, regla o cualquier otra variable de interés.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="3d9e9-178">Para obtener más información sobre las consultas y los filtros del Kibana, consulte toohello [documentación oficial](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="3d9e9-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="3d9e9-179">Conclusión</span><span class="sxs-lookup"><span data-stu-id="3d9e9-179">Conclusion</span></span>

<span data-ttu-id="3d9e9-180">Mediante la combinación de registros de flujo de grupo de seguridad de red de hello con hello pila elástica, hemos creado con toovisualize de forma eficaz y puede personalizar el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="3d9e9-181">Estos paneles permiten ganancia tooquickly y compartan información sobre el tráfico de red, así como filtro hacia abajo e investigar en cualquier posibles anomalías.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="3d9e9-182">Kibana puede personalizar estos paneles y crear visualizaciones específico toomeet las necesidades de seguridad, cumplimiento y auditoría.</span><span class="sxs-lookup"><span data-stu-id="3d9e9-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d9e9-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d9e9-183">Next steps</span></span>

<span data-ttu-id="3d9e9-184">Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3d9e9-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
