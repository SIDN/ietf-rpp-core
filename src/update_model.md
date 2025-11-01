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
        ... allowed for items which are clearly identified by a label, but not by value
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


# add

-- preconditions
-- cardinality 0-1
-- it's not yet set
## Simple values (primitive)
```
{
    "foo": "value"
}
```

-- preconditions
-- cardinality 0-1
-- it's not yet set
## Composition
```
{
    "foo": {
        ...
    }
}
```

-- Cardinatily 1+ or 0+
-- semantics: if element does not exist, add it
  -- add all elements to the existing array
```
{
    "foo": [{
        ...
    },
    {
        ...
    }
    ]
}
```

## Composition Dictionary

-- Cardinatily 1+ or 0+
-- add labels
-- fail if label already exist
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
--Cardinatily 1+ or 0+
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


# remove

-- preconditions
-- cardinality 0-1
## Simple values (primitive)
```
{
    "foo": null
}
```

-- preconditions
-- cardinality 0-1
## Composition
```
{
    "foo": null
}
```

-- preconsitions
-- remove all items matching the provided values (recourse same generic alg. over all values)
```
{
    "foo": [{
        "...": "xxxx"
    },
    {
        "...": "xxxx"        
    }
    ]
}
```

## Composition Dictionary

-- Cardinatily 1+ or 0+
-- remove all labels
-- fail if label does not exist exist
```
{
    "foo": {
        "label1": null
        "label2": null,
        ...
    }
}
```

## Labelled Composition
--Cardinatily 1+ or 0+
-- remove all items matching the provided values (recourse same generic alg. over all values)
```json
{
    "contacts": [
        {
            "label": "adminc",
            "object": {
                "...": "..."
            }
        },
        {
            "label": "adminc",
            "object": {
                "...": "..."
            }
        },
        ...
    ]
}
```


# change

-- preconditions
-- cardinality 1 or 0-1
## Simple values (primitive)
```
{
    "foo": "value"
}
```

-- preconditions
-- cardinality 1 or 0-1
## Composition
```
{
    "foo": {
        ...
    }
}
```

-- Cardinatily 1+ or 0+
-- forbidden, do remove and add

## Composition Dictionary

-- Cardinatily 1+ or 0+
-- full replace labels ???
-- fail if label does not exist
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
--Cardinatily 1+ or 0+
-- forbidden, just do remove and add

--- examples

```json
{
    "status": [
      {
        "name": "ok"
      },
      {
        "name": "clientTransferProhibited",
        "reason": "Abuse lock",
        "tags": [
            "foo",
            "bar"
        ]
      },
      {
        "name": "clientTransferProhibited",
        "reason": "registrar Lock",
        "tags": [
            "foo"
        ]
      },
      {
        "name": "serverRenewProhibited"
      }
    ]
}


{
    "remove": {
        "status": [
            {
                "name": "clientTransferProhibited",
                "tags": [
                    "foo"
                ]
            }
        ]
    }
}
```

```json
{
    "remove": {
        "contacts": [
            {
                "label": "techc",
                "object: {
                    "id": "1234"
                }
            }
        ]
    }
}
```