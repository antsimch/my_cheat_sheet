# File Upload
## application.properties
### BLOB file size
BLOB  < 64 KB

MEDIUMBLOB < 16MB

LONGBLOB < 4GB
```yaml
spring.servlet.multipart.enabled=true
spring.servlet.multipart.max-file-size=16MB
spring.servlet.multipart.max-request-size=16MB
spring.servlet.multipart.file-size-threshold=1MB
```

## Spring Boot
```java
@Autowired JdbcTemplate template;

@PostMapping(consumes = MediaType.MULTIPART_FORM_DATA)
public ResponseEntity<String> post(@RequestPart MultipartFile file,
    @RequestPart String name) {

    String fileName = file.getName();
    String originalName = file.getOriginalFileName();
    String mediaType = file.getContentType();
    InputStream is = file.getInputStream();

    template.update("insert into table(…, content) values (…, ?)", …, is);
}
```

## Angular
```ts
const formData = new FormData()

formData.set('name', this.form.get('formControlName').value)

formData.set('file', this.viewChildVariable.nativeElement.files[0])
```