# nestjs-with-https

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
