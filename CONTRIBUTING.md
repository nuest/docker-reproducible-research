# Contributing

[AuthorCarpentry](http://authorcarpentry.github.io) is an open source project,
and we welcome contributions of all kinds:
new lessons,
fixes to existing material,
bug reports,
and reviews of proposed changes are all welcome.

## Contributor Agreement

By contributing,
you agree that we may redistribute your work under [our license](LICENSE.md).
In exchange,
we will address your issues and/or assess your change proposal as promptly as we can,
and help you become a member of our community.
Everyone involved in [Author Carpentry](http://authorcarpentry.github.io)
agrees to abide by our [code of conduct](CONDUCT.md).

## Working With GitHub

1.  Fork the `authorcarpentry/lesson-name` repository on GitHub.  

2.  The default branch in our lessons is `gh-pages`. Create a 
    new branch for your changes.  
    Give your branch a meaningful name,
    such as `fixing-typos-in-shell-lesson`
    or `adding-tutorial-on-visualization`.

3.  Clone this repository and branch to work with it on your computer.  
    git clone the repository with -b 'branch name'

4.  Make your changes, commit them, and push them to your repository on GitHub.

5.  Send a pull request to the `gh-pages` branch of the main datacarpentry
    repository at http://github.com/authorcarpentry/lesson-name. This can
    be done through the github web interface. 

If it is easier for you to send them to us some other way,
please mail us at
[m@m.org](mailto:m@m.org).
Given a choice between you creating content or wrestling with Git,
we'd rather have you doing the former.

## Locations and Formats

Every lesson has a repository of its own, while individual topics are files
in that directory.  For example, the `shell-ecology` directory holding our
introduction to the shell for ecology contains the files `00-intro.md`, 
`01-filedir.md` and so on.  (We use two digits followed by a one-word topic 
key to ensure files
appear in the right order when listed.)

Lessons may be written in Markdown, as IPython Notebooks, or in other formats.
However, as explained in [the README file](README.md), Jekyll (the tool GitHub
uses to create websites) only knows how to handle Markdown and HTML.  if some
other format is used, the author of the lesson must add the generated Markdown
to the repository.  This ensures that people who *aren't* familiar with some
format don't have to install the tools needed to work with it (e.g., R
programmers don't have to install the IPython Notebook).

> If a lesson is in a format we don't already handle, the author must also add
> something to the Makefile to re-create the Markdown from the source.  Please
> check with us if you plan to do this.


## Formatting of the material

To ensure a consistent formatting of the lessons, we recommend the following
guidelines:
* No trailing white space
* Wrap lines at 80 characters (unless it breaks URLs)
* Use unclosed atx style headers (see below)

## FAQ

*   *Where can I get help?*

    Mail us at [authorcarpentry@library.caltech.edu](mailto:authorcarpentry@library.caltech.edu)
