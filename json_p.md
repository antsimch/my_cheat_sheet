# Json-P

## Create Generic Json Object
```ts
{
	AttributeName1: JsonObject / value,
	AttributeName2: JsonObject / value,
	AttributeName3: JsonObject / value,
	AttributeName4: JsonObject / value
}

```

```java
JsonObject obj = Json.createObjectBuilder()
		.add("AttributeName1", JsonObject / value)
		.add("AttributeName2", JsonObject / value)
		.add("AttributeName3", JsonObject / value)
		.add("AttributeName4", JsonObject / value)
		.build();
```

## Create Generic Json Array
```js
[
	JsonObject1,
	JsonObject2,
	JsonObject3,
	JsonObject4	
]
```

```java
JsonArray arr = Json.createArrayBuilder()
		.add(JsonObject1)
		.add(JsonObject2)
		.add(JsonObject3)
		.add(JsonObject4)
		.build();
```

## Create Json Object with Json Array as 1 of the attribute
```js
{
	AttributeName1: JsonObject,
	AttributeName2: JsonObject,
	AttributeName3: JsonObject,
	AttributeName4: [ JsonArrObject, … ]
}

JsonArrObject = {
	AttributeName1: JsonObject / value
	AttributeName2: JsonObject / value
}
```

```java
JsonArrayBuilder arr = Json.createArrayBuilder();
collection.stream().map(v -> Json.createObjectBuilder()
                .add("AttributeName1", JsonObject / value)
                .add("AttributeName2", JsonObject / value)
                .build())
        .forEach(v -> arr.add(v));

JsonObject obj = Json.createObjectBuilder()
		.add("JsonAttributeName1", JsonAttributeValue)
		.add("JsonAttributeName2", JsonAttributeValue)
		.add("JsonAttributeName3", JsonAttributeValue)
		.add("JsonAttributeName4", arr)
		.build();
```

## Parse JsonObjectString to Generic Json Object and retrieve values
```js
{
	Attribute1: value,
	Attribute2: value,
	Attribute3: value
}
```

```java
JsonObject obj = Json.createReader(new StringReader(JsonString))
		.readObject();
String attribute1  = obj.getString("Attribute1");
int attribute2 = obj.getJsonNumber("Attribute2").intValue();
```

## Parse JsonObjectString and retrieve nested Json Object
```js
{
	Attribute1: value,
	Attribute2: value,
	Attribute3: JsonObject
}
```

```java
JsonObject obj = Json.createReader(new StringReader(JsonString))
		.readObject();
JsonObject attribute3 = obj.getJsonObject("Attribute3");
```

## Parse JsonArrayString and collect into a List collection
```js
[
	string1,
	string2,
	string3,
	string4
]
```

```java
JsonArray arr = Json.createReader(new StringReader(JsonString))
		.readArray();
List<String> collection = new ArrayList<>();
arr.stream().forEach(v -> collection.add(v));
```