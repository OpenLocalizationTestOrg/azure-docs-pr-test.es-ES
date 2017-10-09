# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Escalado de nodos de agente en un clúster de Container Service
Después de [implementación de un clúster de servicio de contenedor de Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), tendrá que número de hello toochange de nodos de agente. Por ejemplo, puede que necesite más agentes para poder ejecutar más aplicaciones o instancias de contenedor. 

Puede cambiar número de Hola de nodos de agente en un clúster de DC/OS, Docker Swarm o Kubernetes con hello portal de Azure u Hola 2.0 de CLI de Azure. 

## <a name="scale-with-hello-azure-portal"></a>Escalar con hello portal de Azure

1. Hola [portal de Azure](https://portal.azure.com), busque **servicios de contenedor**y, a continuación, haga clic en servicio de contenedor de Hola que desea toomodify.
2. Hola **servicio de contenedor** hoja, haga clic en **agentes**.
3. En **recuento de VM**, escriba Hola deseado número de nodos de agentes.

    ![Escalar un grupo en el portal de Hola](./media/container-service-scale/container-service-scale-portal.png)

4. configuración de hello toosave, haga clic en **guardar**.

## <a name="scale-with-hello-azure-cli-20"></a>Escalar con hello 2.0 de CLI de Azure

Asegúrese de que se [instalado](/cli/azure/install-az-cli2) Hola 2.0 más reciente de CLI de Azure y registran en tooan cuenta de azure (`az login`).

### <a name="see-hello-current-agent-count"></a>Vea el número de agentes de hello actual
número de hello toosee de agentes actualmente en clúster de hello, ejecute hello `az acs show` comando. Esto muestra la configuración de clúster de Hola. Por ejemplo, Hola siguiente comando muestra Hola configuración del servicio de contenedor de hello denominado `containerservice-myACSName` en grupo de recursos de Hola `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

comando Hello devuelve el número de Hola de agentes de hello `Count` valor bajo `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Use Hola az comandos de escala de acs
número de hello toochange de nodos de agente, ejecute hello `az acs scale` comando y proporcione hello **grupo de recursos**, **el nombre del servicio de contenedor**, hello deseado y **nuevo número de agentes**. Con un número mayor o menor, puede reducir o aumentar verticalmente, respectivamente.

Por ejemplo, número de hello toochange de agentes en hello too10 de clúster anterior, escriba Hola siguiente comando:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Hola 2.0 de CLI de Azure devuelve una cadena JSON que representa la nueva configuración del servicio de contenedor de hello, incluido el nuevo número de agentes Hola de Hola.

Para obtener más opciones de comando, ejecute `az acs scale --help`.

## <a name="scaling-considerations"></a>Consideraciones sobre escalado

* número de Hola de nodos de agente debe estar entre 1 y 100, ambos inclusive. 

* Su cuota de núcleos puede limitar el número de Hola de nodos de agente en un clúster.

* Las operaciones de escalado de nodo de agente son el conjunto de escalas de máquina virtual de Azure tooan aplicados que contiene el grupo de agente de Hola. En un clúster de DC/OS, solo los nodos de agente de grupo privada Hola se escalan por operaciones de Hola que se muestran en este artículo.

* Función de orchestrator de Hola que se implementan en el clúster, puede escalar por separado número Hola de instancias de un contenedor que se ejecuta en el clúster de Hola. Por ejemplo, en un clúster de DC/OS, usar hello [interfaz de usuario de maratón](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) número de hello toochange de instancias de una aplicación de contenedor.

* Actualmente, no se admite el escalado automático de nodos de agente en un clúster de servicio de contenedores.

## <a name="next-steps"></a>Pasos siguientes
* Consulte [más ejemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) de uso de comandos de la CLI de Azure 2.0 con Azure Container Service.
* Aprenda más sobre los [grupos de agentes de DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) en Azure Container Service.

