# NestJS with HTTPS

## Installation

To install the necessary dependencies for this project, run the following command:

```sh
npm install
```

Next, install `mkcert` using `choco`. You can find more information about `mkcert` on its [Cert Official Github page](https://github.com/FiloSottile/mkcert).

```sh
choco install mkcert
```

After that, install the local CA:

```sh
mkcert -install
```

A local CA (Certificate Authority) is a trusted entity that issues digital certificates for securing communications within a local network or development environment.

Then, create the `cert` folder:

```sh
mkdir -p src/cert # if you don't have the src/cert directory
```

Next, create two certificate files and secure the domain:

```sh
mkcert -key-file ./src/cert/key.pem -cert-file ./src/cert/cert.pem localhost
```

The `key.pem` file contains the private key, and the `cert.pem` file contains the public certificate. These files are used to establish a secure HTTPS connection for the `localhost` domain.

## Config and Running

### Config

Next, configure the `main.ts` file as follows:

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as fs from 'fs';

async function bootstrap() {
  const httpsOptions = {
    key: fs.readFileSync('./src/cert/key.pem'),
    cert: fs.readFileSync('./src/cert/cert.pem'),
  };

  const app = await NestFactory.create(AppModule, { httpsOptions });

  await app.listen(3000);
}

bootstrap();
```

#### Explanation of Some Commands:

- `fs.readFileSync('./src/cert/key.pem')`: Reads the content of the `key.pem` file containing the private key.
- `fs.readFileSync('./src/cert/cert.pem')`: Reads the content of the `cert.pem` file containing the public certificate.
- `NestFactory.create(AppModule, { httpsOptions })`: Creates a NestJS application with HTTPS configuration.
- `app.listen(3000)`: Listens for HTTPS connections on port 3000.

### Running

Finally, run the project with the command:

```sh
npm run start
```

and access the page at [https://localhost:3000](https://localhost:3000)
