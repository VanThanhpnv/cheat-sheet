# JPA

JPA allows to simply store data into mysql. During our practical work, we will not even need to know and write a single SQL query.

OpenJPA is the implementation of JPA James is using.

JPA allow you to persist Java Beans into the database.

In this session we will use JPA as a key/value database reader, wich makes queries easy to write.

Example :

```
    public void save(JPASubscription subscription) throws SubscriptionException {
        try {
            entityManager.getTransaction().begin();
            entityManager.merge(subscription);
            entityManager.getTransaction().commit();
        } catch (PersistenceException e) {
            throw new SubscriptionException(e);
        }
    }
    
    
    public void remove(JPASubscription subscription) throws SubscriptionException {
        try {
            entityManager.getTransaction().begin();
            entityManager.remove(subscription);
            entityManager.getTransaction().commit();
        } catch (PersistenceException e) {
            throw new SubscriptionException(e);
        }
    }
    
    
    public Subscrition save(String user) throws SubscriptionException {
        try {
            return entityManager.find(JPASubscription.class, user);
        } catch (PersistenceException e) {
            throw new SubscriptionException(e);
        }
    }
```

With :

```
@Entity(name = "Subscription")
@Table(name = "JAMES_SUBSCRIPTION")
public class JPASubscription implements Subscription {
    @Id
    @Column(name = "USER_NAME", nullable = false, length = 100)
    private String username;
    
    @Basic(optional = false)
    @Column(name = "MAILBOX_NAME", nullable = false, length = 100)
    private String mailbox;
    
    @Basic(optional = false)
    @Column(name = "SUBSCRIPTION_ID", nullable = false)
    private long id;
    
    public JPASubscription() {}
    
    // Getters ommitted for simplicity

    @Override
    public int hashCode() {
        // Ommitted for simplicity
    }

    @Override
    public boolean equals(Object obj) {
        // Ommitted for simplicity
    }
```

Remarks : 

 - Writes (merges and remove) needs to be wrapped in transactions
 - Read don't need to be wrapped in transactions
 - We need to give an Entity and table name to the persisted object using annotations
 - We need to specify the Id to use.
 - We can then specify the column to use. We can set a name and some more parameters.
 - We need to implement equals and hashCode for the persisted object.
 - OpenJPA needs non final fields, with empty constructor. 
 
 
