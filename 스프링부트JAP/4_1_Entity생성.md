![image](https://user-images.githubusercontent.com/64408793/170416571-99eedd7f-46fb-4274-8b5c-a1309c5a71ff.png)


### Address
```
@Embeddable
@Getter
public class Address {

    private String city;
    private String street;
    private String zipcode;

    protected Address() {
    }

    public Address(String city, String street, String zipcode) {
        this.city = city;
        this.street = street;
        this.zipcode = zipcode;
    }
}
```

### Category
```
@Entity
@Getter @Setter
public class Category {

    @Id @GeneratedValue
    @Column(name = "category_id")
    private Long id;

    private String name;

    @ManyToMany
    @JoinTable(name = "category_item" ,
        joinColumns = @JoinColumn(name = "category_id"),
        inverseJoinColumns = @JoinColumn(name ="item_id"))
    private List<Item> items = new ArrayList<>();

    @ManyToOne
    @JoinColumn(name = "parent_id")
    private Category parent;

    @OneToMany(mappedBy = "parent")
    private List<Category> child = new ArrayList<>();
}
```

### Delivary
```
@Entity
@Getter @Setter
public class Delivary {

    @Id @GeneratedValue
    @Column(name = "delivary_id")
    private Long id;

    @OneToOne(mappedBy = "delivary")
    private Order order;

    @Embedded
    private Address address;

    @Enumerated(EnumType.STRING)
    private DelivaryStatus status; // READY, COMP
}
```

### Album 
```
@Entity
@DiscriminatorValue("A")
@Getter @Setter
public class Album extends Item{

    private String artist;
    private String etc;

}
```

### Book 
```
@Entity
@DiscriminatorValue("B")
@Getter
@Setter
public class Book extends Item{

    private String avthor;
    private String isbn;

}
```

### Item
```
@Entity
@Getter
@Setter
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "dtype")
public abstract class Item {

    @Id @GeneratedValue
    @Column(name="item_id")
    private Long id;

    private String name;
    private int price;
    private int stockQuantity;

    @ManyToMany(mappedBy = "items")
    private List<Category> categories = new ArrayList<>();

}
```

### Movie 
```
@Entity
@Getter
@DiscriminatorValue("M")
@Setter
public class Movie extends Item{

    private String director;
    private String actor;

}
```

### Member
```
@Entity
@Getter
@Setter
public class Member {

    @Id @GeneratedValue
    @Column(name ="member_id")
    private Long id;

    private String name;

    @Embedded
    private Address address;

    @OneToMany(mappedBy = "member")
    private List<Order> orderList = new ArrayList<>();

}
```

### Order
```
@Entity
@Table(name = "orders")
@Getter
@Setter
public class Order {

    @Id @GeneratedValue
    @Column(name="order_id")
    private Long id;

    @ManyToOne
    @JoinColumn(name = "member_id")
    private Member member;

    @OneToMany(mappedBy = "order")
    private List<OrderItem> orderItems = new ArrayList<>();

    @OneToOne
    @JoinColumn(name = "delivary_id")
    private Delivary delivary;

    private LocalDateTime orderDate; // 주문시간

    @Enumerated(EnumType.STRING)
    private OrderStatus status; // 주문 상탱 ( ORDER , CANCLE )
}
```

### OrderItem
```
@Entity
@Getter
@Setter
public class OrderItem {

    @Id @GeneratedValue
    @Column(name="order_item_id")
    private Long id;

    @ManyToOne
    @JoinColumn(name="item_id")
    private Item item;

    @ManyToOne
    @JoinColumn(name="order_id")
    private Order order;

    private int orderPrice;

    private int count;

}
```

