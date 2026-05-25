# Proyecto Final: Análisis del Comportamiento de Aplicaciones bajo Diferentes Escenarios de Despliegue

## Curso

Principios y prácticas de desarrollo de software orientado a objetos

## Integrantes

* Santiago Camargo Ardila – 2211873
* Sebastián Laguna Funes – 2211911
* Juan Manuel Ramírez Salamanca – 2192279

---

# 1. Introducción

Este proyecto tiene como propósito analizar el comportamiento y rendimiento de una aplicación backend desplegada en diferentes escenarios de infraestructura utilizando tecnologías de contenedores y orquestación. A lo largo del desarrollo se compararon métricas importantes como el throughput y la latencia promedio para determinar cómo cambia el rendimiento de una aplicación cuando pasa de un entorno local a un entorno distribuido basado en Kubernetes.

Para el desarrollo del proyecto se utilizó una aplicación basada en FastAPI y PostgreSQL, desplegada mediante Docker Compose y posteriormente en clústeres de Kubernetes sobre DigitalOcean. El análisis se realizó utilizando pruebas de carga generadas con Apache JMeter y la visualización de resultados mediante Jupyter Notebook.

El objetivo principal fue observar el impacto del escalado horizontal, el número de nodos y el número de réplicas sobre el rendimiento general de la aplicación, permitiendo identificar ventajas, limitaciones y comportamientos característicos de cada arquitectura de despliegue.

---

# 2. Objetivo General

Analizar el comportamiento de una aplicación backend bajo diferentes escenarios de despliegue utilizando Docker y Kubernetes, observando métricas de rendimiento y escalabilidad para comprender cómo influye la infraestructura en el desempeño de la aplicación.

---

# 3. Objetivos Específicos

* Desplegar una aplicación utilizando Docker Compose en un entorno local.
* Implementar la misma aplicación en Kubernetes con diferentes configuraciones de nodos y réplicas.
* Generar carga utilizando Apache JMeter para medir métricas de rendimiento.
* Analizar el throughput y la latencia bajo diferentes niveles de carga.
* Comparar el comportamiento entre entornos locales y distribuidos.
* Evaluar el impacto del escalado horizontal sobre el rendimiento.
* Documentar el proceso completo mediante Jupyter Notebook.

---

# 4. Descripción de la Aplicación

La aplicación utilizada corresponde al repositorio Full Stack FastAPI Template, una solución moderna orientada al desarrollo de aplicaciones backend y frontend.

La arquitectura del sistema está compuesta por:

* Backend desarrollado en FastAPI.
* Base de datos PostgreSQL.
* Frontend en React.
* Contenedores Docker.
* Orquestación con Kubernetes.

La aplicación expone una API REST que permite realizar operaciones sobre los datos almacenados en la base de datos. Para garantizar pruebas más realistas, se poblaron aproximadamente 5000 registros utilizando un script automatizado de seeding.

---

# 5. Tecnologías Utilizadas

Durante el desarrollo del proyecto se utilizaron las siguientes herramientas:

* Python 3
* FastAPI
* PostgreSQL
* Docker
* Docker Compose
* Kubernetes
* kubectl
* DigitalOcean
* Apache JMeter
* Jupyter Notebook
* Pandas
* Matplotlib
* Seaborn

---

# 6. Escenarios de Despliegue

## Fase 1: Docker Compose Local

En esta fase la aplicación fue desplegada localmente utilizando Docker Compose. Este escenario permitió establecer una línea base de rendimiento para comparar posteriormente con Kubernetes.

Se levantaron los siguientes servicios:

* Backend FastAPI
* Frontend React
* Base de datos PostgreSQL

Posteriormente se realizaron pruebas de carga para observar el comportamiento del sistema bajo estrés.

---

## Fase 2: Kubernetes con 1 Nodo

En esta fase la aplicación fue desplegada en un clúster de Kubernetes compuesto por un único nodo en DigitalOcean.

Se utilizaron archivos YAML para crear:

* Deployments
* Services
* Configuración de Pods

Posteriormente se realizaron pruebas variando el número de réplicas:

* 1 réplica
* 2 réplicas
* 3 réplicas

El objetivo fue analizar el impacto del escalado dentro de un único nodo físico.

---

## Fase 3: Kubernetes con 2 Nodos

En esta fase el clúster fue expandido a dos nodos para implementar escalado horizontal distribuido.

Se mantuvieron las mismas pruebas de carga y variaciones de réplicas:

* 1 réplica
* 2 réplicas
* 3 réplicas

Esto permitió comparar cómo influye la distribución de carga entre múltiples nodos físicos.

---

# 7. Metodología de Pruebas

Las pruebas de carga se realizaron utilizando Apache JMeter.

La configuración utilizada fue:

| Parámetro             | Valor       |
| --------------------- | ----------- |
| Usuarios Concurrentes | 50          |
| Ramp-Up               | 10 segundos |
| Loop Count            | 100         |
| Método HTTP           | GET         |

Las métricas observadas fueron:

* Throughput (peticiones por segundo)
* Latencia promedio (ms)

Las pruebas se ejecutaron para cada escenario y para cada número de réplicas.

---

# 8. Resultados Obtenidos

| Escenario          | Réplicas | Throughput | Latencia |
| ------------------ | -------- | ---------- | -------- |
| Local              | 1        | 81.43      | 508 ms   |
| Kubernetes 1 Nodo  | 1        | 96.8       | 410 ms   |
| Kubernetes 1 Nodo  | 2        | 104.5      | 365 ms   |
| Kubernetes 1 Nodo  | 3        | 109.2      | 344 ms   |
| Kubernetes 2 Nodos | 1        | 122.6      | 291 ms   |
| Kubernetes 2 Nodos | 2        | 136.9      | 248 ms   |
| Kubernetes 2 Nodos | 3        | 148.4      | 221 ms   |

---

# 9. Análisis de Resultados

Los resultados obtenidos muestran una mejora progresiva del rendimiento a medida que la infraestructura se vuelve más distribuida y escalable.

En el entorno local se observó el menor throughput y la mayor latencia, lo cual evidencia las limitaciones de ejecutar pruebas de carga sobre una máquina local con virtualización de contenedores.

Cuando la aplicación fue desplegada en Kubernetes con un solo nodo, el rendimiento mejoró significativamente debido a una mejor administración de recursos y al uso eficiente de contenedores.

Sin embargo, el mayor rendimiento se obtuvo en el escenario de Kubernetes con dos nodos, donde el escalado horizontal permitió distribuir mejor la carga de trabajo y reducir considerablemente los tiempos de respuesta.

Además, se observó que aumentar el número de réplicas incrementó el throughput y disminuyó la latencia, demostrando la efectividad del balanceo de carga y la capacidad de Kubernetes para escalar aplicaciones backend.

---

# 10. Conclusiones

* Kubernetes permitió mejorar significativamente el rendimiento respecto al entorno local.
* El escalado horizontal utilizando múltiples nodos generó mejores resultados que únicamente aumentar réplicas dentro de un mismo nodo.
* El throughput aumentó progresivamente al incrementar el número de réplicas.
* La latencia disminuyó considerablemente en los escenarios distribuidos.
* La mejor configuración encontrada fue Kubernetes con 2 nodos y 3 réplicas.
* Docker Compose es útil para desarrollo local, pero Kubernetes ofrece mejores capacidades de escalabilidad y tolerancia a carga.
* Las pruebas realizadas demostraron la importancia de la infraestructura en el rendimiento de aplicaciones backend modernas.

---

# 11. Recomendaciones

* Implementar monitoreo utilizando Prometheus y Grafana para obtener métricas internas más detalladas.
* Realizar pruebas con mayor número de usuarios concurrentes.
* Optimizar la base de datos para reducir posibles cuellos de botella.
* Implementar balanceadores de carga avanzados para mejorar aún más el rendimiento.

---

# 12. Referencias

* Repositorio Full Stack FastAPI Template
* Documentación oficial de FastAPI
* Documentación oficial de Kubernetes
* Apache JMeter
* Docker Documentation
* DigitalOcean Kubernetes Documentation

