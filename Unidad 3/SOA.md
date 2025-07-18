Son las siglas de **Arquitectura Orientada a Servicios**.

Los **Servicios** pueden ser componentes o flujos que sirven de apoyo para ejecutar o desarrollar cierta funcionalidad.

[[Topología]]:
```mermaid
graph TD
	A[Interfaz Usuario] --> B
	A --> C
	A --> D
	B[Servicio 1] --> E
	C[Servicio 2] --> E
	D[Servicio N] --> E
	E[Base de datos]
```
**Variantes:**

- Separación por servicio
```mermaid
graph TD
	A[Interfaz Usuario] --> B
	B[API Layer] --> C
	B --> D
	B --> E
	C[Servicio 1] --> F
	D[Servicio 2] --> F
	E[Servicio N] --> F
	F[Base de datos]
```

- Separación de dominio
```mermaid
graph TD
	A[Interfaz Usuario] --> C
	A --> D
	B[Interfaz Usuario] --> E
	B --> F
	C[Servicio 1] --> G
	D[Servicio 2] --> G
	E[Servicio 3] --> G
	F[Servicio 4] --> G
	G[Base de datos]
```

- Separación por servicio y dominio
```mermaid
graph TD
	A[Interfaz Usuario] --> C
	A --> D
	B[Interfaz Usuario] --> E
	B --> F
	C[Servicio 1] --> G
	D[Servicio 2] --> G
	E[Servicio 3] --> G
	F[Servicio 4] --> H
	G[Base de datos]
	H[Base de datos]
```

---

**Granularidad en los servicios:**

A diferencia de [[Microservice]], aquí los **Servicios** son mas grandes por la necesidad de abarcar una funcionalidad completa de dominio.

La [[Topología]] de estos puede ser:

**Por Capas:**
```mermaid
graph TD
	A[Capa de API] --> B
	B[Capa de negocio] --> C[Capa de persistencia]
```
**Por Dominio:**
```mermaid
graph TD
	A[Capa de API] --> B
	A[Capa de API] --> D
	B[Componente] --> C[Componente]
	D[Componente] --> E[Componente]
```
---
**Consideraciones**
Por la naturaleza de este [[Estilo arquitectónico]] puede darse que la Base de datos se corrompa, para evitar esto es recomendable realizar una partición de la base de datos, desarrollar una interfaz común para todos los servicios y adicional desarrollar interfaces especificas para que cada servicio, dependiendo de sus necesidades, pueda acceder a alguna de las particiones de escritura o lectura, como en los siguientes diagramas:

**Sin Particionamiento:**
```mermaid
graph TD
	A[Capa de API] --> B
	A[Capa de API] --> C
	A[Capa de API] --> D
	B[Servicio 1] --> E
	C[Servicio 2] --> E
	D[Servicio N] --> E
	E[Unica biblioteca DB] --> F[Base de datos]
```

**Con Particionamiento:**
```mermaid
graph TD
	A[Capa de API] --> B
	A[Capa de API] --> C
	A[Capa de API] --> D
	B[Servicio 1] --> E
	C[Servicio 2] --> F
	D[Servicio N] --> G
	E[Biblioteca Compartida DB] --> J
	F[Biblioteca Compartida DB] --> H
	G[Biblioteca Compartida DB] --> I
	H[Ext2 Biblioteca DB] --> J
	I[ExtN Biblioteca DB] --> J
	J[Base de datos con particiones]
```

---

Se recomienda ocuparlo cuando:
- Proyecto de largo plazo y la mantenibilidad es importante
- Modernización de monolitos o sistemas legacy
- Reutilización e interoperabilidad de componentes
- Cuando el diseño del sistema esta basado en el dominio
- Cuando la modularidad tiene mayor relevancia que la granularidad

No se recomienda ocuparlo cuando:
- Proyectos pequeños o de corta duración
- Experiencia limitada en esta arquitectura
- Requerimiento no requieren ser desacoplados
- Consistencia de datos en "tiempo real"