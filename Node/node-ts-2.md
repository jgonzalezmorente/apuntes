# Node con TypeScript - TSX + NodeNext

## 1. Inicializar el proyecto

```bash
npm init -y
```

---

## 2. Instalar dependencias de desarrollo

```bash
npm i -D typescript @types/node tsx rimraf
```

---

## 3. Inicializar TypeScript

```bash
npx tsc --init
```

---

## 4. Configurar `tsconfig.json`

```json
{
  "exclude": ["node_modules", "dist"],
  "include": ["src/**/*"],
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist",

    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "target": "ES2022",
    "lib": ["ES2022"],
    "types": ["node"],

    "sourceMap": true,
    "declaration": true,
    "declarationMap": true,

    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,

    "verbatimModuleSyntax": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "skipLibCheck": true
  }
}
```

---

## 5. Configurar `package.json`

Añadir `"type": "module"` y los scripts:

```json
{
  "type": "module",
  "scripts": {
    "dev": "tsx watch src/app.ts",
    "build": "rimraf dist && tsc",
    "start": "node dist/app.js"
  }
}
```

---

## 6. Estructura recomendada

```txt
src/
 ├── app.ts
 └── presentation/
      └── server.ts
```

---

## 7. Ejemplo de `src/app.ts`

```ts
import { Server } from "./presentation/server.js";

(async() => {
    main();
})();


function main() {
    Server.start();
}
```

---

## 8. Ejemplo de `src/presentation/server.ts`

```ts
export class Server {
  static start() {
    console.log('Server started...');
  }
}
```

---

## 9. Imports en NodeNext

Con `NodeNext`, en imports relativos se usa extensión `.js`:

```ts
import { Server } from "./presentation/server.js";
```

Aunque el archivo real sea:

```txt
server.ts
```

Esto es normal en ESM moderno, porque el código compilado acabará siendo:

```txt
dist/presentation/server.js
```

---

## 10. Ejecutar en desarrollo

```bash
npm run dev
```

---

## 11. Compilar

```bash
npm run build
```

---

## 12. Ejecutar en producción

```bash
npm start
```

---

## 13. Ventajas frente a `ts-node-dev`

- Mejor soporte para ES Modules.
- Compatible con `NodeNext`.
- Menos problemas con `import` / `export`.
- Arranque rápido.
- Configuración más simple.
- Más alineado con Node moderno.