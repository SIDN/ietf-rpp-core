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

EPP UPDATE model
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

Attempts to model PATCH without add/remove/change logic:
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
... both will offer serious limitations!

```json
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
```
# Analysis of approaches based on type of relations and expressions in Data Objects

## Example modelling (before change)

### Simple values (primitive)
```json
{
    "foo": "value"
}
```

### Component Objects
... same as any object composition?

### Composition
Cardinatily 1 or 0-1
```json
{
    "foo": {
        ...
    }
}
```

Cardinatily 1+ or 0+
```json
{
    "foo": [{
        ...
    }]
}
```


### Composition Dictionary
Cardinatily 1 or 0-1
... same as below but does not make too much sense

Cardinatily 1+ or 0+
```json
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

### Labelled Composition
Cardinatily 1 or 0-1
... same as below but does not make too much sense

Cardinatily 1+ or 0+
```json
{
    "contacts": [
        {
            "label": "adminc",
            "object": {
                "handle_id": "..."
            }
        },
        {
            "label": "adminc",
            "object": {
                "handle_id": "..."
            }
        },
        ...
    ]
}
```


## add

-- preconditions
-- cardinality 0-1
-- it's not yet set
### Simple values (primitive)
```json
{
    "add": {
        "foo": "value"
    }
}
```

-- preconditions
-- cardinality 0-1
-- it's not yet set
### Composition
```json
{
    "add": {
        "foo": {
            ...
        }
    }
}
```

-- Cardinatily 1+ or 0+
-- semantics: if element does not exist, add it
  -- add all elements to the existing array
```json
{
    "add": {
        "foo": [
            {
                ...
            },
            {
                ...
            }
        ]
    }
}
```

### Composition Dictionary

-- Cardinatily 1+ or 0+
-- add labels
-- fail if label already exist
```json
{
    "add": {
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
}
```

### Labelled Composition
--Cardinatily 1+ or 0+
```json
{
    "foo": {
        "contacts": [
            {
                "label": "adminc",
                "object": {
                    "handle_id": "..."
                }
            },
            {
                "label": "adminc",
                "object": {
                    "handle_id": "..."
                }
            },
            ...
        ]
    }
}
```


## remove

-- preconditions
-- cardinality 0-1
### Simple values (primitive)
```json
{
    "remove": {
        "foo": null
    }
}
```

-- preconditions
-- cardinality 0-1
### Composition
```json
{
    "remove": {
        "foo": null
    }
}
```

-- preconsitions
-- remove all items matching the provided values (recourse same generic alg. over all values)
```json
{
    "remove": {
        "foo": [
            {
                "...": "xxxx"
            },
            {
                "...": "xxxx"        
            }
        ]
    }
}
```

### Composition Dictionary

-- Cardinatily 1+ or 0+
-- remove all labels
-- fail if label does not exist exist
```json
{
    "remove": {
        "foo": {
            "label1": null
            "label2": null,
            ...
        }
    }
}
```

### Labelled Composition
--Cardinatily 1+ or 0+
-- remove all items matching the provided values (recourse same generic alg. over all values)
```json
{
    "remove": {
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
}
```


## change

-- preconditions
-- cardinality 1 or 0-1
### Simple values (primitive)
```json
{
    "change": {
        "foo": "value"
    }
}
```

-- preconditions
-- cardinality 1 or 0-1
### Composition
```json
{
    "change": {
        "foo": {
            ...
        }
    }
}
```

-- Cardinatily 1+ or 0+
-- forbidden, do remove and add

### Composition Dictionary

-- Cardinatily 1+ or 0+
-- full replace labels ???
-- fail if label does not exist
```json
{
    "change": {
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
}
```


### Labelled Composition
--Cardinatily 1+ or 0+
-- forbidden, just do remove and add

# examples

Input
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
```

Example to remove based on matching of name and tag
```json
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

Example remove based on match of label and object's property id (can be literalily any property)
```json
{
    "remove": {
        "contacts": [
            {
                "label": "techc",
                "object": {
                    "id": "1234"
                }
            }
        ]
    }
}
```
