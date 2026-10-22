# IP

## Bloques privados 

10.0.0.0/8 - 10.255.255.255

172.16.0.0/12 - 172.31.255.255

192.168.0.0/16 - 192.168.255.255

## Máscaras de subred

### Reglas
- La máscara de subred debe ser contigua, es decir, no puede haber un 0 entre 1s.
- La máscara de subred debe tener al menos 2 bits en 1, es decir, no puede ser 0.0.0.0.

### Clase A
| CIDR | Máscaras | HEX | 
|------|----------|-----| 
| /8 | 255.0.0.0 | FF.0.0.0 |
| /9 | 255.128.0.0 | FF.80.0.0 |
| /10 | 255.192.0.0 | FF.C0.0.0 |
| /11 | 255.224.0.0 | FF.E0.0.0 |
| /12 | 255.240.0.0 | FF.F0.0.0 |
| /13 | 255.248.0.0 | FF.F8.0.0 |
| /14 | 255.252.0.0 | FF.FC.0.0 |
| /15 | 255.254.0.0 | FF.FE.0.0 |

### Clase B
| CIDR | Máscaras | - |
|------|----------|-----|
| /16 | 255.255.0.0 | - |
| /17 | 255.255.128.0 | - |
| /18 | 255.255.192.0 | - |
| /19 | 255.255.224.0 | - |
| /20 | 255.255.240.0 | - |
| /21 | 255.255.248.0 | - |
| /22 | 255.255.252.0 | - |
| /23 | 255.255.254.0 | - |

### Clase C

| CIDR | Máscaras | - |
|------|----------|-----|
| /24 | 255.255.255.0 | - |
| /25 | 255.255.255.128 | - |
| /26 | 255.255.255.192 | - |
| /27 | 255.255.255.224 | - |
| /28 | 255.255.255.240 | - |
| /29 | 255.255.255.248 | - |
| /30 | 255.255.255.252 | - |
| /31 | 255.255.255.254 | - |


### Ejemplo 

169.10.5.49/25

- La red es clase B
- La máscara de subred es 255.255.255.128

### Comando útil `ipcalc`
El comando `ipcalc` es una herramienta útil para calcular información relacionada con direcciones IP y máscaras de subred. Permite determinar la red, el rango de direcciones IP, la dirección de broadcast y otros detalles importantes a partir de una dirección IP y una máscara de subred. Es especialmente útil para administradores de red y profesionales de TI que necesitan planificar y gestionar redes de manera eficiente. Por ejemplo, al ejecutar `ipcalc 169.10.5.49/25`, se obtiene información sobre la red, el rango de direcciones IP, la dirección de broadcast y otros detalles importantes.


