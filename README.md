# PortTrack: Despliegue y Monitoreo Continuo

Este repositorio contiene los archivos de configuración y scripts necesarios para la estrategia de **Despliegue Continuo (CD)** y **Monitoreo** de la plataforma PortTrack, una solución de gestión de navegación portuaria.

La estrategia se basa en principios de **DevOps** y utiliza **GitHub Actions** para el pipeline de CI/CD, y **Prometheus** junto con **Kubernetes** para el monitoreo.

---

## 📂 Estructura del Repositorio

```
.github/workflows/      # Archivo YAML para el pipeline de GitHub Actions
    └─ main.yml           # Define el flujo de trabajo de CI/CD
config/                 # Archivos de configuración para monitoreo
    └─ prometheus.yml     # Configuración del servidor Prometheus
k8s/                    # Manifiestos de Kubernetes (no incluidos en este ejemplo)
README.md               # Este archivo
```

---

## 🚀 Despliegue Continuo con GitHub Actions

El pipeline de CI/CD está automatizado para ejecutarse en cada push a la rama `main`. El flujo de trabajo realiza los siguientes pasos:

1. **Build y Test:** Construye la aplicación y ejecuta pruebas unitarias.
2. **Construcción de Imagen Docker:** Crea una imagen Docker del servicio.
3. **Despliegue a Kubernetes:** Despliega la nueva versión en el clúster, siguiendo una estrategia *Blue-Green*.
4. **Notificaciones:** Envía notificaciones automáticas a Slack sobre el estado del despliegue (éxito o fallo).

**GitHub Secrets necesarios:**

- `GH_PAT_TOKEN`: Token de acceso personal de GitHub con permisos para paquetes.
- `KUBE_CONFIG`: Archivo de configuración de Kubernetes codificado en base64.
- `SLACK_WEBHOOK_URL`: URL del webhook de Slack para notificaciones.

---

## 📊 Monitoreo con Prometheus

El monitoreo de la infraestructura y microservicios se realiza con **Prometheus**. La configuración en `config/prometheus.yml` está diseñada para:

- **Descubrimiento de Servicios:** Integración con Kubernetes para encontrar automáticamente nodos y endpoints.
- **Scrape de Métricas:** Recolecta métricas de rendimiento (CPU, memoria, etc.) de todos los componentes del clúster.

> **Nota:** Cada microservicio debe exponer un endpoint de métricas compatible con Prometheus.

---

## 🌐 Enlaces Útiles

- [Documentación de GitHub Actions](https://docs.github.com/es/actions)
- [Documentación de Prometheus](https://prometheus.io/docs/introduction/overview/)
- [Documentación de Kubernetes](https://kubernetes.io/es/docs/)

---