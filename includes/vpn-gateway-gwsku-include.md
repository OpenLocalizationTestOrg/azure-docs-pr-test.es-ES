Cuando se crea una puerta de enlace de red virtual, deberá toospecify puerta de enlace de hello SKU que desea toouse. Seleccione las SKU de Hola que satisface sus requisitos en función de los tipos de Hola de cargas de trabajo, capacidad de proceso, características y los SLA.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Cargas de trabajo  *de producción* frente a cargas de desarrollo y pruebas

Debido a diferencias de toohello de SLA y conjuntos de características, se recomienda que siga SKU para la producción de hello *frente a* desarrollo pruebas:

| **Carga de trabajo**                       | **SKU**               |
| ---                                | ---                    |
| **Cargas de trabajo de producción, críticas** | VpnGw1, VpnGw2, VpnGw3 |
| **Desarrollo y pruebas o prueba de concepto**   | Básica                  |
|                                    |                        |

Si usas Hola antiguo recomendaciones de SKU de producción de hello las SKU son Standard y SKU de alto rendimiento. Para obtener información sobre Hola SKU anteriores, vea [SKU de puerta de enlace (SKU heredadas)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Conjuntos de características de las SKU de puerta de enlace

Hola nueva puerta de enlace SKU optimizada Hola conjuntos de características que se ofrece en las puertas de enlace de hello:

| **SKU**| **Características**|
| ---    | ---         |
|**Básico**   | **VPN basada en enrutamiento**: 10 túneles con P2S<br><br>**VPN basada en directivas**: (IKEv1): 1 túnel; sin P2S|
| **VpnGw1, VpnGw2 y VpnGw3** | **VPN basadas en enrutamiento**: túneles too30 (*), P2S, BGP, directiva de IPsec/IKE activo / activo, personalizada, coexistencia de VPN/ExpressRoute |
|        |             |

(*) Se pueden configurar tooconnect "PolicyBasedTrafficSelectors" un basadas en enrutamiento puerta de enlace (VpnGw1, VpnGw2, VpnGw3) toomultiple local basada en directivas de firewall los dispositivos VPN. Consulte demasiado[toomultiple de puertas de enlace de VPN conectarse dispositivos VPN basada en directivas con PowerShell local](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obtener más información.

###  <a name="resize"></a>Cambio de tamaño de las SKU de puerta de enlace

1. Puede cambiar el tamaño entre las SKU de VpnGw1, VpnGw2 y VpnGw3.
2. Cuando se trabaja con la puerta de enlace anterior de hello SKU, puede cambiar el tamaño entre básico, estándar y SKU de alto rendimiento.
2. Se **no** cambiar el tamaño de las SKU Standard/Basic/HighPerformance toohello nuevo SKU VpnGw1/VpnGw2/VpnGw3. En su lugar, debe [migrar](#migrate) toohello SKU nuevo.

###  <a name="migrate"></a>Migrar desde el antiguo toohello SKU SKU nueva

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
