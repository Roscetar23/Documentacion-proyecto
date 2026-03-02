# Setup Instructions - TypeScript, Jest, ESLint & Prettier

## Instalación de Dependencias

Ejecuta los siguientes comandos para instalar todas las dependencias necesarias:

### 1. TypeScript y tipos
```bash
npm install --save-dev typescript @types/react @types/react-native @types/jest
```

### 2. ESLint y plugins
```bash
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-react-native
```

### 3. Prettier y integración con ESLint
```bash
npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
```

### 4. Testing con TypeScript
```bash
npm install --save-dev @testing-library/react-native @testing-library/jest-native @types/react-test-renderer ts-jest
```

### 5. Husky para pre-commit hooks
```bash
npm install --save-dev husky
npx husky install
chmod +x .husky/pre-commit
```

### 6. Fast-check (ya instalado)
El proyecto ya tiene `fast-check` instalado para property-based testing.

## Verificación de la Configuración

Después de instalar las dependencias, verifica que todo funciona:

```bash
# Verificar TypeScript
npm run type-check

# Verificar ESLint
npm run lint

# Verificar Prettier
npm run format:check

# Ejecutar tests
npm test
```

## Comandos Disponibles

- `npm run type-check` - Verifica tipos de TypeScript sin compilar
- `npm run lint` - Ejecuta ESLint
- `npm run lint:fix` - Ejecuta ESLint y corrige automáticamente
- `npm run format` - Formatea código con Prettier
- `npm run format:check` - Verifica formato sin modificar archivos
- `npm test` - Ejecuta todos los tests
- `npm run test:coverage` - Ejecuta tests con reporte de cobertura

## Configuración del Editor

### VS Code
Instala las siguientes extensiones:
- ESLint
- Prettier - Code formatter
- TypeScript and JavaScript Language Features (incluido por defecto)

Agrega a tu `.vscode/settings.json`:
```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

## Notas Importantes

1. **Path Aliases**: El proyecto está configurado con alias `@/` que apunta a `src/`
   - Ejemplo: `import { User } from '@/types/entities'`

2. **Coverage Thresholds**: Los módulos core requieren 80% de cobertura
   - `src/services/gamification/**`
   - `src/stores/**`

3. **Pre-commit Hook**: Antes de cada commit se ejecutan:
   - Type checking
   - Linting
   - Format checking
   - Tests relacionados

4. **Strict Mode**: TypeScript está configurado en modo estricto
   - No se permite `any` explícito
   - Todas las variables deben tener tipos

## Solución de Problemas

### Error: "Cannot find module '@/...'"
- Asegúrate de que `tsconfig.json` tiene configurado el path alias
- Reinicia el servidor de TypeScript en tu editor

### Error en pre-commit hook
- Verifica que el archivo `.husky/pre-commit` tiene permisos de ejecución
- En Windows, puede que necesites configurar Git bash

### Tests fallan con módulos de Expo
- Verifica que `jest.setup.js` tiene los mocks necesarios
- Asegúrate de que `transformIgnorePatterns` incluye los módulos de Expo
