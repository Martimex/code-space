## THIS IS A NEW FILE

`Creating` something beyond the level of "personal project" felt overwhelming and out of my skill range for a long time. This time I took myself a challenge to overcome this problem. My goal was to build an app that might actually matter - not only for me, the developer, but also for people that can benefit from it.

Photos are universal property, being useful in various fields, like website design, marketing, etc. Searching for a perfect one through different websites might feel like an endless, daunting task. And the feel of paying the license fee for every single photo that you want to use is far from good, especially for non-commercial projects. 3PhotoLib is my answer to these concerns. The application unifies the biggest royalty-photo providers in a single app, giving you the possibility to find high-quality images much quicker.

The initial idea for the project was to make 3PhotoLib feel more like a photos search engine, that enables to only view and download photos. With that thought in mind, I have started the development process of 3PhotoLib on March 24th, 2024. The first important challenge was to incorporate different photo Providers into an app. Every Provider shares different information about a photo. While one may include many pieces of useful details about an image, the other one may not. This required several workarounds to be made. The "unification" process took a lot of testing and fixing things up. Eventually, as a proper solution was established, this issue became a thing of a past.

Afterwards, the design process of the application interface started. I have created the Searchbar, the Advaned Search Options menu, the Homepage component and also the Search Results page. During that time I was slowly realizing the project has a lot more potential rather than being a simple "search-by-phrase" photo galery. So, instead of finishing the functional part of the project, I have decided to unleash its full potential shortly after.

June 7th, 2024 was the turning point for 3PhotoLib. The main focus was now to introduce a user account feature with all its functionalities. First off, the actual Landing Page has been redefined to a SignIn / LogIn page. That step involved adding the actual process of creating the account, verifying it, logging into it, and finally - resetting the password. All of these parts were done from scratch, and it took a huge amount of time to complete them. Despite some frustrating bits from time to time, I really enjoyed the process of designing the authentication part of the app. I have also learned a lot about forms and inputs, which surprisingly, had been my weak point for a long time.

Next step to take was to add all the interactivity that a registered user can make. It involved, among all other features, creating a mechanism for a user to like / unlike the photo or designing a complete photo collections system. All of the action-based additions took 1 month and a half! During this period of time, I have made a lot of tests and fixed some issues to make sure that everything worked correctly and the project is free from bugs / glitches of any kind. The cherry on top was the final creation of the very last webpage inside the project - a very simple User Account page.

Since by that time, the core functionality of the project was finally completed, 3PhotoLib got released live on October 18th, 2024. The following month the updates were mostly about some simple bug fixing or interface impovements. However, there was still one important part left to be done - the responsive layout. So far, the design was already completed for the mobile version, resulting in nice and smooth design. Alas, that was not a true for desktop devices... yet!

Redesigning the project layout for desktop turned out to be the final challenge to overcome. Huge screen version required some extra mechanisms to be applied, so that the application will look great on the desktops, but also will not break or cause any modifications for mobile device layout. Finding a perfect balance was not an easy task. It really took plenty of work to get a satisfying result.

Ultimately, on January 1st, 2025 - the 9-month development journey has reached the finish line. The end results of (finally completed) application can be viewed here - https://threephotolib.vercel.app

```
for(let i=0; i<1; i++) {
    theme: {
        fontOrigin: "origin_source",
        cdnCaching: true,
        typography: {
        header: {
            name: "Some name",
            weights: [400],
        },
    }
}
```