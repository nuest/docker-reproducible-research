## Using this template

### Copying this template

If you want to generate a new Author Carpentry lesson, use the Github import
feature.  Click the + sign in the upper right corner of the Github window, next
to your user account logo.  Select "Import a Repository".  For the URL enter
https://github.com/AuthorCarpentry/lesson-template and choose the location and
name for the new lesson.  If you're generating an authorized AuthorCarpentry
lesson, select "AuthorCarpentry" as the owner.  If want to independently use
this template to make a lesson, select your Github username or other
organization as the owner.  We're using the "Import a Repository" tool instead
of forking because Github doesn't allow multiple forks under the same owner.
If you're developing an independent lesson in your account, feel free to use
Fork instead.

### Modifying this template for a new lesson

Set up

* Download and install mkpage from https://github.com/caltechlibrary/mkpage
* Clone a copy of the repository to your local machine.  You can use the GitHub
Desktop application or the command line command using 
'git clone https://github.com/AuthorCarpentry/lesson-name'

Add Content

* Edit README.md with information about this lesson
* Add individual .md files with lesson topics in repository with leading
* numbers like: 00-topic1.md;
01-topic2.md
* Edit nav.md to set links in the navigation bar

View Lesson

* In your terminal, type ./mk-website.bash to generate .html files
* To preview the lesson, type ws and point your web browser to
http://localhost:8000/.  
* When you're happy with the lesson, type ./publish_website.bash to send
* changes to
github (script does a git commit and git push)


## Modifying template for a workshop containing multiple lessons

### Optional-Importing new changes from the template

Because we're generating a new copy of the template, there's no was within
Github to automatically adopt new template modifications (such as images or
updated text).  However, you can import modifications using the command line
version of Git.  Clone the repository to your personal computer (use git clone
or GitHub Desktop).  Open up your command line application (such as Terminal on
a Mac) and cd to the directory where you put the cloned repository.  Then type

```shell
    git remote add template https://github.com/AuthorCarpentry/lesson-template
    git fetch template
    git merge -s recursive -Xours -m "Merge in template changes" template/gh-pages
```

This will pull information from the template and merge any changes into the
lesson.  You only need to use the last two commands to merge future changes.
This merge will work automatically in most cases and preserve the
customizations you've made to the lesson.  In some cases this automatic merge
will fail and you should look at the changes to determine the reason for the
clash.  When you're happy with the updates type

```shell
    git commit
    git push
```

or use GitHub Desktop to sent the changes up to GitHub.


