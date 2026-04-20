# Laboratorio 5 – Análisis de paquetes y detección de anomalías
**CC3094 Security Data Science** | Universidad del Valle de Guatemala

## Descripción
Análisis de una captura de red (`analisis_paquetes.pcap`) para detectar tráfico sospechoso usando técnicas estadísticas y machine learning, siguiendo el flujo de trabajo de un SOC.

## Flujo del laboratorio
1. **Exploración inicial** – carga del pcap con Scapy, inspección de IPs, puertos y protocolos.
2. **Z-Score** – detección de anomalías por tamaño de payload, primero con estadísticas del propio pcap (falla por distribución bimodal) y luego con baseline del protocolo DNS (μ=50 bytes, σ=15 bytes), detectando **30 paquetes anómalos**.
3. **Isolation Forest** – confirmación automática de las mismas 30 anomalías sin conocimiento previo del protocolo.
4. **Inspección manual del payload** – los bytes del payload revelan la firma PNG (`\x89PNG`, `IHDR`, `IDAT`) dentro de paquetes DNS, confirmando un ataque de **DNS Tunneling**.

## Resultado
La máquina `10.1.10.53` exfiltraba imágenes PNG hacia `84.54.22.33` ocultando los datos en consultas DNS (puerto 53) para evadir firewalls.

## Requisitos
```
scapy · pandas · numpy · matplotlib · scikit-learn
```
