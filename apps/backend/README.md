# Backend

A basic Node.js backend built with Express and TypeScript.

## Getting Started

### Development

```bash
npm run dev
```

The server will start on `http://localhost:3000` (or the port specified in the `PORT` environment variable).

### Build

```bash
npm run build
```

### Production

```bash
npm start
```

## API Endpoints

- `GET /` - Welcome message
- `GET /health` - Health check endpoint

## Scripts

- `dev` - Start development server with hot reload
- `build` - Build the TypeScript code
- `start` - Start the production server
- `lint` - Run ESLint
- `check-types` - Type check without emitting files
