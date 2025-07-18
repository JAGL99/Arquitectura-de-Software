Se caracteriza por la independencia de cada uno de los **Servicios**, los cuales son gestionados por una API que los manda a ejecutar dependiendo de las peticiones de los clientes.
Los **Servicios** deben ser lo mas acotados posibles 

[[Topología]]:
```mermaid
graph TD
	A[Cliente 1] --> D
	B[Cliente 2] --> D
	C[Cliente N] --> D
	D[API] --> E
	D[API] --> F
	D[API] --> G
	E[Servicio 1]
	subgraph E[Servicio 1]
        E1[Capa 1]
        E2[Capa 2]
        E3[DB]
    end
	F[Servicio 2]
	subgraph F[Servicio 2]
        F1[Capa 1]
        F2[Capa 2]
        F3[DB]
    end
	G[Servicio N]
	subgraph G[Servicio N]
        G1[Capa 1]
        G2[Capa 2]
        G3[DB]
    end
```

Se recomienda ocuparla:
- Cuando el dominio cambia muy rapido
- Cuando la tolerancia al fallo sea MUY importante
- Cuando la modularidad sea importante
- Cuando la reusabilidad sea importante
- Cuando quieras evolucionar partes independietes del software

No se recomienda ocuparla:
- Cuando los recursos sean escasos
- Cuando quieras una arquitectura simple
- Cuando el rendimiento sea MUY importante