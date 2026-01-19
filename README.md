# Java Message Service (JMS) 101

The Java Message Service (JMS) is an API that allows Java to communicate asynchronously between JVMs.  JMS is the Java standard for connecting to a Message Broker such as the Azure Service Bus.  

This presentation will cover all of the entry level concepts needed to start using JMS and then move on to some of the best practices and tuning techniques useful when starting out with JMS.

## Slide instructions
This is an html5 presentation that uses the [reveal.js](https://github.com/hakimel/reveal.js/) presentation framework.

### Viewing the presentation
This presentation is automatically deployed to GitHub Pages and can be accessed at:
https://dreamuth.github.io/Jms101/

### Local development
To run the presentation locally:
1. Start a web server in the project root directory (e.g., `python -m http.server 8000`)
2. Open your browser to [http://localhost:8000/](http://localhost:8000/)

### Deployment
The presentation is automatically deployed to GitHub Pages via GitHub Actions when changes are pushed to the `master` branch. The workflow builds the reveal.js assets and deploys the entire repository to GitHub Pages.
