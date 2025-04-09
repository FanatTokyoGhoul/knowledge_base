# `@JmixEntity(annotatedPropertiesOnly = false)` (по умолчанию)

1) JPA сущность: все свойства, кроме аннотированных @javax.persistence.Transient;
2) DTO сущность: все свойства
3) JPA и DTO сущности: все свойства и методы с аннотацией @JmixProperty

# `@JmixEntity(annotatedPropertiesOnly = true)`
1) JPA и DTO: только свойства и методы с аннотацией @JmixProperty

# Example
```java
@JmixEntity
@Table(name = "ID_TRANSACTION", indexes = {
        @Index(name = "IDX_ID_TRANSACTION_OWNER", columnList = "OWNER_ID")
})
@Entity(name = "id_Transaction")
public class Transaction{
    @JmixGeneratedValue
    @Column(name = "ID", nullable = false)
    @Id
    private UUID id;
    @CreatedBy
    @Column(name = "CREATED_BY")
    private String createdBy;
    @CreatedDate
    @Column(name = "CREATED_DATE")
    private OffsetDateTime createdDate;
    @LastModifiedBy
    @Column(name = "LAST_MODIFIED_BY")
    private String lastModifiedBy;
    @LastModifiedDate
    @Column(name = "LAST_MODIFIED_DATE")
    private OffsetDateTime lastModifiedDate;
    @JoinColumn(name = "OWNER_ID")
    @NotNull
    @ManyToOne(fetch = FetchType.LAZY)
    private User owner;
    
    @Transient
    private Int transientInt;

    public void setOwner(User owner) {
        this.owner = owner;
    }

    public User getOwner() {
        return owner;
    }

    @InstanceName
    public String getTransactionName() { return String.join("_", owner.getUsername(), id.toString()); }

    public OffsetDateTime getLastModifiedDate() {
        return lastModifiedDate;
    }

    public void setLastModifiedDate(OffsetDateTime lastModifiedDate) {
        this.lastModifiedDate = lastModifiedDate;
    }

    public String getLastModifiedBy() {
        return lastModifiedBy;
    }

    public void setLastModifiedBy(String lastModifiedBy) {
        this.lastModifiedBy = lastModifiedBy;
    }

    public OffsetDateTime getCreatedDate() {
        return createdDate;
    }

    public void setCreatedDate(OffsetDateTime createdDate) {
        this.createdDate = createdDate;
    }

    public String getCreatedBy() {
        return createdBy;
    }

    public void setCreatedBy(String createdBy) {
        this.createdBy = createdBy;
    }

    public UUID getId() {
        return id;
    }

    public void setId(UUID id) {
        this.id = id;
    }
}
```

При таком подходе будут доступны все поля кроме `transientInt`