```json
{
    "name": "foo.com",
    "ns": [
      "ns1.example.com",
      "ns2.example.net"
    ],
    "status": [
      {
        "name": "ok"
      },
      {
        "name": "clientTransferProhibited"
      },
      {
        "name": "serverRenewProhibited"
      }
    ],
    "authInfo": {
      "value": "oldauth"
    },
    "registrant": "blah"
}
```

```json
{
  "add": {
    "ns": [
      "ns1.foo.example",
      "ns2.foo.example"
    ],
    "foo": "xxx",
    "contact": [
      {
        "type": "techc",
        "value": "123456"
      }
    ],
    "status": [
      {
        "name": "clientHold"
      }
    ]
  },

  "remove": {
    "ns": [
      "ns1.example.com",
      "ns2.example.net"
    ]
  },

  "change": {
    "authInfo": {
      "value": "newauthcode"
    }
  }
}
```

```json
-- an existing key is a full replacement
{
    "ns": [
      "ns1.foo.example",
      "ns2.foo.example"
    ],
}
```

```json
-- an existing key is a full replacement
{
    "foo": null,
    "ns": [
    ]
}
```

{
    -- generalisation based on data objects 
    "remove": {
        ... allowed for elements with cardinality different than 1 (mandatory properties)
        ... allowed for arrays to remove single elements, as long as the array in result won't break constraints
        ... allowed for items which are read-writew
    },
    "add": {
        
        ... allowed for items which are read-write
    },
    "change": {
        
        ... allowed for items which are read-write
    }
}

## Simple values (primitive)
```
{
    "foo": "value"
}
```

## Component Objects
... same as any object composition?

## Composition
Cardinatily 1 or 0-1
```
{
    "foo": {
        ...
    }
}
```

Cardinatily 1+ or 0+
```
{
    "foo": [{
        ...
    }]
}
```


## Composition Dictionary
Cardinatily 1 or 0-1
... same as below but does not make too much sense

Cardinatily 1+ or 0+
```
{
    "foo": {
        "label1" {
            ...
        },
        "label2" {
            ...
        },
        ...
    }
}
```

## Labelled Composition
Cardinatily 1 or 0-1
... same as below but does not make too much sense

Cardinatily 1+ or 0+
```
{
    "contacts": [
        {
            "label": "adminc",
            "object: {
                "handle_id": "..."
            }
        },
        {
            "label": "adminc",
            "object: {
                "handle_id": "..."
            }
        },
        ...
    ]
}
```
