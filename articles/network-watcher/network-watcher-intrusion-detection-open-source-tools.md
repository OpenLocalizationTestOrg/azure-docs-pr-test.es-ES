---
title: "aaaPerform la detección de intrusiones de red con Monitor de red de Azure y herramientas de código abierto | Documentos de Microsoft"
description: "Este artículo describe cómo toouse Monitor de red de Azure y código abierto herramientas tooperform la detección de intrusiones de red"
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
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="d10b0-103">Realización de detección de intrusiones en la red con Azure Network Watcher y herramientas de código abierto</span><span class="sxs-lookup"><span data-stu-id="d10b0-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="d10b0-104">Las capturas de paquetes son un componente clave de la implementación de sistemas de detección de intrusiones de red (IDS) y de la ejecución de supervisión de seguridad de la red (NSM).</span><span class="sxs-lookup"><span data-stu-id="d10b0-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="d10b0-105">Existen varias herramientas IDS de código abierto que procesan las capturas de paquetes y buscan firmas de posibles intrusiones y actividad malintencionada.</span><span class="sxs-lookup"><span data-stu-id="d10b0-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="d10b0-106">Con capturas de paquetes de saludo proporcionadas por el Monitor de red, puede analizar la red en busca de vulnerabilidades ni las intrusiones perjudiciales.</span><span class="sxs-lookup"><span data-stu-id="d10b0-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="d10b0-107">Una de estas herramientas de código abierto es Suricata, un motor de identificadores que usa el tráfico de red de rulesets toomonitor y desencadena alertas cuando se producen eventos sospechosos.</span><span class="sxs-lookup"><span data-stu-id="d10b0-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="d10b0-108">Suricata ofrece un motor multiproceso, lo que significa que puede realizar el análisis del tráfico de red con una mayor velocidad y eficiencia.</span><span class="sxs-lookup"><span data-stu-id="d10b0-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="d10b0-109">Para más información sobre Suricata y sus funcionalidades, visite este sitio web en https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="d10b0-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="d10b0-110">Escenario</span><span class="sxs-lookup"><span data-stu-id="d10b0-110">Scenario</span></span>

<span data-ttu-id="d10b0-111">Este artículo explica cómo tooset una tooperform de su entorno mediante el Monitor de red, Suricata, la detección de intrusiones de red y Hola pila elástico.</span><span class="sxs-lookup"><span data-stu-id="d10b0-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="d10b0-112">Monitor de red se proporciona con el paquete de saludo captura tooperform usa la detección de intrusiones de red.</span><span class="sxs-lookup"><span data-stu-id="d10b0-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="d10b0-113">Captura de paquetes de saludo de Suricata procesos y las alertas de desencadenador se basan en paquetes que coincidan con su conjunto de reglas determinado de amenazas.</span><span class="sxs-lookup"><span data-stu-id="d10b0-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="d10b0-114">Estas alertas se almacenan en un archivo de registro en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="d10b0-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="d10b0-115">Utilice Hola pila elástica, registros de hello generados por Suricata se pueden indizar y usan toocreate un panel de Kibana, le proporciona una representación visual de los registros de Hola y un vulnerabilidades de red significa tooquickly ganancia visión toopotential.</span><span class="sxs-lookup"><span data-stu-id="d10b0-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![escenario sencillo de aplicación web][1]

<span data-ttu-id="d10b0-117">Ambas herramientas de código abierto pueden configurarse en una máquina virtual de Azure, permitiéndole tooperform este análisis dentro de su propio entorno de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="d10b0-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="d10b0-118">Pasos</span><span class="sxs-lookup"><span data-stu-id="d10b0-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="d10b0-119">Instalación de Suricata</span><span class="sxs-lookup"><span data-stu-id="d10b0-119">Install Suricata</span></span>

<span data-ttu-id="d10b0-120">Para más información sobre todos los demás métodos de instalación, visite http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="d10b0-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="d10b0-121">En el terminal de línea de comandos de saludo de la máquina virtual ejecute Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="d10b0-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="d10b0-122">tooverify la instalación, ejecute el comando de hello `suricata -h` lista completa de hello toosee de comandos.</span><span class="sxs-lookup"><span data-stu-id="d10b0-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="d10b0-123">Descargar el conjunto de reglas de hello nuevas amenazas</span><span class="sxs-lookup"><span data-stu-id="d10b0-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="d10b0-124">En esta fase, no tenemos ninguna regla para Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="d10b0-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="d10b0-125">Puede crear sus propias reglas si hay amenazas específicas de red tooyour le gustaría toodetect o también puede conjuntos de reglas de uso desarrolladas desde un número de proveedores, como nuevas amenazas o reglas VRT de Snort.</span><span class="sxs-lookup"><span data-stu-id="d10b0-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="d10b0-126">Se utiliza el conjunto de reglas de hello libremente accesible nuevas amenazas aquí:</span><span class="sxs-lookup"><span data-stu-id="d10b0-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="d10b0-127">Descargar el conjunto de reglas de Hola y cópielos en el directorio de hello:</span><span class="sxs-lookup"><span data-stu-id="d10b0-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="d10b0-128">Procesamiento de las capturas de paquetes con Suricata</span><span class="sxs-lookup"><span data-stu-id="d10b0-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="d10b0-129">captura de paquetes de tooprocess con Suricata, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="d10b0-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="d10b0-130">toocheck Hola resultante alertas, leer el archivo de Hola fast.log:</span><span class="sxs-lookup"><span data-stu-id="d10b0-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="d10b0-131">Configurar Hola pila elástica</span><span class="sxs-lookup"><span data-stu-id="d10b0-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="d10b0-132">Mientras que los registros de Hola que genera Suricata contienen información valiosa acerca de lo que ocurre en nuestra red, estos archivos de registro no son tooread más fácil de Hola y entenderán.</span><span class="sxs-lookup"><span data-stu-id="d10b0-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="d10b0-133">Mediante la conexión Suricata con hello pila elástica, podemos crear un panel de Kibana lo que nos permite toosearch, gráfico, analizar y obtener la percepción de nuestros registros.</span><span class="sxs-lookup"><span data-stu-id="d10b0-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="d10b0-134">Instalación de Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="d10b0-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="d10b0-135">Hola pila elástico desde la versión 5.0 y versiones posteriores requiere Java 8.</span><span class="sxs-lookup"><span data-stu-id="d10b0-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="d10b0-136">Ejecute el comando de hello `java -version` toocheck su versión.</span><span class="sxs-lookup"><span data-stu-id="d10b0-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="d10b0-137">Si no tiene java de instalación, consulte toodocumentation en [sitio Web de Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="d10b0-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="d10b0-138">Descargue el paquete binario correcto de hello para el sistema:</span><span class="sxs-lookup"><span data-stu-id="d10b0-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="d10b0-139">Puede encontrar otros métodos de instalación en [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Instalación de Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="d10b0-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="d10b0-140">Compruebe que se está ejecutando con el comando Hola Elasticsearch:</span><span class="sxs-lookup"><span data-stu-id="d10b0-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="d10b0-141">Debería ver un toothis similar de respuesta:</span><span class="sxs-lookup"><span data-stu-id="d10b0-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="d10b0-142">Para obtener más instrucciones sobre instalación búsqueda elástica, consulte toohello página [instalación](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="d10b0-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="d10b0-143">Instalación de Logstash</span><span class="sxs-lookup"><span data-stu-id="d10b0-143">Install Logstash</span></span>

1. <span data-ttu-id="d10b0-144">tooinstall Logstash ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="d10b0-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="d10b0-145">A continuación, necesitamos tooconfigure Logstash tooread de salida de hello del archivo eve.json.</span><span class="sxs-lookup"><span data-stu-id="d10b0-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="d10b0-146">Cree un archivo logstash.conf mediante:</span><span class="sxs-lookup"><span data-stu-id="d10b0-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="d10b0-147">Agregar hello toohello contenido el archivo siguiente (asegúrese de que ese archivo de eve.json hello toohello de ruta de acceso sea correcto):</span><span class="sxs-lookup"><span data-stu-id="d10b0-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

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

1. <span data-ttu-id="d10b0-148">Asegúrese de que toogive Hola permisos correctos toohello eve.json el archivo para que Logstash puede introducir archivo hello.</span><span class="sxs-lookup"><span data-stu-id="d10b0-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="d10b0-149">toostart Logstash ejecutar comando hello:</span><span class="sxs-lookup"><span data-stu-id="d10b0-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="d10b0-150">Para obtener más instrucciones acerca de cómo instalar Logstash, consulte toohello [documentación oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="d10b0-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="d10b0-151">Instalación de Kibana</span><span class="sxs-lookup"><span data-stu-id="d10b0-151">Install Kibana</span></span>

1. <span data-ttu-id="d10b0-152">Ejecute hello después comandos tooinstall Kibana:</span><span class="sxs-lookup"><span data-stu-id="d10b0-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="d10b0-153">toorun Kibana use comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="d10b0-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="d10b0-154">tooview web Kibana interfaz, vaya demasiado`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="d10b0-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="d10b0-155">En este escenario, el patrón de índice de hello utilizado para hello Suricata registra es "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="d10b0-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="d10b0-156">Si desea Kibana panel de tooview Hola remotamente, cree una regla de NSG entrada permitir el acceso demasiado**puerto 5601**.</span><span class="sxs-lookup"><span data-stu-id="d10b0-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="d10b0-157">Creación de un panel de Kibana</span><span class="sxs-lookup"><span data-stu-id="d10b0-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="d10b0-158">Para este artículo, proporcionamos un panel de ejemplo para que tooview tendencias y los detalles de las alertas.</span><span class="sxs-lookup"><span data-stu-id="d10b0-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="d10b0-159">Descargar archivo de panel de hello [aquí](https://aka.ms/networkwatchersuricatadashboard), archivo de visualización de hello [aquí](https://aka.ms/networkwatchersuricatavisualization)y el archivo de búsqueda de hello guarda [aquí](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="d10b0-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="d10b0-160">En hello **administración** ficha de Kibana, navegue demasiado**objetos guardados** e importar los tres archivos.</span><span class="sxs-lookup"><span data-stu-id="d10b0-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="d10b0-161">A continuación en hello **panel** ficha puede abrir y carga Hola panel de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d10b0-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="d10b0-162">También puede crear visualizaciones y paneles propios que se adapten a las métricas que le interesen.</span><span class="sxs-lookup"><span data-stu-id="d10b0-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="d10b0-163">Puede leer más sobre la creación de visualizaciones de Kibana en la [documentación oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana.</span><span class="sxs-lookup"><span data-stu-id="d10b0-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![panel de kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="d10b0-165">Visualización de registros de alertas de IDS</span><span class="sxs-lookup"><span data-stu-id="d10b0-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="d10b0-166">panel de ejemplo de Hola proporciona varias visualizaciones de registros de alertas de Hola Suricata:</span><span class="sxs-lookup"><span data-stu-id="d10b0-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="d10b0-167">Alertas por GeoIP: un mapa que muestra la distribución de Hola de alertas de su país de origen en función de la ubicación geográfica (determinado por IP)</span><span class="sxs-lookup"><span data-stu-id="d10b0-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![ip geográfica][3]

1. <span data-ttu-id="d10b0-169">Top 10 alertas: un resumen de hello 10 más frecuentes desencadenada alertas y sus descripciones.</span><span class="sxs-lookup"><span data-stu-id="d10b0-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="d10b0-170">Al hacer clic en una alerta individual filtra hacia abajo de la información del panel de hello toohello pertenecen toothat de alerta específica.</span><span class="sxs-lookup"><span data-stu-id="d10b0-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![imagen 4][4]

1. <span data-ttu-id="d10b0-172">Número de alertas: Hola recuento total de alertas activadas por hello ruleset</span><span class="sxs-lookup"><span data-stu-id="d10b0-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![imagen 5][5]

1. <span data-ttu-id="d10b0-174">20 primeros origen/destino IP/puerto - que muestra los gráficos circulares Hola superior 20 direcciones IP y puertos que las alertas se han activado en.</span><span class="sxs-lookup"><span data-stu-id="d10b0-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="d10b0-175">Puede filtrar hacia abajo en toosee de direcciones IP y puertos específico cuántas y qué tipo de alertas se desencadena.</span><span class="sxs-lookup"><span data-stu-id="d10b0-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![imagen 6][6]

1. <span data-ttu-id="d10b0-177">Resumen de alertas: tabla que resume detalles específicos de cada alerta individual.</span><span class="sxs-lookup"><span data-stu-id="d10b0-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="d10b0-178">Puede personalizar esta tabla tooshow otros parámetros de interés para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="d10b0-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![imagen 7][7]

<span data-ttu-id="d10b0-180">Para ver más documentación sobre la creación de visualizaciones y paneles personalizados, consulte la [documentación oficial del Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="d10b0-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="d10b0-181">Conclusión</span><span class="sxs-lookup"><span data-stu-id="d10b0-181">Conclusion</span></span>

<span data-ttu-id="d10b0-182">Al combinar las capturas de paquetes proporcionadas por Network Watcher con herramientas IDS de código abierto como Suricata, puede realizar la detección de intrusiones para una amplia variedad de amenazas.</span><span class="sxs-lookup"><span data-stu-id="d10b0-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="d10b0-183">Estos paneles permiten tooquickly detectar tendencias y las anomalías dentro de la red, también adentrarse en hello causas raíz de toodiscover de datos de alertas, como agentes de usuario malintencionado o puertos vulnerables.</span><span class="sxs-lookup"><span data-stu-id="d10b0-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="d10b0-184">Con estos datos extraídos, puede tomar decisiones informadas acerca de cómo tooreact tooand proteger su red de los intentos de intrusión perjudicial y crear reglas tooprevent futuras intrusiones tooyour red.</span><span class="sxs-lookup"><span data-stu-id="d10b0-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d10b0-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d10b0-185">Next steps</span></span>

<span data-ttu-id="d10b0-186">Obtenga información acerca de la captura de paquetes de tootrigger alertas en función de si visita [usar paquetes captura toodo automático supervisión de red con funciones de Azure](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d10b0-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="d10b0-187">Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="d10b0-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
