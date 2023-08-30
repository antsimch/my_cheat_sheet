# Retrieve file from SQL database

## Retrieving BLOB with ResultSetExtractor (Return in byte[])
```java
@GetMapping(path = "/{id}")
public ResponseEntity<byte[]> getImage(@PathVariable Integer id) {
    Optional<FileData> opt = template.query("select * from table where id = ?", 
            params, (rs: ResultSet) -> {
                    if (!rs.next()) 
                        return Optional.empty();

                    FileData file = new FileData();
                    file.setName(rs.getString("name"));
                    file.setContentType(rs.getString("media_type"));
                    file.setContent(rs.getBytes("content"));
                    return Optional.of(file);
            }, id)
}
```