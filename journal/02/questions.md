# Intro to JavaScript
01. Which keywords are used to declare a variable in JavaScript?

    > | The three keywords to declare variables are "let", "const", and "var". const will not allow you to override any of the variables it declares. |

02. What is the definition of a function?

    > | Functions are pieces of code designed to carry out a specific task. They cannot act on their own, however, but must be called. In this way they are also a storage site, kind of like DNA, waiting for certain environmental triggers to begin accessing the code. |

03. What are the `SOLID` principles?

    > | Principles I need to learn to follow more closely. I will repeat the definitions I have found here, but I am still very fuzzy with their application starting at L.
    S: Single-responsiblity - keep functions aligned to task
    O: Open-closed - avoid writing in ways where critical code can be overridden
    Liskov Substitution - something about not having conflicting class elements when going between more general and more specific element definitions. So all grandmas are women, but not all women are grandmas, but the class of "good for society" should not be impacted whether or not the element is "grandmas" or "women".
    Interface Segregation - is something I won't even pretend to get. Cars do not belong on sidewalks and pedestrians in the street is equally bad?
    Dependency Inversion - inverted pyramids are unstable, do not code like this, with higher levels relying on the functionality of modifiable functions. |

04. Given this array: How could you remove the `pineapple`?

    ```js
    let fruit = ['apple', 'banana', 'pineapple', 'orange', 'strawberry']
    ```

    > | Well, I know there is a "splice" method, but when doing the pre-coursework I repeatedly botched the function (I always ended up with the first or last item being removed, or with the ID being run as a number for subtraction). I _think_ you open the array and run splice under two parameters
    fruit.splice(index, 'pineapple') <-- not that this really worked for me after Contact List. |

05. Given these two objects: How could you add each to the others friends arrays?

    ```js
    let you = {
        name: "You",
        hair: true,
        friends: []
    }
    let them = {
        name: "Them",
        hair: false,
        friends: []
    }

    ```

    > |
    function addFriend() {
  let buddy = you.find(your => your.friends += 'them')
  let pal = them.find(their => their.friends += 'you')
}
I know this is wrong because the kahoot went over this, something about push. |

06. Give an example of a JavaScript `Conditional`:

    > | function hope() {
        let codeWorking = false
        let stress = ""
        if(codingWorking == true) {
            stress = 3
            console.log("Reasonable bedtime for you")
        }
        else {
            stress = 7
            console.log("Despairing")
        }
    } 

    Did that even work? |

07. What is the main difference between `parameters` and `arguments`?

    > | Arguments fall within parameters, like with regular, verbal arguments, ideally. A baker's dozen is 13, so the rule for arguing that a dozen is, indeed, 13 and not 12, you must invoke the mental function where the parameters can make the argument valid.
    const dozen = 12
    const freebie = 1
    function bakersDozen(num1, num2) {
        let num1 = dozen
        let num2 = freebie
        return num1 + num2
    } 
    |

08. Instead of writing everything to the console, what is a better way to debug your code?

    > | Inquiring minds would like to know. Use the dev tools to target elements and tinker that way? |

09. What is the difference between a `primitive` value and a `reference` value?

    > | Primitive values are when the variable's value is the base date, whereas relative values are in reference to primitive values. So a smartphone is a reference for contacts, and can be accessed by multiple phones or devices but the contact itself is not able to change their info (without phone companies or courts). |

10. Demonstrate a loop that prints the numbers between -100 and 100?

    > | for (let i = -100; i<= 100; i++) |
