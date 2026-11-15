# Restricciones y políticas del servicio

## Acceso geográfico

El servicio puede estar restringido a direcciones IP del Perú. Si tu app se despliega fuera del país, es posible que necesites una validación extra o un entorno con IP autorizada.

## Rate limiting

No se especifica un límite de solicitudes en la información disponible. Se recomienda no hacer polling agresivo ni consultas masivas sin una razón clara.

## Buenas prácticas

- Usar un `User-Agent` personalizado para identificar la app o sitio.
- Guardar en caché la respuesta si la usas repetidamente.
- Evitar loops de consultas y consultar solo cuando sea necesario.
- Validar la estructura del JSON antes de procesarlo.

## Importante

La información aquí documentada es informativa y se basa en la respuesta de ejemplo observada. La disponibilidad y el formato pueden variar; la fuente oficial es DePeru.com.
