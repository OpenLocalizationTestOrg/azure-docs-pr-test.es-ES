---
title: "Visualización de registros de flujo de grupo de seguridad de red de Azure Network Watcher con herramientas de código abierto | Microsoft Docs"
description: "En esta página se describe cómo utilizar herramientas de código abierto para visualizar los registros de flujo de grupo de seguridad de red."
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
ms.openlocfilehash: 20f60ccd9108a7473705c2368f28d3152d0dd614
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="e5bca-103">Visualización de registros de flujo de grupo de seguridad de red de Azure Network Watcher con herramientas de código abierto</span><span class="sxs-lookup"><span data-stu-id="e5bca-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="e5bca-104">Los registros de flujo de grupo de seguridad de red proporcionan información que sirve para comprender el tráfico IP de entrada y salida en grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="e5bca-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="e5bca-105">Estos registros de flujo muestran los flujos de entrada y salida en función de cada regla, la NIC a la que se aplica el flujo, 5 datos sobre el flujo (IP de origen y de destino, puerto de origen y de destino, protocolo), y si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="e5bca-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="e5bca-106">El análisis y la extracción de información de forma manual de estos registros de flujo pueden resultar difíciles.</span><span class="sxs-lookup"><span data-stu-id="e5bca-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="e5bca-107">Sin embargo, hay varias herramientas de código abierto que pueden ayudar a visualizar estos datos.</span><span class="sxs-lookup"><span data-stu-id="e5bca-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="e5bca-108">En este artículo se proporciona una solución para visualizar estos registros mediante Elastic Stack, lo que le permitirá indexar y visualizar rápidamente el flujo de registros en un panel de Kibana.</span><span class="sxs-lookup"><span data-stu-id="e5bca-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="e5bca-109">Escenario</span><span class="sxs-lookup"><span data-stu-id="e5bca-109">Scenario</span></span>

<span data-ttu-id="e5bca-110">En este artículo, se configurará una solución que le permitirá visualizar registros de flujo de grupo de seguridad de red con Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="e5bca-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="e5bca-111">Un complemento de entrada de Logstash obtendrá los registros de flujo directamente del blob de almacenamiento configurado como contenedor de los registros de flujo.</span><span class="sxs-lookup"><span data-stu-id="e5bca-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="e5bca-112">A continuación, con Elastic Stack, se indexarán los registros de flujo y se usarán para crear un panel de Kibana para visualizar la información.</span><span class="sxs-lookup"><span data-stu-id="e5bca-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![escenario][scenario]

## <a name="steps"></a><span data-ttu-id="e5bca-114">Pasos</span><span class="sxs-lookup"><span data-stu-id="e5bca-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="e5bca-115">Habilitación de los registros de flujo de grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="e5bca-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="e5bca-116">En este escenario, debe tener el registro de flujo de grupo de seguridad de red habilitado en al menos un grupo de seguridad de red de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="e5bca-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="e5bca-117">Para ver instrucciones para habilitar los registros de flujo de grupo de seguridad de red, consulte el artículo siguiente [Introducción a los registros de flujo de grupos de seguridad de red con Azure Network Watcher](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5bca-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="e5bca-118">Configuración de Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="e5bca-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="e5bca-119">Mediante la conexión de los registros de flujo de grupo de seguridad con Elastic Stack, se puede crear un panel de Kibana que permita buscar, representar, analizar y extraer información de los registros.</span><span class="sxs-lookup"><span data-stu-id="e5bca-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="e5bca-120">Instalación de Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="e5bca-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="e5bca-121">La versión 5.0 y superiores de Elastic Stack requieren Java 8.</span><span class="sxs-lookup"><span data-stu-id="e5bca-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="e5bca-122">Ejecute el comando `java -version` para comprobar la versión.</span><span class="sxs-lookup"><span data-stu-id="e5bca-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="e5bca-123">Si no tiene instalado Java, consulte la documentación en el [sitio web de Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html).</span><span class="sxs-lookup"><span data-stu-id="e5bca-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="e5bca-124">Descargue el paquete binario correcto para su sistema:</span><span class="sxs-lookup"><span data-stu-id="e5bca-124">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="e5bca-125">Puede encontrar otros métodos de instalación en [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Instalación de Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="e5bca-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="e5bca-126">Compruebe que Elasticsearch se esté ejecutando con el comando:</span><span class="sxs-lookup"><span data-stu-id="e5bca-126">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="e5bca-127">La respuesta debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5bca-127">You should see a response similar to this:</span></span>

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

<span data-ttu-id="e5bca-128">Para más instrucciones sobre cómo instalar Elasticsearch, consulte la página de [instalación](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html).</span><span class="sxs-lookup"><span data-stu-id="e5bca-128">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="e5bca-129">Instalación de Logstash</span><span class="sxs-lookup"><span data-stu-id="e5bca-129">Install Logstash</span></span>

1. <span data-ttu-id="e5bca-130">Para instalar Logstash, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e5bca-130">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="e5bca-131">A continuación, necesitamos configurar Logstash para tener acceso a los registros de flujo y analizarlos.</span><span class="sxs-lookup"><span data-stu-id="e5bca-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="e5bca-132">Cree un archivo logstash.conf mediante:</span><span class="sxs-lookup"><span data-stu-id="e5bca-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="e5bca-133">Agregue el siguiente contenido al archivo:</span><span class="sxs-lookup"><span data-stu-id="e5bca-133">Add the following content to the file:</span></span>

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

<span data-ttu-id="e5bca-134">Para más instrucciones sobre cómo instalar Logstash, consulte la [documentación oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span><span class="sxs-lookup"><span data-stu-id="e5bca-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="e5bca-135">Instalación del complemento de entrada de Logstash para Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="e5bca-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="e5bca-136">Este complemento de Logstash le permitirá acceder directamente a los registros de flujo desde su cuenta de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="e5bca-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="e5bca-137">Para instalar este complemento, desde el directorio de instalación predeterminado de Logstash (en este caso /usr/share/logstash/bin), ejecute el comando:</span><span class="sxs-lookup"><span data-stu-id="e5bca-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="e5bca-138">Para iniciar Logstash, ejecute el comando:</span><span class="sxs-lookup"><span data-stu-id="e5bca-138">To start Logstash run the command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="e5bca-139">Para obtener más información sobre este complemento, consulte la documentación [aquí](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span><span class="sxs-lookup"><span data-stu-id="e5bca-139">For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="e5bca-140">Instalación de Kibana</span><span class="sxs-lookup"><span data-stu-id="e5bca-140">Install Kibana</span></span>

1. <span data-ttu-id="e5bca-141">Ejecute los siguientes comandos para instalar Kibana:</span><span class="sxs-lookup"><span data-stu-id="e5bca-141">Run the following commands to install Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="e5bca-142">Para ejecutar Kibana, use los comandos:</span><span class="sxs-lookup"><span data-stu-id="e5bca-142">To run Kibana use the commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="e5bca-143">Para ver la interfaz web de Kibana, vaya a `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="e5bca-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="e5bca-144">En este escenario, el patrón de índice usado para los registros de flujo es "nsg-flow-logs".</span><span class="sxs-lookup"><span data-stu-id="e5bca-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="e5bca-145">Puede cambiarlo en la sección "output" del archivo logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="e5bca-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="e5bca-146">Si quiere ver el panel de Kibana de forma remota, cree una regla de grupo de seguridad de red de entrada que permita acceder al **puerto 5601**.</span><span class="sxs-lookup"><span data-stu-id="e5bca-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="e5bca-147">Creación de un panel de Kibana</span><span class="sxs-lookup"><span data-stu-id="e5bca-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="e5bca-148">En este artículo, se proporciona un panel de ejemplo para que vea tendencias y detalles de sus alertas.</span><span class="sxs-lookup"><span data-stu-id="e5bca-148">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

![Figura 1][1]

1. <span data-ttu-id="e5bca-150">Descargue el archivo de panel de [aquí](https://aka.ms/networkwatchernsgflowlogdashboard), el archivo de visualización de [aquí](https://aka.ms/networkwatchernsgflowlogvisualizations) y el archivo de búsqueda guardada de [aquí](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="e5bca-150">Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="e5bca-151">En la pestaña **Management** (Administración) de Kibana, vaya a **Saved Objects** (Objetos guardados) e importe los tres archivos.</span><span class="sxs-lookup"><span data-stu-id="e5bca-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="e5bca-152">A continuación, en la pestaña **Dashboard** (Panel), puede abrir y cargar el panel de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e5bca-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="e5bca-153">También puede crear visualizaciones y paneles propios que se adapten a las métricas que le interesen.</span><span class="sxs-lookup"><span data-stu-id="e5bca-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="e5bca-154">Puede leer más sobre la creación de visualizaciones de Kibana en la [documentación oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana.</span><span class="sxs-lookup"><span data-stu-id="e5bca-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="e5bca-155">Visualización de registros de flujo de grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="e5bca-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="e5bca-156">El panel de ejemplo proporciona varias visualizaciones de los registros de flujo:</span><span class="sxs-lookup"><span data-stu-id="e5bca-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="e5bca-157">Flujos por decisión o dirección a lo largo del tiempo: gráficos de serie temporal que muestran el número de flujos en el período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e5bca-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="e5bca-158">Puede editar la unidad de tiempo y el alcance de estas dos visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="e5bca-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="e5bca-159">Flows by Decision (Flujos por decisión) muestra la proporción de decisiones de permitir o denegar tomadas, mientras que Flows by Direction (Flujos por dirección) muestra la proporción de tráfico de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="e5bca-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="e5bca-160">Con estos objetos visuales, puede examinar las tendencias del tráfico a lo largo del tiempo y buscar picos o patrones poco habituales.</span><span class="sxs-lookup"><span data-stu-id="e5bca-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Figura 2][2]

1. <span data-ttu-id="e5bca-162">Flujos por puerto de origen o destino (Flows by Destination Port y Flows by Source Port): gráficos circulares que muestran el desglose de los flujos a sus puertos respectivos.</span><span class="sxs-lookup"><span data-stu-id="e5bca-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="e5bca-163">En esta vista se ven los puertos de uso más frecuente.</span><span class="sxs-lookup"><span data-stu-id="e5bca-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="e5bca-164">Si hace clic en un puerto específico en el gráfico circular, el resto del panel se filtrará para mostrar flujos de ese puerto.</span><span class="sxs-lookup"><span data-stu-id="e5bca-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

  ![Figura 3][3]

1. <span data-ttu-id="e5bca-166">Number of Flows (Número de flujos) y Earliest Log Time (Hora de registro más antigua): métricas que muestran el número de flujos registrados y la fecha del registro más antiguo capturado.</span><span class="sxs-lookup"><span data-stu-id="e5bca-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

  ![Figura 4][4]

1. <span data-ttu-id="e5bca-168">Flows by NSG and Rule (Flujos por grupo de seguridad de red y regla): gráfico de barras que muestra la distribución de los flujos dentro de cada grupo de seguridad de red, así como la distribución de reglas en cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="e5bca-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="e5bca-169">Desde aquí puede ver qué grupo de seguridad de red y qué reglas generan la mayor parte del tráfico.</span><span class="sxs-lookup"><span data-stu-id="e5bca-169">From here you can see which NSG and rules generated the most traffic.</span></span>

  ![Figura 5][5]

1. <span data-ttu-id="e5bca-171">Diez principales IP de origen o destino (Top 10 Source IPs y Top 10 Destination IPs): gráficos de barras que muestran las diez principales direcciones IP de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="e5bca-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="e5bca-172">Puede ajustar estos gráficos para mostrar más o menos direcciones IP principales.</span><span class="sxs-lookup"><span data-stu-id="e5bca-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="e5bca-173">Desde aquí puede ver las direcciones IP más frecuentes, así como la decisión de tráfico (permitir o denegar) que se está tomando para cada IP.</span><span class="sxs-lookup"><span data-stu-id="e5bca-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

  ![Figura 6][6]

1. <span data-ttu-id="e5bca-175">Flow Tuples (Tuplas de flujo): en esta tabla se muestra la información contenida en cada tupla de flujo, así como su grupo de seguridad de red y regla correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e5bca-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![Figura 7][7]

<span data-ttu-id="e5bca-177">Mediante la barra de consulta en la parte superior del panel, puede filtrar el panel en función de cualquier parámetro de los flujos, como el id. de suscripción, los grupos de recursos, la regla o cualquier otra variable de interés.</span><span class="sxs-lookup"><span data-stu-id="e5bca-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="e5bca-178">Para más información sobre las consultas y los filtros de Kibana, consulte la [documentación oficial](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html).</span><span class="sxs-lookup"><span data-stu-id="e5bca-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="e5bca-179">Conclusión</span><span class="sxs-lookup"><span data-stu-id="e5bca-179">Conclusion</span></span>

<span data-ttu-id="e5bca-180">Al combinar los registros de flujo de grupo de seguridad de red con Elastic Stack, dispone de una forma eficaz y personalizable para visualizar el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="e5bca-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="e5bca-181">Estos paneles permiten obtener y compartir rápidamente información detallada sobre el tráfico de red, así como filtrar e investigar cualquier posible anomalía.</span><span class="sxs-lookup"><span data-stu-id="e5bca-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="e5bca-182">Con Kibana, puede personalizar estos paneles y crear visualizaciones específicas para satisfacer las necesidades de seguridad, cumplimiento y auditoría.</span><span class="sxs-lookup"><span data-stu-id="e5bca-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5bca-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5bca-183">Next steps</span></span>

<span data-ttu-id="e5bca-184">Aprenda a visualizar los registros de flujo de grupo de seguridad de red con Power BI en el artículo [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualización de registros de flujo de grupo de seguridad de red con Power BI).</span><span class="sxs-lookup"><span data-stu-id="e5bca-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
