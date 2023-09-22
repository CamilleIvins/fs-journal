# Managing the Fullstack Application

1. Describe the two ways to bind Data in Vue?

  > | One way is one-way data binding, which does not see the DOM automatically update information, whereas two-way binding does update on every instance of data change absent user initiative. |

2. The `SPA` acronym stands for what?

  > | Single Page Application - a model of web design that uses a single page that is filled with new data at each navigation point. |

3. What are some of the advantages/uses of a `SPA` over a traditional one?

  > | Because it is a single page, there is only a single instance of loading the page, even though from the user's perspective they are navigating around the site. Also, well-designed code for SPAs can reused across the site, reducing workload. |

4. What does the `onMounted` method in Vue do?

  > | It functions akin to the default draw that we used to use...way back in our junior days. It links to the functions that are expected to be performed when the page is loaded, before any user-side interaction. |

5. What is the `v-model` attribute in Vue for, and when might you use it?

  > | V-model is a two-way binding method that is very useful for instances where a user needs to enter or update information. Like a form. Lots and lots of forms. |

6. What is the package.json file used for?

  > | package.json is the map you get at a city's visitor's center, but for an application. Here you can see the basic information of a proect, like it's name. |

7. Which Vue attributes(directives) could you use to conditionally render elements on a page?

  > | v-if/v-else are good for making visibility conditional. The elements in question cannot be nested, as they need to function as alternatives to one another. |

8. What is the purpose of the `key` attribute when using `v-for` on an element?

  > | v-for is kind of like a forEach, iterating over arrays and entering the relevant date for each instance. Using a key will target a particular property you wish to target. |

9. What is the `<slot>` element and what is it used for?

  > | Slots are like portablr pieces of template that can be stuffed into modals. This contend can augment or replace existing code in the areas they are inserted. |
