# ExamenFinalRedes_GabrielHernanz_153982

Link con acceso al respositorio --> https://github.com/GabriHR/ExamenFinalRedes_GabrielHernanz_153982.git

# Parte I - Misiones de Conocimiento Teórico

## 🛰️ Misión 1: Reconexión en la Base Eco (Hoth) – Direccionamiento IP y Subredes

## 📖 Situación
La Base Eco en Hoth ha quedado incomunicada tras un bombardeo imperial. La General Leia Organa te encomienda diseñar un nuevo esquema de red para restablecer la comunicación interna y con la flota rebelde. Hoth alberga varios departamentos (mando, defensa, médico, hangar) y cada uno necesita su propia subred IP debido a requisitos de seguridad y cantidad de dispositivos. Disponéis de un bloque de direcciones limitado y es crucial usarlo eficientemente.

**Narrativa:** Bajo la tormenta helada de Hoth, los generadores de energía zumban mientras instalas nuevos equipos de red. Leia, con su atuendo invernal, te explica: "Necesitamos reorganizar las comunicaciones de la base. Cada sector debe tener su red, y todas deben poder conectarse con la antena principal. El rango de direcciones del que disponemos es limitado, joven padawan. Debes dividir la red sabiamente, como un Jedi dividiría sus esfuerzos.".

**Objetivo de la misión:** Diseña un plan de direccionamiento IP para la Base Eco utilizando subnetting. Parte de una red asignada (por ejemplo, 172.16.0.0/24) y subdivide en subredes adecuadas para cada departamento, cumpliendo estos requisitos (ficticios):

- Comando Central: ~50 hosts (dispositivos)

- Defensa Perimetral: ~30 hosts

- Centro Médico: ~20 hosts

- Hangar y Taller: ~14 hosts

Además, reserva una subred adicional para el enlace troncal con la antena de comunicaciones que conecta Hoth con el resto de la galaxia. Debes detallar la dirección de red, máscara y rango de hosts de cada subred resultante.

**Pregunta:** ¿Cómo dividirías la red 172.16.0.0/24 en subredes para satisfacer las necesidades anteriores, asignando direcciones IP a cada segmento de la base? Indica las subredes obtenidas (con su notación de máscara /xx), la cantidad de hosts útiles en cada una, y especifica qué subred se destinaría al enlace troncal interplanetario.
## 🛠️ Plan de direccionamiento IP
Partimos de la red **172.16.0.0/24** y la dividimos en subredes adecuadas para cada departamento.

### Asignación de subredes

| Departamento         | Dirección de Red     | Máscara de Subred       | Rango de Hosts Utilizables     | Total de Hosts |
|----------------------|---------------------|-------------------------|-------------------------------|--------------|
| **Comando Central** | `172.16.0.0/26`     | `255.255.255.192`       | `172.16.0.1 - 172.16.0.62`    | 62          |
| **Defensa Perimetral** | `172.16.0.64/27`   | `255.255.255.224`       | `172.16.0.65 - 172.16.0.94`   | 30          |
| **Centro Médico**   | `172.16.0.96/27`    | `255.255.255.224`       | `172.16.0.97 - 172.16.0.126`  | 30          |
| **Hangar y Taller** | `172.16.0.128/28`   | `255.255.255.240`       | `172.16.0.129 - 172.16.0.142` | 14          |
| **Enlace Troncal**  | `172.16.0.144/28`   | `255.255.255.240`       | `172.16.0.145 - 172.16.0.158` | 14          |

## Conclusión
Cada departamento de la Base Eco cuenta ahora con una subred optimizada, maximizando el uso del espacio disponible y asegurando la comunicación interna y con la antena de comunicaciones. ¡Misión cumplida, padawan! Que la Fuerza del subnetting te acompañe. 

---

# 🌌 Misión 2: Sabiduría de Yoda – Algoritmos de Enrutamiento y Rutas
## 📖 Situación 
La flota rebelde ha interceptado transmisiones imperiales que mencionan distintos códigos de planeta y nombres en clave. Para coordinar un contraataque, la Alianza necesita entender cómo los nombres de dominio galácticos se traducen en localizaciones reales. En otras palabras, requieren restablecer un servicio DNS rebelde que asocie nombres de sistemas estelares con direcciones de la red. Sin DNS, comunicarse es tan difícil como encontrar un Ewok en la noche de Endor.

## Narrativa: 
A bordo de la nave de mando Home One, los técnicos rebelde te muestran un panel donde parpadea la petición “Unknown host”. El Almirante Ackbar frunce el ceño mientras exclaims: "¡Es una trampa... de nombres! Nuestros sistemas no reconocen las direcciones de destino." Mon Mothma asiente con gravedad: "Debemos reconstruir nuestro directorio de comunicaciones. Aprendiz, ¿cómo funciona este Sistema de Nombres de Dominio nuestro? ¿Por qué es tan importante?".

Tú recuerdas tus lecciones sobre cómo en la Red (o la HoloRed) se gestionan las direcciones simbólicas. Un nombre como “echo.base” debe traducirse a una dirección IP para establecer conexión. Ha llegado el momento de explicarlo claramente.

**Pregunta: Explica el funcionamiento básico del sistema DNS** y su importancia en la comunicación en redes. ¿Cómo realiza la red rebelde (o cualquier red TCP/IP) la resolución de nombres de dominio a direcciones IP? Incluye en tu explicación qué es un servidor DNS y un registro (por ejemplo, un registro A), ilustrando con un ejemplo simple (por ejemplo: traducir holonet.rebelion.org a una dirección IP)


Además, menciona brevemente qué sucede si el servidor DNS no está disponible y cómo eso afectaría a las comunicaciones de la Alianza.

## Solución:
### Comparación: Enrutamiento Estático vs. Dinámico

| Tipo de Enrutamiento | Ventajas | Inconvenientes |
|----------------------|----------|---------------|
| **Estático** | - Control total sobre las rutas.<br>- Menor consumo de recursos.<br>- Mayor seguridad al evitar cambios automáticos. | - No se adapta a cambios en la red.<br>- Difícil de gestionar en redes grandes.<br>- Requiere configuración manual en cada nodo. |
| **Dinámico** | - Se ajusta automáticamente a cambios en la topología.<br>- Escalable para redes grandes.<br>- Optimiza el uso del ancho de banda. | - Mayor consumo de CPU y memoria.<br>- Puede tardar en converger tras una falla.<br>- Más complejo de configurar. |

### Protocolos de Enrutamiento Dinámico
Uno de los protocolos más utilizados en enrutamiento dinámico es **OSPF (Open Shortest Path First)**. Este protocolo de estado de enlace permite que los routers intercambien información sobre la topología de la red y calculen la mejor ruta de manera eficiente.

Por otro lado, los protocolos de **vector de distancia**, como **RIP (Routing Information Protocol)**, funcionan enviando información sobre las rutas a sus vecinos, pero tienen limitaciones en redes grandes debido a su tiempo de convergencia y la métrica basada en el número de saltos.

### Diferencias entre Vector de Distancia y Estado de Enlace
- **Vector de distancia**: Los routers solo conocen información de sus vecinos y envían actualizaciones periódicas. Es más simple pero menos eficiente en redes grandes.
- **Estado de enlace**: Cada router tiene una visión completa de la red y calcula rutas óptimas. Es más rápido y preciso, pero requiere más recursos.

### Respuesta ante fallos y escalabilidad
Si un nodo cae repentinamente:
- **Enrutamiento estático**: La ruta se rompe y debe ser corregida manualmente.
- **Enrutamiento dinámico**: Los routers detectan el fallo y recalculan automáticamente nuevas rutas.

Si la red debe expandirse a más planetas:
- **Enrutamiento estático**: Se vuelve inmanejable debido a la cantidad de rutas manuales.
- **Enrutamiento dinámico**: Se adapta automáticamente, permitiendo una expansión fluida.

### Conclusión
El enrutamiento estático es ideal para redes pequeñas y controladas, mientras que el dinámico es esencial para redes grandes y cambiantes. ¡Misión cumplida, padawan! Que la Fuerza del enrutamiento te guíe en tu camino. 

---

# 🌌 Misión 3: Los Nombres del Holonet – DNS y Resolución de Nombres

## 📖 Situación
La flota rebelde ha interceptado transmisiones imperiales que mencionan distintos códigos de planeta y nombres en clave. Para coordinar un contraataque, la Alianza necesita entender cómo los nombres de dominio galácticos se traducen en localizaciones reales. En otras palabras, requieren restablecer un servicio DNS rebelde que asocie nombres de sistemas estelares con direcciones de la red. Sin DNS, comunicarse es tan difícil como encontrar un Ewok en la noche de Endor.

**Narrativa:** A bordo de la nave de mando Home One, los técnicos rebelde te muestran un panel donde parpadea la petición “Unknown host”. El Almirante Ackbar frunce el ceño mientras exclaims: "¡Es una trampa... de nombres! Nuestros sistemas no reconocen las direcciones de destino." Mon Mothma asiente con gravedad: "Debemos reconstruir nuestro directorio de comunicaciones. Aprendiz, ¿cómo funciona este Sistema de Nombres de Dominio nuestro? ¿Por qué es tan importante?".

Tú recuerdas tus lecciones sobre cómo en la Red (o la HoloRed) se gestionan las direcciones simbólicas. Un nombre como “echo.base” debe traducirse a una dirección IP para establecer conexión. Ha llegado el momento de explicarlo claramente.

**Pregunta:** Explica el funcionamiento básico del sistema DNS y su importancia en la comunicación en redes. ¿Cómo realiza la red rebelde (o cualquier red TCP/IP) la resolución de nombres de dominio a direcciones IP? Incluye en tu explicación qué es un servidor DNS y un registro (por ejemplo, un registro A), ilustrando con un ejemplo simple (por ejemplo: traducir holonet.rebelion.org a una dirección IP)​

Además, menciona brevemente qué sucede si el servidor DNS no está disponible y cómo eso afectaría a las comunicaciones de la Alianza.
##  ¿Qué es el DNS y por qué es importante?
El **Sistema de Nombres de Dominio (DNS)** traduce nombres de dominio legibles por humanos en direcciones IP comprensibles por las máquinas. Sin DNS, tendríamos que recordar largas secuencias numéricas en lugar de nombres intuitivos como `holonet.rebelion.org`.

## ¿Cómo funciona la resolución de nombres?
Cuando un dispositivo intenta acceder a un dominio, sigue estos pasos:
1. **Consulta al servidor DNS local**: El dispositivo pregunta a su servidor DNS si conoce la dirección IP del dominio.
2. **Búsqueda en caché**: Si el servidor DNS ya tiene la dirección almacenada, la devuelve inmediatamente.
3. **Consulta a servidores superiores**: Si no tiene la respuesta, pregunta a los servidores raíz, que dirigen la consulta a los servidores de dominio adecuados.
4. **Respuesta final**: Una vez encontrada la dirección IP, el servidor DNS la envía al dispositivo, permitiendo la conexión.

## Elementos clave del DNS
- **Servidor DNS**: Un sistema que almacena y gestiona la traducción de nombres de dominio a direcciones IP.
- **Registro A**: Un tipo de registro DNS que asocia un nombre de dominio con una dirección IPv4. Ejemplo:
