GEN-CERT
=====

Utility shell to generate self-signed certificates such as CA, server, peer and client using [cfssl](https://github.com/cloudflare/cfssl).

### Usage
```
$ gen-cert --help
USAGE: gen-cert [options]
DESCRIPTION: Utility to generate different self-signed certificates: CA, server or peer and client using CFSSL.
OPTIONS:
    -a, --all                           : generate all certificates: CA, server, client.
    --type <ca,server,client,all>       : generate the specified certificate type. If the options corresponding to each type are not specified, it will use the default ones. Mandatory. Default: all.
    --ca-name <name>                    : name for generated CA certificates. Default: ca.
    --ca-csr-config <path>              : specify CA CSR config file. Default: ca-csr.json.
    --ca-config <path>                  : specify CA config file. Optional. Default: ca.json
    --ca-key <path>                     : specify the existing CA key. Default: ca-key.pem
    --ca-cert <path>                    : specify the existing CA certificate. Default: ca.pem
    --server-name <name>                : name for generated server certificates. Default: server.
    --server-config <path               : specify server config file. Default: server.json
    --client-name <name>                : name for generated client certificates. Default: client.
    --client-config <path               : specify client config file. Default: client.json
    -h,--help                           : show this message
```

To generate certificates, `gen-cert` uses different configuration files specified by the options: `--ca-csr-config`, `--ca-config`, `--server-config` and `--client-config`. If an option is not set, `gen-cert` uses its default value.

### Examples

**Generate all certificates:**
```
$ cd examples
$ gen-cert -t all
```
or
```
$ gen-cert -t all --ca-csr-config ./example/ca-csr.json --ca-config ./example/ca.json --server-config ./example/server.json --client-config ./example/client.json
```

**Generate CA certificate**
```
$ gen-cert -t ca --ca-name CA --ca-csr-config ./example/ca-csr.json
```

**Generate server certificate**
```
$ gen-cert -t server --server-name SERVER --ca-config ./example/ca.json --ca-key CA-key.pem --ca-cert CA.pem --server-config ./example/server.json
```

**Generate client certificate**
```
$ gen-cert -t client --client-name CLIENT --ca-config ./example/ca.json --ca-key CA-key.pem --ca-cert CA.pem --client-config ./example/client.json
```




