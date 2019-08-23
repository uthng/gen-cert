GEN-CERT
=====

Utility shell to generate self-signed certificates such as CA, server, peer and client using [cfssl](https://github.com/cloudflare/cfssl).

### Usage
```
$ gen-cert --help
USAGE: gen-cert [options]
DESCRIPTION: Utility to generate different self-signed certificates: CA, server or peer and client using CFSSL.
OPTIONS:
    -t, --type <ca,server,client,all>   : generate the specified certificate type. If the options corresponding to each type are not specified, it will use the default ones. Mandatory. Default: all.
    --ca-name <name>                    : name for generated CA certificates. Optional. Default: ca.
    --ca-csr-config <path>              : specify CA CSR config file. Optional. Default: ca-csr.json.
    --ca-config <path>                  : specify CA config file. Optional.
    --ca-key <path>                     : specify the existing CA key. Optional. Default: ca-key.pem.
    --ca-cert <path>                    : specify the existing CA certificate. Optional. Default: ca.pem.
    --server-name <name>                : name for generated server/peer certificates. Optional. Default: server.
    --server-config <path>              : specify server/peer config file. Optional. Default: server.json
    --server-profile <profile>          : profile defined in ca.json to use for server/peer. Optional.
    --client-name <name>                : name for generated client certificates. Optional. Default: client.
    --client-config <path>              : specify client config file. Default: client.json.
    --client-profile <profile>          : profile defined in ca.json to use for client. Optional.
    -h,--help                           : show this message.
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
$ DEBUG=1 gen-cert -t server --server-name SERVER --ca-config ./example/ca.json --ca-key CA-key.pem --ca-cert CA.pem --server-config ./example/server.json --server-profile server
```

**Generate client certificate**
```
$ gen-cert -t client --client-name CLIENT --ca-config ./example/ca.json --ca-key CA-key.pem --ca-cert CA.pem --client-config ./example/client.json
```




