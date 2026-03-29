# ⚙️ Config Server - ElectrodoStore

## 📌 Descripción
Servidor de configuración centralizada para el ecosistema de microservicios
de ElectrodoStore, basado en **Spring Cloud Config Server**.

Todos los microservicios obtienen su configuración desde este servidor al
momento de iniciar, eliminando la necesidad de gestionar archivos de
configuración de forma individual en cada servicio.

---

## ⚙️ Tecnologías utilizadas

- Java + Spring Boot
- Spring Cloud Config Server
- Git (como backend de configuración)

---

## 🔄 ¿Cómo funciona?

El Config Server lee las configuraciones directamente desde el
**config-repo** (repositorio GitHub), y las sirve a cada microservicio
en el momento de su arranque.
```
Microservicio → Config Server → config-repo
```

Esto permite:
- Cambiar configuraciones sin recompilar ni redesplegar servicios
- Centralizar variables de entorno y propiedades
- Versionar la configuración junto al código

---

## 🗂️ Repositorio de configuraciones

Las configuraciones de todos los servicios están alojadas en **GitHub**
→ [config-repo](https://github.com/electrodostore/electrodostore-config-server-repo)

| Propiedad | Valor |
|---|---|
| Visibilidad | ✅ Público |
| Credenciales | 🔒 Externalizadas mediante variables de entorno |

---

## 🔌 Configuración de red

| Propiedad | Valor |
|---|---|
| Puerto | `8888` |
| Acceso | 🔒 Solo interno — consumido por los microservicios |

---

## ⚠️ Variables de entorno requeridas

| Variable | Descripción |
|---|---|
| `GITHUB_URL` | URL del repositorio de configuraciones |
| `GITHUB_USERNAME` | Usuario de GitHub |
| `GITHUB_TOKEN` | Token de acceso a GitHub |
| `PORT` | Puerto del servidor (por defecto `8888`) |

---

## ▶️ Ejecución local

**Con Maven**
```bash
# Corre en el puerto 8888
mvn spring-boot:run
```

**Con Docker**
```bash
docker build -t config-server .
```

> ⚠️ Este servicio debe iniciarse **antes que cualquier otro microservicio**,
> ya que todos dependen de él para obtener su configuración.

---

## 💡 Decisiones de diseño

- Backend Git para versionar la configuración junto al código
- Credenciales externalizadas mediante variables de entorno
- Puerto estándar de Spring Cloud Config (`8888`)

---

## 🚀 Mejoras futuras

- Cifrado de propiedades sensibles con Spring Cloud Config encryption
- Refresh automático de configuración sin reiniciar servicios (`@RefreshScope`)
- Monitoreo del estado del servidor