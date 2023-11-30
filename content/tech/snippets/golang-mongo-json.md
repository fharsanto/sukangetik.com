---
title: "Golang Mongo"
date: 2023-11-30T18:25:14+07:00
# draft: true
categories: ["tech/snippets"]
tags: ["snippets", "golang"]
---

## Handle MongoDB Collection intermitten between String and Embedded Document
```go
func (a *Address) UnmarshalBSONValue(t bsontype.Type, data []byte) error {
	if s, _, ok := bsoncore.ReadString(data); ok {
		a.Address = s
		return nil
	}

	if t != bson.TypeEmbeddedDocument {
		return fmt.Errorf("expected embedded document, got BSON type: %v", t)
	}

	var doc bson.D
	if err := bson.Unmarshal(data, &doc); err != nil {
		return fmt.Errorf("error unmarshaling embedded document: %v", err)
	}

	for _, elem := range doc {
		switch elem.Key {
        // List down the sub field, if Neeed to read
		case "address":
			a.Address = elem.Value.(string)
		case "kec":
			a.Kec = elem.Value.(string)
		case "kel":
			a.Kel = elem.Value.(string)
		}
	}
	return nil
}
```

## Handle Document value datetime or string
```go
func (cd *CustomDate) UnmarshalBSONValue(t bsontype.Type, data []byte) error {
	if s, _, ok := bsoncore.ReadDateTime(data); ok {
		ts := time.Unix(s/1000, 0).Format(time.RFC3339)
		cd.Value = ts
		return nil
	}

	if s, _, ok := bsoncore.ReadString(data); ok {
		cd.Value = s
	}
	return nil
}
```

## Handle JSON decode with strip field
Source
```json
{
    "date": {
        "Value": "2020-01-11T12:00:11"
    }
}
```
To
```json
{
    "date": "2020-01-11T12:00:11"
}
```

```go
func (cd CustomDate) MarshalJSON() ([]byte, error) {
	return json.Marshal(cd.Value)
}
```