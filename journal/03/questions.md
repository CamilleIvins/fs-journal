# Application Architecture, MVC Design Pattern
01. What are the Pillars of Object Oriented Programming (`OOP`)?
  
  > | Encapsulation - classing code by subject or process so as to segregate purpose for clarity
  Abstraction - hiding processes from the user through layering interactive and non-interactive code
  Inheritance - code that has properties associated with another class, allowing for resuse of code
  Polymorphism - coding multpile methods with the "same" code, allowing for easymaintenance and replication |

02. How does `export` differ from `export default`?
  
  > | Default exports export single values, be it a class or am independent function, whereas general exports allow for specific funcrions within classes and such to be relayed without exporting code for which other pages have no use. |

03. What is Encapsulation?
  
  > | Ravioli-ing code so that it is user friendly, but not user-tamperable. Encapsulating allows for developers to protect critical operating code while leaving the users to work on changing information relevent without threatening the integrity of the application. Need-to-use basis only for users. |

04. What are some of the benefits of the `Proxy` object that we are using in our structure for applications?
  
  > | Proxy methods are part of what allow for effective encapsulation because they let data be manipulated without needing to touch the base code. Just like in regular use, proxies are allowed to act on behalf of other code. |

05. What the difference between a `class` and an instance of a `class`?
  
  > | Classes are the layout for each instance therein. So a student would be an instance of a class. |

06. What is a computed Property?
  
  > | Coding origami. Useful when dealing with templates. Like a single swan from the tedious template totally not coded in js but HTML, as instructed. |

07. What is the purpose of the `MVC` pattern?
  
  > | MVC is used to organize code in an industry standardized fashion so as to make development more efficicent by dividing what type of code goes where based on why, and by whom, it is accessed. |

08. What is the job of the `Controller` in the `MVC` Pattern?
  
  > | This is bit and bridle and blinders for users of an application, taking in their requests without giving them access to functions processing them. Controllers are the only part of the code with which users interact. |

09. What is the job of the `Service` in `MVC`?
  
  > | All work and no play makes Jack a dull boy, and the Service is a real Jack. All the data manipulation happens at this level, with requests from the Controller being processed here with relation to the core model data. |

10. What is the job of the `Model` in `MVC`?
  
  > | The model provides the framework in which data is stored, so changes must be triggered from the model in order to affect any alteration for the viewer. |
