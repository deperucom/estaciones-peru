# Guía técnica de uso

Esta guía muestra cómo consultar el endpoint desde una aplicación. La URL documentada es:

```text
https://deperu.com/api/rest/estaciones.json
```

El ejemplo disponible indica que el servicio devuelve las estaciones del año por año y por temporada. Ejecuta los ejemplos desde un entorno autorizado y evita llamadas innecesarias.

## User-Agent personalizado

Se recomienda enviar un encabezado `User-Agent` que identifique el dominio o nombre de la aplicación cliente y su versión. Ejemplo:

```http
User-Agent: GuiaPlaza.com_Estaciones/1.0
```

Reemplaza este valor por el nombre de tu app o dominio real.

## cURL

```bash
curl --fail --silent --show-error \
  --max-time 10 \
  --user-agent 'GuiaPlaza.com_Estaciones/1.0' \
  https://deperu.com/api/rest/estaciones.json
```

## Python

```python
import json
from urllib.error import HTTPError, URLError
from urllib.request import Request, urlopen

URL = "https://deperu.com/api/rest/estaciones.json"
USER_AGENT = "GuiaPlaza.com_Estaciones/1.0"

request = Request(
    URL,
    headers={
        "Accept": "application/json",
        "User-Agent": USER_AGENT,
    },
)

try:
    with urlopen(request, timeout=10) as response:
        data = json.loads(response.read().decode("utf-8"))
except HTTPError as error:
    raise SystemExit(f"El servidor respondió HTTP {error.code}") from error
except (URLError, TimeoutError) as error:
    raise SystemExit(f"No se pudo consultar el servicio: {error}") from error
except json.JSONDecodeError as error:
    raise SystemExit(f"La respuesta no contiene JSON válido: {error}") from error

for anio, estaciones in data.items():
    print(f"Año: {anio}")
    for nombre, info in estaciones.items():
        print(f"- {nombre}: {info.get('textoInicio')} ({info.get('fechaInicio')})")
```

## PHP

```php
<?php
$url = 'https://deperu.com/api/rest/estaciones.json';
$userAgent = 'GuiaPlaza.com_Estaciones/1.0';
$curl = curl_init($url);

curl_setopt_array($curl, [
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CONNECTTIMEOUT => 5,
    CURLOPT_TIMEOUT => 10,
    CURLOPT_USERAGENT => $userAgent,
    CURLOPT_HTTPHEADER => ['Accept: application/json'],
]);

$body = curl_exec($curl);
$status = curl_getinfo($curl, CURLINFO_HTTP_CODE);
$error = curl_error($curl);
curl_close($curl);

if ($body === false) {
    throw new RuntimeException("Error de conexión: {$error}");
}
if ($status < 200 || $status >= 300) {
    throw new RuntimeException("El servidor respondió HTTP {$status}");
}

$data = json_decode($body, true);
if (!is_array($data) || json_last_error() !== JSON_ERROR_NONE) {
    throw new RuntimeException('La respuesta no contiene JSON válido.');
}

foreach ($data as $anio => $estaciones) {
    echo "Año: {$anio}\n";
    foreach ($estaciones as $nombre => $info) {
        echo "- {$nombre}: {$info['textoInicio']} ({$info['fechaInicio']})\n";
    }
}
```

## Node.js

```js
const url = "https://deperu.com/api/rest/estaciones.json";
const userAgent = "GuiaPlaza.com_Estaciones/1.0";

async function main() {
  let response;
  try {
    response = await fetch(url, {
      headers: {
        Accept: "application/json",
        "User-Agent": userAgent,
      },
      signal: AbortSignal.timeout(10_000),
    });
  } catch (error) {
    throw new Error(`No se pudo consultar el servicio: ${error.message}`);
  }

  if (!response.ok) {
    throw new Error(`El servidor respondió HTTP ${response.status}`);
  }

  let data;
  try {
    data = await response.json();
  } catch {
    throw new Error("La respuesta no contiene JSON válido.");
  }

  for (const [anio, estaciones] of Object.entries(data)) {
    console.log(`Año: ${anio}`);
    for (const [nombre, info] of Object.entries(estaciones)) {
      console.log(`- ${nombre}: ${info.textoInicio} (${info.fechaInicio})`);
    }
  }
}

main().catch((error) => {
  console.error(error.message);
  process.exitCode = 1;
});
```

## Java

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;

public class EstacionesPeru {
    public static void main(String[] args) throws Exception {
        var client = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(5))
                .build();
        var request = HttpRequest.newBuilder()
                .uri(URI.create("https://deperu.com/api/rest/estaciones.json"))
                .timeout(Duration.ofSeconds(10))
                .header("Accept", "application/json")
                .header("User-Agent", "GuiaPlaza.com_Estaciones/1.0")
                .GET()
                .build();

        var response = client.send(request, HttpResponse.BodyHandlers.ofString());
        if (response.statusCode() < 200 || response.statusCode() >= 300) {
            throw new IllegalStateException("El servidor respondió HTTP " + response.statusCode());
        }

        System.out.println(response.body());
    }
}
```

## Manejo de respuesta y errores

- Comprueba el código HTTP antes de interpretar el cuerpo.
- Usa timeout para evitar bloqueos indefinidos.
- Valida que el JSON tenga la estructura esperada: año → estación → propiedades.
- Verifica campos de fecha y texto antes de presentarlos en una interfaz.
- Identifica la app con un User-Agent claro, como `GuiaPlaza.com_Estaciones/1.0`.

## Frecuencia y caché

No se especifica una frecuencia de actualización en la documentación disponible. Por ello, se recomienda no consultar demasiado a menudo y almacenar los datos en caché si se usan en una aplicación pública o web.
