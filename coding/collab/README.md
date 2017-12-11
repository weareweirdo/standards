# Designer & Developer collaboration

 ## Principle-based development

 Ideally, designers & developers should always work towards creating a set of standards that can be re-used across the project, as opposed to styling pages or elements in isolation.

 ### Is it worth it?

 Maybe you’ve given a design and one element has 10px space at the bottom.

 Why 10px? Everything else across the site is based off an 8px baseline, why is this space 10px? Is that extra 2px worth the bespoke style needed to apply it? Will the user notice that extra 2px?

 In isolation this kind of questioning approach might seem a bit extreme, however simply accepting rules which go against the established standards of codebase sets a precedent that its ok to add rules like this. We’re then in a situation where these kind of rules proliferate throughout the codebase and things can quickly spiral out of control.

 **Will the user notice an extra 2px? Unlikely. Will the user notice the website getting slower because we have an unnecessary amount of CSS? More likely.**