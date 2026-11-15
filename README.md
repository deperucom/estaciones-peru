# Estaciones del Perú — API de DePeru.com

Repositorio informativo sobre el servicio de estaciones climáticas del Perú publicado por [DePeru.com](https://www.deperu.com) y su endpoint JSON. Reúne la URL del servicio, el formato de respuesta observado, las restricciones de acceso y ejemplos sencillos para consultar la información desde distintas plataformas.

> **Este repositorio no es la API ni está afiliado oficialmente a DePeru.com.** Los datos y el servicio son proporcionados por DePeru.com. Consulta el sitio original para verificar la información más reciente.

## Enlaces

- **Portal del clima:** https://www.deperu.com/clima/
- **Endpoint JSON:** https://deperu.com/api/rest/estaciones.json
- **Contacto DePeru.com:** https://deperu.com/contacto

## ¿Qué ofrece el servicio?

El endpoint devuelve la información de inicio de cada estación del año en Perú, con hora, día, mes, fechas y descripciones textuales. El formato observado incluye la temporada, la hora de inicio y la fecha de inicio en formato `DD-MM-YYYY`.

### Características conocidas

| Propiedad | Detalle |
| --- | --- |
| Servicio | Estaciones climáticas del Perú |
| Fuente | DePeru.com |
| Formato observado | JSON |
| Periodicidad | Datos estructurados por año, según el ejemplo disponible |
| Restricción geográfica | El proveedor indica que el acceso puede estar restringido a IPs del Perú |
| Límite de solicitudes | No especificado en la información disponible |

## Ejemplo de respuesta

```json
{
  "2026": {
    "Otoño": {
      "horaInicio": "09:46",
      "diaInicio": "20",
      "mesInicio": "3",
      "fechaInicio": "20-3-2026",
      "textoInicio": "20 de Marzo de 2026",
      "fechaFinal": "21-6-2026"
    },
    "Invierno": {
      "horaInicio": "03:24",
      "diaInicio": "21",
      "mesInicio": "6",
      "fechaInicio": "21-6-2026",
      "textoInicio": "21 de Junio de 2026",
      "fechaFinal": "22-9-2026"
    },
    "Primavera": {
      "horaInicio": "19:05",
      "diaInicio": "22",
      "mesInicio": "9",
      "fechaInicio": "22-9-2026",
      "textoInicio": "22 de Setiembre de 2026",
      "fechaFinal": "21-12-2026"
    },
    "Verano": {
      "horaInicio": "15:50",
      "diaInicio": "21",
      "mesInicio": "12",
      "fechaInicio": "21-12-2026",
      "textoInicio": "21 de Diciembre de 2026",
      "fechaFinal": "20-3-2027"
    }
  }
}
```

El ejemplo es ilustrativo y puede variar según el año. La estructura presenta un objeto principal por año (`"2026"`) y dentro de este, los nombres de las estaciones: `Otoño`, `Invierno`, `Primavera` y `Verano`.

## Identifica tu aplicación con User-Agent

Se recomienda enviar un encabezado `User-Agent` personalizado en las solicitudes. Incluye el dominio o nombre de la aplicación que consulta los datos y, de ser posible, su versión. Ejemplo:

```http
User-Agent: GuiaPlaza.com_Estaciones/1.0
```

Sustituye el valor por el dominio o nombre de tu propio sitio o aplicación. No uses un identificador genérico que no te pertenezca.

## Consulta rápida

Desde una IP permitida, puedes probar con `curl` y un User-Agent identificable:

```bash
curl --fail --silent --show-error \
  --max-time 10 \
  --user-agent 'GuiaPlaza.com_Estaciones/1.0' \
  https://deperu.com/api/rest/estaciones.json
```

Para ejemplos con manejo de errores en PHP, Python, Node.js y Java, consulta la [guía técnica](docs/guia-tecnica.md).

## Recomendaciones de consumo

- Envía un `User-Agent` que identifique tu dominio o aplicación y su versión.
- Valida la estructura del JSON antes de procesarlo: el ejemplo usa un objeto por año y temporada.
- Maneja errores de red, respuestas HTTP no exitosas y JSON inválido.
- Evita consultas repetitivas innecesarias; si necesitas información estática, almacénala en caché.
- Si el servicio está restringido a IPs del Perú, verifica que tu entorno cumpla esa condición.
- No asumas garantía de disponibilidad ni SLA del servicio.

## Uso responsable y atribución

Al mostrar los datos, conserva una atribución visible a **DePeru.com**. Si reutilizas la información en una app o sitio, considera enlazar a la fuente original y revisar términos de uso, si existen.

## Documentación

- [Guía técnica de uso: cURL, PHP, Python, Node.js y Java](docs/guia-tecnica.md)
- [Descripción del servicio y estructura de la respuesta](docs/servicio.md)
- [Restricciones y buenas prácticas](docs/limitaciones.md)

## Aviso

Este proyecto es informativo y se basa en la estructura observada del endpoint. El servicio puede cambiar su respuesta o políticas sin previo aviso; confirma con la fuente original antes de depender de él en producción.
