#XTemplates
A tag interface for declaring methods that accept objects and convert them into HTML based on an associated template.
Methods return SafeHtml instances which can be used in many GWT and GXT widgets to render content. 

##Features
XTemplates support a variety of features to make it easy to generate content, including:

* Reading properties and nested properties.
* Formatting data into strings.
* Collection and Array iterating, applying sub templates to each item.
* Conditional support, including the ability to call other Java methods that return boolean.
* Basic math and expression support.

##Reference
* <a href="http://docs.sencha.com/gxt/3/com/sencha/gxt/core/client/XTemplates.html" target="_target">XTemplates Javadoc</a>

##Example
Templates are declared by creating an interface that extends XTemplate. 
Instances can then be created by invoking GWT.create on the template class.

* Example using XTemplates:

```java
public interface SampleXTemplates extends XTemplates {
  @XTemplate("<div>Hello, {name}!</div>")
  SafeHtml hello(String name);
}
```

* Instantiating the Template class:

		```java
		private SampleXTemplates tpl = GWT.create(SampleXTemplates.class);
		```
		
* Example invoking `tpl.hello("test")` would return the SafeHtml instance representing the annotated HTML.

		```html
		<div>Hello, test!<div>
		```
				
##XTemplate Template Source
Two methods exist for loading the template source. 

* Example of both methods, using the annotated template source and using the file template source.
 
 		```java
		public interface SampleXTemplates extends XTemplates {
		  // Specifying the template source directly in the annotation. 
		  @XTemplate("<div>Hello, {name}!</div>")
		  SafeHtml hello(String name);
		  
		  // Specifying the template source as an external file.
		  @XTemplate(source = "hello.html")
		  SafeHtml helloExternal(String name);
		}
		```

* Example using the templates in the application.

		```java
		public void displayTemplates() {
		  SampleXTemplates tpl = GWT.create(SampleXTemplates.class);
		  
		  // Example using the template source in the annotation.
		  // Displays: 'Hello, Fred!'
		  RootPanel.get().add(new HTML(tpl.hello("Fred")));
		  
		  // Example using the template source in the file.
		  // Displays: 'Hello, Willma!'
		  RootPanel.get().add(new HTML(tpl.helloExternal("Willma")));
		}
		```


##XTemplate Source Variables
Passing data to the templates using method variables.
 
* The variable data types can be of any data type, from String, primitives and objects. 
* Variables referencing the object's variables instances is done using bean getter naming conventions.   

###String and Primitives Variables
Passing data to the template via a `String` variable. 

* Variables are defined by surrounding a name with curly braces like `{variable}`:

		```java
		public interface SampleXTemplates extends XTemplates {
	      // Using a String variable
		  @XTemplate("<div>Hello, {name}!</div>")
		  SafeHtml hello(String name);
		}
		```

###Objects in XTemplate Method Signatures
XTemplates can reference the object's instance variables. 
For example in the `Person` object the name and age data members are provided and are referenced with 
template variables like `{name}` and `{age}`. The variable names follow the bean getter naming convention.   

* Example of a `Person` object which is used in the XTemplate method signature below.  		

		```java
		public class Person {
		  private String name;
		  private int age;
		  public Person(String name, int age) {
		    this.name = name;
		    this.age = age;
		  }
		  public String getName() {
		    return name;
		  }
		  public int getAge() {
		    return age;
		  }
		}
		```

*  Setting up the XTemplates method `hello(Person person)` with `Person` in the method signature and then in the
 XTemplate source add the `Person` XTemplate variable references to `{name}` and `{age}`.  

		```java
		public interface SampleXTemplates extends XTemplates {
		  // Providing person instance to the XTemplate method.
		  // {name} uses Person.getName();
		  // {age} uses Person.getAge();
		  @XTemplate("<div>Hello, {name}! Is your age {age}?</div>")
		  SafeHtml hello(Person person);
		}```
	
* Using the XTemplate method `hello(person)` in the application example:

		```java
		public void displayTemplates() {
		  SampleXTemplates tpl = GWT.create(SampleXTemplates.class);
		  
		  // Displays: 'Hello, Barney! Is your age 34?'
    	  Person barney = new Person("Barney", 34);
    	  RootPanel.get().add(new HTML(tpl.hello(barney)));
		}
		```

###XTemplate Variable Referencing, Objects in Objects
When referencing the object provided in the XTemplate method signature 
and that object data member is an object with more data member variables then 
a path to the deeper instance variable will be needed to be given in the XTemplate source variables.

*  Example of a `Person` object used in the XTemplate method signature. Notice the `private Person father` and `public Person getFather() {...`.

		```java
		public class Person {
		  private String name;
		  private int age;
		  private Person father;
		  public Person(Person father, String name, int age) {
		    this.father = father;
		    this.name = name;
		    this.age = age;
		  }
		  public String getName() {
		    return name;
		  }
		  public int getAge() {
		    return age;
		  }
		  public Person getFather() {
		    return father;
		  }
		}
		```

* When the XTemplate is used, `father.name` path uses the `father.getName()` to replace XTemplate source variabel `{father.name}` 
with the `Person.father.name` instance variable.
  
  		```java
		public interface SampleXTemplates extends XTemplates {
		  // Providing person instance to the XTemplate method.
		  // {name} uses Person.getName();
		  // {age} uses Person.getAge();
		  // {father.name} uses Person.getFather().getName();
		  @XTemplate("<div>Hello, {name}! Is your age {age}? {name}&lsquo;s father is {father.name}.</div>")
		  SafeHtml hello(Person person);
		}
		```
  
* Using the XTemplate method `hello(person)` in the application example:

		```java
		public void displayTemplates() {
		  SampleXTemplates tpl = GWT.create(SampleXTemplates.class);
		   
		  // Displays: 'Hello, Barney! Is your age 34?'
		  Person father = new Person(null, "Bob", 61);
		  Person barney = new Person(father, "Barney", 34);
		  RootPanel.get().add(new HTML(tpl.hello(barney)));
		}
		```

####XTemplate Variable Referencing, Deeper Object Graph Paths
XTeamplate can reach deeper into the Object graph by using deeper source paths to reference any of the 
Object instance variables. 

* For instance having these classes below representing the `Person` object graph.

		```java
		public class Person {
		  private String name;
		  private int age;
		  private Person father;
		  private Book favoriteBook;
		  public Person(Person father, String name, int age, Book favoriteBook) {
		    this.father = father;
		    this.name = name;
		    this.age = age;
		    this.favoriteBook = favoriteBook;
		  }
		  public String getName() {
		    return name;
		  }
		  public int getAge() {
		    return age;
		  }
		  public Person getFather() {
		    return father;
		  }
		  public Book getFavoriteBook() {
		    return favoriteBook;
		  }
		}
		
		public class Book {
		  private String title;
		  private Recommendation recommendation;
		  public Book(String title, Recommendation recommendation) {
		    this.title = title;
		    this.recommendation = recommendation;
		  }
		  public String getTitle() {
		    return title;
		  }
		  public Recommendation getRecommendation() {
		    return recommendation;
		  }
		}
		
		public class Recommendation {
		  private String message;
		  public Recommendation(String message) {
		    this.message = message;
		  }
		  public String getMessage() {
		    return message;
		  }
		}
		```
		
* Building on the earlier examples of path reference, `{favoriteBook.recommendation.message}` references a 
deeper object in the graph. Or you could say `{favoriteBook.recommendation.message}` uses `Person.getFavoriteBook().getRecommendation.getMessage()`.

		```java
		public interface SampleXTemplates extends XTemplates {
		  // Providing person instance to the XTemplate method.
		  // {name} uses Person.getName();
		  // {age} uses Person.getAge();
		  // {father.name} uses Person.getFather().getName();
		  // {favoriteBook.title} uses Person.getFavoriteBook().getTitle();
		  // {favoriteBook.recommendation.message} uses Person.getFavoriteBook().getRecommendation.getMessage();
		  @XTemplate("<div>Hello, {name}! Is your age {age}? " +
		  		"{name}&lsquo;s father is {father.name}. " +
		  		"My favorite book is {favoriteBook.title} and " +
		  		"has recommendation: {favoriteBook.recommendation.message}</div>")
		  SafeHtml hello(Person person);
		}
		```

* Using the XTemplate method `hello(person)` in the application example:

		```java
		public void displayTemplates() {
		  SampleXTemplates tpl = GWT.create(SampleXTemplates.class);
		  
		  // Displays: 'Hello, Barney! Is your age 34? Barney's father is Bob. My favorite book is 
		  //            Dinosaurs and has recommendation: This book was good.'
		  Recommendation recommendation = new Recommendation("This book was good.");
		  Book book = new Book("Dinosaurs", recommendation);
		  Person father = new Person(null, "Bob", 61, null);
		  Person barney = new Person(father, "Barney", 34, book);
		  RootPanel.get().add(new HTML(tpl.hello(barney)));
		}
		```





##Common XTemplate Problems
Since the variable references are strings makes for a few common things going wrong and 
GXT has good debug logging to help diagnose the issue quickly. 

###MisNamed XTemplate Source Variable
Misnamed variable in the XTemplate source will cause an build error. 
The screen shot below this demonstrates making the mistake of naming the variable incorrectly in the XTemplate source. 
The variable was named {book.title} but should have been named {favoriteBook.title}. 

<img src="images/MisNamedVar.png" />
  
###No Getter in Object for XTemplate Variable Name
XTemplates references the Object instance variables through the getters and 
it follows the beans getter naming convention. 
The screen shot below this demonstrates a 'no getter' error during the build. 
In this case, when using `{favoriteBook.recommendation}` looked for the getter method favoriteBook.getRecommendation()
and it did not exist thus causing the error. 

<img src="images/NoGetter.png" /> 


 
