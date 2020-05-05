# Encoding Contract Parameters in JSON

> insert intro about using JSON encoded ContractParameters in neo-express invoke files and launch.json for neo-debug 

## Current JSON encoding of Contract Parameters

Neo-core ContractParameter type has From/To JSON functions. These functions
encode a single contract parameter into a JSON object with the following shape:

> Note, these types are defined in TypeScript for readability.
> There is no requirement that this format be implemented in TypeScript.

``` typescript
// InteropInterface and Void ContractParameterTypes can not be specified in JSON
enum ContractParameterType {
    Signature,
    Boolean,
    Integer,
    Hash160,
    Hash256,
    ByteArray,
    PublicKey,
    String,
    Array,
    Map,
}

interface ContractParameter {
    type: ContractParameterType,
    value: boolean | string | ContractParameter[] | {key: ContractParameter, value: ContractParameter}[]
}
```

The specifics of the JSON encoded value field vary by parameter type:

* Boolean parameter values encoded as JSON bool
* String parameter values encoded as JSON string
* Signature and ByteArray parameter values are encoded as a hex string
* Integer, Hash160/256, Public Key are encoded as JSON string
* Array parameters are encoded as JSON array of encoded contract parameters
* Map parameter are encoded as a JSON array of objects, each with a "key" and "value" property containing an encoded contract parameter

While this encoding is complete and deterministic, it is also verbose. For example, here is the standard contract parameter encoding for invoking the register operation of the Domain Smart Contract example

``` json
[
    {
        "type": "String",
        "value": "register"
    },
    {
        "type": "Array",
        "value": [
            {
                "type": "String",
                "value": "neo.org"
            },
            {
                "type": "Hash160",
                "value": "7f513a2129dd800e1db8c2a57bc0873a021c9b7f"
            }
        ]
    }
]
```

To reduce verbosity and provide a better experience for developers that have to
author contract parameter JSON by hand, this design note proposes additional, compact
encodings of Contract Parameters.

## Direct JSON Encoded Parameters

In cases where there is a direct correlation of JSON type to Contract Parameter type, the
JSON type can be used directly instead of the more verbose type qualified format. The following
JSON types are treated as the corresponding Contract parameter type:

* Boolean
* Integer
  - Note, non-integer JSON numbers are not valid contract parameters
* String
* Array

The example from above is significantly simplified with direct encoding of
strings and arrays:

``` json
[
    "register",
    [
        "neo.org",
        {
            "type": "Hash160",
            "value": "7f513a2129dd800e1db8c2a57bc0873a021c9b7f"
        }
    ]
]
```

### String Encoded Parameters

* ByteArrays can be encoded as hex strings with the '0x' prefix
* Hash160 values can be encoded as base58 checked strings with the '@A'/'@N'
prefix. Note, the character after the ampersand indicates which version of
Neo the address is intended for ('A' is used by Neo v2, 'N' is used by Neo v3)

``` json
[
    "register",
    [
        "neo.org",
        "@ANxbzd4FuNr1BBMJX2ZixSzFKFWeFCReAb"
    ]
]
```

``` typescript
// ContractParameterType unchanged from above

interface TypeQualifiedContractParameter {
    type: ContractParameterType,
    value: bool | string | ContractParameter[] | ContractParameterMapElement[]
}

type ContractParameter = boolean | string | number | ContractParameter[] |t

interface TypeQualifiedContractParameter {
    type: ContractParameterType,
    value: boolean | string | ContractParameter[] | {key:ContractParameter, value: ContractParameter}[]
}

type ContractParameter =  boolean | string | number | ContractParameter[] | TypeQualifiedContractParameter;

```