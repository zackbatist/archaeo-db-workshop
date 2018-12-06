# archaeo-db-workshop

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

## Description

## Module Topics
1. What is a database?
2. Setting up a database
  * Command line basics
  * Installing MariaDB Server
  * Creating and configuring a database
  * Creating users and grant permissions
3. Designing database structure
  * Creating tables
  * Indexes
  * Relationships
4. Importing existing data
5. SELECT and JOIN queries
6. UPDATE and INSERT queries
7. Creating front-end interfaces

## Learning Outcomes

- Understanding what a database is, and how it relates to other aspects of an archaeological information infrastructure
- Understand how to design effective and flexible database structures
- Create a research database
- Understand how to input, modify and look up data
- Become a profficient user of the command line

## Expectations

- Participants will bring their own laptop
- Participants will bring a copy of their own dataset to work with, or be able to think through the specific aspects of the data that they hope to collect in the future
- Participants will receive primer information via a [welcome email](https://zackbatist.github.io/archaeo-db-workshop/articles/general/general-welcome-email.pdf), which includes:
  - [laptop setup instructions](https://zackbatist.github.io/archaeo-db-workshop/articles/general/general-laptop-setup-instructions.pdf),
  - a Linux shell primer,
  - and a [pre-workshop survey](https://zackbatist.github.io/archaeo-db-workshop/articles/general/general-pre-workshop-survey.pdf)
- Participants are comfortable using a computer before, with no assumptions about prior programming or networking knowledge

## Facilitation Guidelines

- The workshop is led by a facilitator driving the session according to the lesson plan
- Aim to have one helper for every 6 students, responsible for:
    - Providing assistance during hands-on sections
    - Keeping groups on schedule for each activity
- Use a [shared notepad](https://etherpad.wikimedia.org/p/archaeo-db-workshop) for:
    - Sharing notes and links
    - Jargon-busting
- Conclude with a [ticket out the door](http://www.ideasforeducators.com/idea-blog/a-twist-on-ticket-out-the-door) activity where students can optionally and anonymously leave feedback as they leave the class

## Workshop Materials
Class materials are written as [Markdown](https://en.wikipedia.org/wiki/Markdown) files and presentation slides are created as a Markdown-based [GitBook](https://www.gitbook.com). All generated assets are hosted on [GitHub Pages](https://zackbatist.github.io/archaeo-db-workshop/) and packaged as a downloadable archive on [GitHub Releases](https://github.com/zackbatist/archaeo-db-workshop/releases/latest).

When facilitating the workshop in an offline environment, you can run `gitbook serve` from a `presentation` directory to serve the slides on `http://localhost:4000`.

If you want to generate course assets yourself, simply run `./install-dependencies.sh` and `./build.sh`. You will find the generated assets in the `output` folder. The `./package.sh` script is used to zip up the generated assets into downloadable archives and to create the course website.

[Travis CI](https://travis-ci.org/) is configured to build, package, and publish a new release to GitHub Pages and Releases whenever a new tag is pushed. So all you need to create a new release is to push a new tag with `git tag <version>` and `git push --tag`.

## Credits
Some aspects of this workshop, including the overall structure of this GitHub repository and some of its contents, are drawn from the material made available by [Toronto Mesh](https://github.com/tomeshnet) for their [P2P Internet Workshop](https://github.com/tomeshnet/p2p-internet-workshop). Gracious thanks to Dawn Walker [[@dcwalk](https://github.com/dcwalk)] for providing me with this, as well as other helpful resources.

## License
All workshop materials at github.com/zackbatist/archaeo-db-workshop/ are licensed under a Creative Commons Attribution-ShareAlike 4.0 International License, the text of which is included in the repository LICENSE file.