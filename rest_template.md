# RestTemplate

## GET without exchange
```java
RestTemplate template = new RestTemplate();
ResponseEntity<String> resp = template.getForEntity(url, String.class);
```

## GET with exchange
```java
RequestEntity<String> req = RequestEntity
		.get(url)
		.accept(MediaType.APPLICATION_JSON)
		.build();

RestTemplate template = new RestTemplate();
ResponseEntity<String> resp = template.exchange(req, String.class);
try {
    JsonObject = Json.createReader(new StringReader(resp.getBody()))
            .readObject();
} catch (IOException ex) {
	
} 
```
