Azure ofrece Hola siguiendo las SKU de puerta de enlace VPN:

|**SKU**   | **Túneles<br>S2S/entre redes virtuales** | **Conexiones<br>P2S** | **Pruebas comparativas de rendimiento<br>agregado** |
|---       | ---                             | ---                    | ---                         |
|**VpnGw1**| Máx. 30                         | Máx. 128               | 650 MBps                    |
|**VpnGw2**| Máx. 30                         | Máx. 128               | 1 Gbps                      |
|**VpnGw3**| Máx. 30                         | Máx. 128               | 1,25 Gbps                   |
|**Básica** | Máx. 10                         | Máx. 128               | 100 Mbps                    | 
|          |                                 |                        |                             | 

- Las pruebas comparativas de rendimiento agregado se basan en las mediciones de varios túneles agregados a través de una sola puerta de enlace. No es un rendimiento garantizado debido a las condiciones del tráfico tooInternet y los comportamientos de la aplicación.

- Información sobre los precios puede encontrarse en hello [precios](https://azure.microsoft.com/pricing/details/vpn-gateway) página.

- Información del SLA (contrato de nivel de servicio) puede encontrarse en hello [SLA](https://azure.microsoft.com/support/legal/sla/vpn-gateway/) página.
