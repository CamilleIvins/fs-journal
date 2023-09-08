# Intro to Server side concerns with JavaScript
01. What do the letters of the acronym `CRUD` stand for?

  > | Create, read, update, delete. Is also what you say when you forget the acronym during Kahoots. |

02. Each action that `CRUD` represents maps to an HTTP request. What HTTP request does each `CRUD` action correspond to?

  > | Create: POST
  Read: GET
  Update: PUT
  Delete:....DELETE |

03. What does `ORM` stand for? Which `ORM` do we use when interacting with MongoDB

  > | ORM stands for Object Relational Mapping. We have been using Mongoose. |

04. Which two `HTTP` request types include a body?

  > | POST and PUT. They both manipulate the data within the instance. |

05. In a/an _______ coding model, when you call a function, it returns only when the action has finished and stops your program for the time the action takes. Likewise in a/an _______ coding model, multiple things are allowed to happen at one time. When you perform an action, your program continues to run.  Fill in the blanks.

  > | Synchronous and asynchronous? This is the purpose of Promises, I think? |

06. What are the three types of data relationships? Provide an example of each.

  > | One-to-one: This could be for IDs stored across databases so that a particular person can be verified.
  One-to-many/many-to-one: One city can have many people, but those people all live in that once city.
  Many-to-many: Sneakers to people, where many people can own the same style pair of sneakers, or one person can own a variety of pairs. |

07. What is middleware?

  > | Auth0. Middleware is a way to augment an application without having to develop the processes in-house. This is so that applications can more efficiently connect with one another without needing whole operating systems for each one, making data transfer less cumbersome. |

08. The ______ pipeline delivers information from the client while the ______ pipeline returns it. Fill in the blanks. 

  > | continuous integration and continuous delivery? |

09. Demonstrate the pattern that is used to include a request query with the client's `HTTP` request providing the property `tag` and the value `winter`.

  > | `/api/seasons?tag=winter` |

10. What is a ***virtual property***?

  > | A virtual property is a way to assemble and retrieve data without that particular format of the data being saved in a database. Because of this, they cannot be used in queries. |
