# Single Page Applications with Vue
01. What is the entrypoint of an application?

  > | An entry point determines where users can begin their interactions. Home pages act as entry points for applications since all further activity will be derived from that page. |

02. What is the difference between a vue `component` and `page`?

  > | Components are rendered to pages, meaning they are nested within them. While components can be nested in components, a page presents the final form that will be visible to users, with the majority of complex code inserted as packaged components rather than fully written out on the page itself. |

03. What is ***Component-Based Architecture***?

  > | Component-Based Architecture is a framework emphasizing the encapsulation of code. Well-encapsulated code will allow for a measure of reuse, and is very efficient when working with elements that have similar design and functionality, though their inputs may differ. |

04. What are the three tags that make up a Vue component?

  > | Template (housing the HTML), Script (JS), and Style (SCSS). |

05. What are ***lifecycle hooks***? What are lifecycle hooks used for?

  > | Lifecycle hooks are how components are initialized. The ones we are frequently using are onMounted, onUpdated, and onUnmounted - corresponding to the retrieval, change, and removal of a component's data. |

06. Which component in Vue does the vue-router use to mount pages onto?

  > | Maybe the grammar is confusing me, for some reason, but is it not the App.vue? All the pages seem nested there, or else it is simple the designated home page? |

07. What is the difference between the `AppState` and the state object within a component?

  > | The AppState has all of the ojects while components are designed to show specific objects. I think you probably *could* find a way to make a component not function that way, but then it would be a really bad component, above and beyond being plain wrong. |

08. What is the responsibility of `Services` in our Vue projects?

  > | The same as MVC - they convey information from the sandboxes to the components in a form they can run and manipulate. |

09. What are ***props*** and how are they used? Provide an example

  > | Props allow for continuity within components by transferring attributes down through each reference point. In our labs, we threw all the attributes of our items run through the models into the Vue files. Now, the receiving card pages do not have to worry about determining the type of each attribute, because that information has already be set elsewhere, and there is no mandate to change it.
  An example of what life could be like if props were not a stable facet in everyday life and physics can be found in the old video "Your Editing Lacks Continuity". Video not linked due to brief alcohol use. |

10. What is the Vue method used to create watchable objects such as `state` or `AppState`?

  > | C-c-compute? It hails the AppState and adapts the data sort of like a listener. |
