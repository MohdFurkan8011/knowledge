# Builder

The **builder pattern**, as name implies, is an **alternative way to construct complex objects**. This should be used only when you want to build different objects using same object building process.

##### Problem without Builder

In normal practice, if you want to make a immutable `User` class, then you must pass all five information as parameters to constructor. It will look like this:

```java
public User (String firstName, String lastName, int age, String phone, String address){
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.phone = phone;
    this.address = address;
}
```

Very good. Now what if only `firstName` and `lastName` are **mandatory** and rest 3 fields are optional. Problem !! We need more constructors.

```java
public User (String firstName, String lastName, int age, String phone){ ... }
public User (String firstName, String lastName, String phone, String address){ ...  }
public User (String firstName, String lastName, int age){ ...   }
public User (String firstName, String lastName){ ...    }
```

We will need some more like above. Still can manage? Now let’s introduce our sixth attribute i.e. salary. Now it is problem.

##### Solution with Builder

```java
public class User  {
    //All final attributes
    private final String firstName; // required
    private final String lastName; // required
    private final int age; // optional
    private final String phone; // optional
    private final String address; // optional
 
    private User(UserBuilder builder) {
        this.firstName = builder.firstName;
        this.lastName = builder.lastName;
        this.age = builder.age;
        this.phone = builder.phone;
        this.address = builder.address;
    }
 
    //All getter, and NO setter to provde immutability
    public String getFirstName() {
        return firstName;
    }
    public String getLastName() {
        return lastName;
    }
    public int getAge() {
        return age;
    }
    public String getPhone() {
        return phone;
    }
    public String getAddress() {
        return address;
    }
 
    @Override
    public String toString() {
        return "User: "+this.firstName+", "+this.lastName+", "+this.age+", "+this.phone+", "+this.address;
    }
 
    public static class UserBuilder {
        private final String firstName;
        private final String lastName;
        private int age;
        private String phone;
        private String address;
 
        public UserBuilder(String firstName, String lastName) {
            this.firstName = firstName;
            this.lastName = lastName;
        }
        public UserBuilder age(int age) {
            this.age = age;
            return this;
        }
        public UserBuilder phone(String phone) {
            this.phone = phone;
            return this;
        }
        public UserBuilder address(String address) {
            this.address = address;
            return this;
        }
        //Return the finally consrcuted User object
        public User build() {
            User user =  new User(this);
            validateUserObject(user);
            return user;
        }
        private void validateUserObject(User user) {
            //Do some basic validations to check 
            //if user object does not break any assumption of system
        }
    }
}
```

```java
public static void main(String[] args) {
    User user1 = new User.UserBuilder("Lokesh", "Gupta")
    				.age(30)
    				.phone("1234567")
    				.address("Fake address 1234")
    				.build();
 
    System.out.println(user1);
 
    User user2 = new User.UserBuilder("Jack", "Reacher")
    				.age(40)
    				.phone("5655")
    				//no address
    				.build();
 
    System.out.println(user2);
 
    User user3 = new User.UserBuilder("Super", "Man")
    				//No age
    				//No phone
    				//no address
    				.build();
 
    System.out.println(user3);
}
```

