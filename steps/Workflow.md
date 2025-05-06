# Configuración de GitHub Actions

1. En la raíz del proyecto, crea la ruta `.github/workflows/`.
2. Dentro, crea el archivo `test_calculator.yml`.
3. Copia y pega el contenido del workflow YAML proporcionado.
4. Haz commit y push de los cambios.

## ¿Qué hace este workflow?

- Instala Node.js y dependencias.
- Ejecuta las pruebas usando Node.
- Genera un archivo `test-results.txt` con los resultados.
- Carga el archivo como artefacto que puedes descargar desde la pestaña "Actions" de GitHub.

Código

```
name: Run Tests and Upload Artifact

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: Install dependencies
        run: npm install

      - name: Run tests and generate report
        run: node test/calculator.test.js

      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: test-results
          path: results/test-results.txt
```