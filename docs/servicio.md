# Descripción del servicio

## Resumen

El servicio de estaciones climáticas de DePeru.com expone un endpoint JSON con la fecha de inicio de cada estación del año en Perú. La respuesta de ejemplo presenta un objeto por año y una estructura de temporada con información horaria, fechas y texto descriptivo.

## Enlaces

- Portal: https://www.deperu.com/clima/
- Endpoint: https://deperu.com/api/rest/estaciones.json
- Contacto: https://deperu.com/contacto

## Propiedades conocidas

- Nombre: Estaciones del Perú
- Fuente: DePeru.com
- Formato observado: JSON
- Estructura: `año > estación > propiedades`
- Estaciones observadas: `Otoño`, `Invierno`, `Primavera`, `Verano`

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
    }
  }
}
```

## Estructura observada

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `2026` | Objeto | Año principal |
| `Otoño` | Objeto | Nombre de la estación |
| `horaInicio` | Cadena | Hora de inicio |
| `diaInicio` | Cadena | Día de inicio |
| `mesInicio` | Cadena | Mes de inicio |
| `fechaInicio` | Cadena | Fecha completa con formato `DD-MM-YYYY` |
| `textoInicio` | Cadena | Descripción legible en español |
| `fechaFinal` | Cadena | Fecha final de la estación |

## Consideraciones

- La estructura puede cambiar sin previo aviso.
- La fecha se observa como cadena con formato `DD-MM-YYYY`.
- Antes de mostrar la información en una interfaz, valida que los campos existan.
