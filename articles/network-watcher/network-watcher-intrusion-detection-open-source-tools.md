---
title: "Realización de detección de intrusiones en la red con Azure Network Watcher y herramientas de código abierto | Microsoft Docs"
description: "En este artículo se describe cómo usar Azure Network Watcher y las herramientas de código abierto para realizar la detección de intrusiones en la red."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 82d5e525859ebe03b152c63e4debbae469049c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="75e98-103">Realización de detección de intrusiones en la red con Azure Network Watcher y herramientas de código abierto</span><span class="sxs-lookup"><span data-stu-id="75e98-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="75e98-104">Las capturas de paquetes son un componente clave de la implementación de sistemas de detección de intrusiones de red (IDS) y de la ejecución de supervisión de seguridad de la red (NSM).</span><span class="sxs-lookup"><span data-stu-id="75e98-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="75e98-105">Existen varias herramientas IDS de código abierto que procesan las capturas de paquetes y buscan firmas de posibles intrusiones y actividad malintencionada.</span><span class="sxs-lookup"><span data-stu-id="75e98-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="75e98-106">Con las capturas de paquetes que proporciona Network Watcher, puede analizar la red en busca de intrusiones o vulnerabilidades de carácter dañino.</span><span class="sxs-lookup"><span data-stu-id="75e98-106">Using the packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="75e98-107">Una de esas herramientas de código abierto es Suricata, un motor de IDS que usa conjuntos de reglas para supervisar el tráfico de red y desencadenar alertas cuando se produce algún evento sospechoso.</span><span class="sxs-lookup"><span data-stu-id="75e98-107">One such open source tool is Suricata, an IDS engine that uses rulesets to monitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="75e98-108">Suricata ofrece un motor multiproceso, lo que significa que puede realizar el análisis del tráfico de red con una mayor velocidad y eficiencia.</span><span class="sxs-lookup"><span data-stu-id="75e98-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="75e98-109">Para más información sobre Suricata y sus funcionalidades, visite este sitio web en https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="75e98-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="75e98-110">Escenario</span><span class="sxs-lookup"><span data-stu-id="75e98-110">Scenario</span></span>

<span data-ttu-id="75e98-111">En este artículo se explica cómo configurar el entorno para realizar la detección de intrusiones de red con Network Watcher, Suricata y Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="75e98-111">This article explains how to set up your environment to perform network intrusion detection using Network Watcher, Suricata, and the Elastic Stack.</span></span> <span data-ttu-id="75e98-112">Network Watcher proporciona las capturas de paquetes usadas para realizar la detección de intrusiones de red.</span><span class="sxs-lookup"><span data-stu-id="75e98-112">Network Watcher provides you with the packet captures used to perform network intrusion detection.</span></span> <span data-ttu-id="75e98-113">Suricata procesa las capturas de paquetes y desencadena alertas en función de los paquetes que coinciden con su conjunto de reglas especificada de amenazas.</span><span class="sxs-lookup"><span data-stu-id="75e98-113">Suricata processes the packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="75e98-114">Estas alertas se almacenan en un archivo de registro en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="75e98-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="75e98-115">Con Elastic Stack, los registros que genera Suricata se pueden indexar y usar para crear un panel de Kibana. Este panel proporciona una representación visual de los registros y un medio de obtener rápidamente información detallada sobre posibles vulnerabilidades de la red.</span><span class="sxs-lookup"><span data-stu-id="75e98-115">Using the Elastic Stack, the logs generated by Suricata can be indexed and used to create a Kibana dashboard, providing you with a visual representation of the logs and a means to quickly gain insights to potential network vulnerabilities.</span></span>  

![escenario sencillo de aplicación web][1]

<span data-ttu-id="75e98-117">Ambas herramientas de código abierto se pueden configurar en una máquina virtual de Azure, lo que le permite realizar este análisis dentro de su propio entorno de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="75e98-117">Both open source tools can be set up on an Azure VM, allowing you to perform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="75e98-118">Pasos</span><span class="sxs-lookup"><span data-stu-id="75e98-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="75e98-119">Instalación de Suricata</span><span class="sxs-lookup"><span data-stu-id="75e98-119">Install Suricata</span></span>

<span data-ttu-id="75e98-120">Para más información sobre todos los demás métodos de instalación, visite http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="75e98-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="75e98-121">En el terminal de la línea de comandos de la máquina virtual, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="75e98-121">In the command-line terminal of your VM run the following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="75e98-122">Para comprobar la instalación, ejecute el comando `suricata -h` para ver la lista completa de comandos.</span><span class="sxs-lookup"><span data-stu-id="75e98-122">To verify your installation, run the command `suricata -h` to see the full list of commands.</span></span>

### <a name="download-the-emerging-threats-ruleset"></a><span data-ttu-id="75e98-123">Descarga del conjunto de reglas Emerging Threats</span><span class="sxs-lookup"><span data-stu-id="75e98-123">Download the Emerging Threats ruleset</span></span>

<span data-ttu-id="75e98-124">En esta fase, no tenemos ninguna regla para ejecutar con Suricata.</span><span class="sxs-lookup"><span data-stu-id="75e98-124">At this stage, we do not have any rules for Suricata to run.</span></span> <span data-ttu-id="75e98-125">Puede crear sus propias reglas si hay amenazas específicas para su red que quiera detectar, o también puede usar conjuntos de reglas desarrolladas por varios proveedores, como Emerging Threats o las reglas VRT de Snort.</span><span class="sxs-lookup"><span data-stu-id="75e98-125">You can create your own rules if there are specific threats to your network you would like to detect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="75e98-126">Aquí usaremos el conjunto de reglas de acceso gratuito Emerging Threats:</span><span class="sxs-lookup"><span data-stu-id="75e98-126">We use the freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="75e98-127">Descargue el conjunto de reglas y cópielo en el directorio:</span><span class="sxs-lookup"><span data-stu-id="75e98-127">Download the rule set and copy them into the directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="75e98-128">Procesamiento de las capturas de paquetes con Suricata</span><span class="sxs-lookup"><span data-stu-id="75e98-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="75e98-129">Para procesar las capturas de paquetes mediante Suricata, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="75e98-129">To process packet captures using Suricata, run the following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="75e98-130">Para comprobar las alertas resultantes, lea el archivo fast.log:</span><span class="sxs-lookup"><span data-stu-id="75e98-130">To check the resulting alerts, read the fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="75e98-131">Configuración de Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="75e98-131">Set up the Elastic Stack</span></span>

<span data-ttu-id="75e98-132">Si bien los registros que produce Suricata contienen información valiosa sobre lo que sucede en la red, estos archivos de registro no son los más fáciles de leer y comprender.</span><span class="sxs-lookup"><span data-stu-id="75e98-132">While the logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t the easiest to read and understand.</span></span> <span data-ttu-id="75e98-133">Mediante la conexión a Suricata con Elastic Stack, podemos crear un panel de Kibana que nos permita buscar, representar, analizar y deducir información de nuestros registros.</span><span class="sxs-lookup"><span data-stu-id="75e98-133">By connecting Suricata with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="75e98-134">Instalación de Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="75e98-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="75e98-135">La versión 5.0 y superiores de Elastic Stack requieren Java 8.</span><span class="sxs-lookup"><span data-stu-id="75e98-135">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="75e98-136">Ejecute el comando `java -version` para comprobar la versión.</span><span class="sxs-lookup"><span data-stu-id="75e98-136">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="75e98-137">Si no tiene instalado Java, consulte la documentación en el [sitio web de Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html).</span><span class="sxs-lookup"><span data-stu-id="75e98-137">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="75e98-138">Descargue el paquete binario correcto para su sistema:</span><span class="sxs-lookup"><span data-stu-id="75e98-138">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="75e98-139">Puede encontrar otros métodos de instalación en [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Instalación de Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="75e98-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="75e98-140">Compruebe que Elasticsearch se esté ejecutando con el comando:</span><span class="sxs-lookup"><span data-stu-id="75e98-140">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="75e98-141">La respuesta debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="75e98-141">You should see a response similar to this:</span></span>

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

<span data-ttu-id="75e98-142">Para más instrucciones sobre cómo instalar Elasticsearch, consulte la página de [instalación](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html).</span><span class="sxs-lookup"><span data-stu-id="75e98-142">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="75e98-143">Instalación de Logstash</span><span class="sxs-lookup"><span data-stu-id="75e98-143">Install Logstash</span></span>

1. <span data-ttu-id="75e98-144">Para instalar Logstash, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="75e98-144">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="75e98-145">A continuación, se debe configurar Logstash para que lea la salida del archivo eve.json.</span><span class="sxs-lookup"><span data-stu-id="75e98-145">Next we need to configure Logstash to read from the output of eve.json file.</span></span> <span data-ttu-id="75e98-146">Cree un archivo logstash.conf mediante:</span><span class="sxs-lookup"><span data-stu-id="75e98-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="75e98-147">Agregue el contenido siguiente al archivo (asegúrese de que la ruta de acceso al archivo eve.json sea correcta):</span><span class="sxs-lookup"><span data-stu-id="75e98-147">Add the following content to the file (make sure that the path to the eve.json file is correct):</span></span>

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. <span data-ttu-id="75e98-148">Asegúrese de conceder los permisos correctos para el archivo eve.json de modo que Logstash pueda ingerir el archivo.</span><span class="sxs-lookup"><span data-stu-id="75e98-148">Make sure to give the correct permissions to the eve.json file so that Logstash can ingest the file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="75e98-149">Para iniciar Logstash, ejecute el comando:</span><span class="sxs-lookup"><span data-stu-id="75e98-149">To start Logstash run the command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="75e98-150">Para obtener más instrucciones sobre cómo instalar Logstash, consulte la [documentación oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span><span class="sxs-lookup"><span data-stu-id="75e98-150">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="75e98-151">Instalación de Kibana</span><span class="sxs-lookup"><span data-stu-id="75e98-151">Install Kibana</span></span>

1. <span data-ttu-id="75e98-152">Ejecute los siguientes comandos para instalar Kibana:</span><span class="sxs-lookup"><span data-stu-id="75e98-152">Run the following commands to install Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="75e98-153">Para ejecutar Kibana, use los comandos:</span><span class="sxs-lookup"><span data-stu-id="75e98-153">To run Kibana use the commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="75e98-154">Para ver la interfaz web de Kibana, vaya a `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="75e98-154">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="75e98-155">En este escenario, el patrón de índice usado para los registros de Suricata es "logstash-*".</span><span class="sxs-lookup"><span data-stu-id="75e98-155">For this scenario, the index pattern used for the Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="75e98-156">Si quiere ver el panel de Kibana de forma remota, cree una regla NSG de entrada que permita acceder al **puerto 5601**.</span><span class="sxs-lookup"><span data-stu-id="75e98-156">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="75e98-157">Creación de un panel de Kibana</span><span class="sxs-lookup"><span data-stu-id="75e98-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="75e98-158">En este artículo, hemos proporcionado un panel de ejemplo para que vea las tendencias y los detalles de sus alertas.</span><span class="sxs-lookup"><span data-stu-id="75e98-158">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

1. <span data-ttu-id="75e98-159">Descargue el archivo de panel [aquí](https://aka.ms/networkwatchersuricatadashboard), el archivo de visualización [aquí](https://aka.ms/networkwatchersuricatavisualization) y el archivo de búsqueda guardado [aquí](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="75e98-159">Download the dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), the visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and the saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="75e98-160">En la pestaña **Management** (Administración) de Kibana, vaya a **Saved Objects** (Objetos guardados) e importe los tres archivos.</span><span class="sxs-lookup"><span data-stu-id="75e98-160">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="75e98-161">A continuación, en la pestaña **Dashboard** (Panel), puede abrir y cargar el panel de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="75e98-161">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="75e98-162">También puede crear visualizaciones y paneles propios que se adapten a las métricas que le interesen.</span><span class="sxs-lookup"><span data-stu-id="75e98-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="75e98-163">Puede leer más sobre la creación de visualizaciones de Kibana en la [documentación oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana.</span><span class="sxs-lookup"><span data-stu-id="75e98-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![panel de kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="75e98-165">Visualización de registros de alertas de IDS</span><span class="sxs-lookup"><span data-stu-id="75e98-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="75e98-166">El panel de ejemplo proporciona varias visualizaciones de los registros de alerta de Suricata:</span><span class="sxs-lookup"><span data-stu-id="75e98-166">The sample dashboard provides several visualizations of the Suricata alert logs:</span></span>

1. <span data-ttu-id="75e98-167">Alertas por GeoIP: mapa que muestra la distribución de las alertas por país de origen según la ubicación geográfica (determinada por la IP)</span><span class="sxs-lookup"><span data-stu-id="75e98-167">Alerts by GeoIP – a map showing the distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![ip geográfica][3]

1. <span data-ttu-id="75e98-169">10 alertas principales: resumen de las 10 alertas activadas más frecuentes y su descripción.</span><span class="sxs-lookup"><span data-stu-id="75e98-169">Top 10 Alerts – a summary of the 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="75e98-170">Al hacer clic en una alerta individual se filtra el panel por la información relacionada con esa alerta específica.</span><span class="sxs-lookup"><span data-stu-id="75e98-170">Clicking an individual alert filters down the dashboard to the information pertaining to that specific alert.</span></span>

    ![imagen 4][4]

1. <span data-ttu-id="75e98-172">Número de alertas: el número total de alertas activadas por el conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="75e98-172">Number of Alerts – the total count of alerts triggered by the ruleset</span></span>

    ![imagen 5][5]

1. <span data-ttu-id="75e98-174">20 puertos/direcciones IP de origen y destino principales: gráficos circulares que muestran los 20 puertos y direcciones IP principales en los que se activaron las alertas.</span><span class="sxs-lookup"><span data-stu-id="75e98-174">Top 20 Source/Destination IPs/Ports - pie charts showing the top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="75e98-175">Puede filtrar por direcciones IP o puertos específicos para ver cuántas alertas y de qué tipo se han activado.</span><span class="sxs-lookup"><span data-stu-id="75e98-175">You can filter down on specific IPs/ports to see how many and what kind of alerts are being triggered.</span></span>

    ![imagen 6][6]

1. <span data-ttu-id="75e98-177">Resumen de alertas: tabla que resume detalles específicos de cada alerta individual.</span><span class="sxs-lookup"><span data-stu-id="75e98-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="75e98-178">Puede personalizar esta tabla para mostrar otros parámetros de interés para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="75e98-178">You can customize this table to show other parameters of interest for each alert.</span></span>

    ![imagen 7][7]

<span data-ttu-id="75e98-180">Para ver más documentación sobre la creación de visualizaciones y paneles personalizados, consulte la [documentación oficial del Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="75e98-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="75e98-181">Conclusión</span><span class="sxs-lookup"><span data-stu-id="75e98-181">Conclusion</span></span>

<span data-ttu-id="75e98-182">Al combinar las capturas de paquetes proporcionadas por Network Watcher con herramientas IDS de código abierto como Suricata, puede realizar la detección de intrusiones para una amplia variedad de amenazas.</span><span class="sxs-lookup"><span data-stu-id="75e98-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="75e98-183">Estos paneles permiten detectar rápidamente tendencias y anomalías de la red, así como escarbar en los datos para descubrir las causas principales de las alertas, como agentes de usuario malintencionados o puertos vulnerables.</span><span class="sxs-lookup"><span data-stu-id="75e98-183">These dashboards allow you to quickly spot trends and anomalies within your network, as well dig into the data to discover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="75e98-184">Con estos datos extraídos, puede tomar decisiones fundamentadas sobre cómo proteger su red y reaccionar ante intentos de intrusión perjudiciales en ella, y crear reglas para impedir que sucedan tales situaciones.</span><span class="sxs-lookup"><span data-stu-id="75e98-184">With this extracted data, you can make informed decisions on how to react to and protect your network from any harmful intrusion attempts, and create rules to prevent future intrusions to your network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75e98-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75e98-185">Next steps</span></span>

<span data-ttu-id="75e98-186">Aprenda a desencadenar capturas de paquetes en función de alertas en el artículo [Uso de la captura de paquetes para realizar la supervisión proactiva de redes con Azure Functions](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="75e98-186">Learn how to trigger packet captures based on alerts by visiting [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="75e98-187">Aprenda a visualizar los registros de flujo de grupos de seguridad de red con Power BI en el artículo [Visualización de registros de flujo del grupo de seguridad de red de Azure con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="75e98-187">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
