# ExamenFinalRedes_GabrielHernanz_153982

Link con acceso al respositorio --> https://github.com/GabriHR/ExamenFinalRedes_GabrielHernanz_153982.git

## Parte I - Misiones de Conocimiento Teórico

# 🛰️ Misión 1: Reconexión en la Base Eco (Hoth) – Direccionamiento IP y Subredes

## 📖 Situación
La Base Eco en Hoth ha quedado incomunicada tras un bombardeo imperial. La General Leia Organa te encomienda diseñar un nuevo esquema de red para restablecer la comunicación interna y con la flota rebelde. Hoth alberga varios departamentos (mando, defensa, médico, hangar) y cada uno necesita su propia subred IP debido a requisitos de seguridad y cantidad de dispositivos. Además, es crucial optimizar el uso del bloque de direcciones disponibles.

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
Cada departamento de la Base Eco cuenta ahora con una subred optimizada, maximizando el uso del espacio disponible y asegurando la comunicación interna y con la antena de comunicaciones. ¡Misión cumplida, padawan! Que la Fuerza del subnetting te acompañe. 🔥✨
