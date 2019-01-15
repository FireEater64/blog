---
title: "Using Jenkins as Part of a Latex Workflow"
date: 2015-10-01T17:33:00Z
draft: false
---

`LaTeX` is a fantastic, sometimes forgotten typesetting system - with a radically different workflow compared to most [WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG) editors. The fact that, in `LaTeX`, what you edit (a `.tex` file), and what you produce (typically a `.pdf` or `.ps` file) are totally different files can take a bit of getting used to. This idea of treating 'documents as source-code' has some powerful benefits, however. Many people already use VCS as a repository for storing `LaTeX` markup - which has numerous benefits when it comes to managing multiple different versions of a document, and writing with multiple contributors. This post takes this markup-as-code' idea one step further and uses another tool familiar to software developers - build servers such as Jenkins[^1]


## Why bother?
Some of you may be asking: Why use a build server to produce `LaTeX` documents?. Why not simply compile the PDF on your local machine, and copy it into Dropbox/Google Drive/an email? Whilst certainly an overkill addition to any small `LaTeX` project, there are numerous advantages when writing long-running documents with multiple contributors:

- No need to install a (sizable) `LaTeX` environment on your main development machine (especially useful if you use a number of packages not in the minimal `LaTeX` install)
- Automatically produces a PDF from the latest version checked into VCS - no more forgetting to email your boss the most up-to-date copy (oops).
- Ensures anybody else working on your document can build the latest version successfully

If nothing else - it's a great learning opportunity.

## How?
We'll be using Jenkins[^1] for this guide on account of it being free and open source - however this can also be done using your favorite build server - be it [TeamCity](https://www.jetbrains.com/teamcity/), [GoCD](http://www.go.cd/) or [Bamboo](https://www.atlassian.com/software/bamboo).

#### Set up your build server
[There are numerous guides on the internet for setting up Jenkins](http://bfy.tw/24hv). Here, however, we want to install an additional plugin - to send our produced `.pdf` to Dropbox. We could simply install Dropbox on the build agent, and move the `.pdf` to the desired folder - but syncing your entire Dropbox onto (potentially) multiple build agents is a bit overkill. Fortunately, the fantastic `publish-to-dropbox`[^2] Jenkins plugin prevents us from having to do this, or messing with the Dropbox API via CURL (yuck). 

Install the plugin from 'Manage Jenkins' -> 'Manage Plugins' -> 'Available', and search for 'Publish Over Dropbox'. Once installed (you'll need to restart Jenkins), and generate a Dropbox API token. To do this, browse to 'Credentials' -> 'Global Credentials' -> 'Add Credentials' and select 'Dropbox API Token' via the dropdown. Generate and save the credential.

![](/img/JenkinsDropboxToken.PNG)

You'll also need to configure the Dropbox location you wish to send the resulting `.pdf` to. This can be done via 'Manage Jenkins' -> 'Configure System' -> 'Dropbox'. Set an easily-identifiable name for the location, select the credential you just set up from the dropdown, and specify the path from the root of your Dropbox you want files to be delivered to in Unix notation. For example, if your Dropbox contains a folder called 'foo', which contains a subfolder named 'bar' - specify `/foo/bar/`.

![](/img/DropboxLocationConfig.PNG)

#### Configure your build agent(s)
Once your build agent(s) are set up, make sure `LaTeX` is installed. There are numerous guides for configuration a `TeX` environment on either Linux or Windows, but on Ubuntu Server (which I was using), a full TeX environment can be installed via apt-get:

    sudo apt-get install --no-install-recommends texlive-fonts-recommended texlive-latex-extra texlive-fonts-extra dvipng texlive-latex-recommended

#### Configure your project in Jenkins
Creating a new project in Jenkins is simple - simply login and hit the `New Item` button.

![](/img/Capture-1.PNG)

As with any other Jenkins project, you'll need to give your VCS details. I use Git here.

![](/img/JenkinsGitDetails.png)

Configure Jenkins to poll VCS reasonably often (or use a post-commit hook), and execute `pdflatex` as the only build step:

![](/img/JenkinsBuildSteps.PNG)

Finally, archive the produced `.pdf` to Jenkins and the Dropbox location you specified earlier:

![](/img/JenkinsArtifactArchive.PNG)

Advanced settings will allow you the option of flattening the output directory structure (advisable), using a DateTime as part of the folder name and/or clearing out the folder before transferring files. This last option might tempt you - but remember that Dropbox will overwrite any files with the same name when you push new files to it. Furthermore, it will treat the new file as a version of the old one - which will allow you to restore the older version should you wish.

![](/img/DropboxVersions.PNG)

#### Run the build
And we're done! Obviously, once you've got a basic build set up for `LaTeX` documents, all sorts of things are possible. You could run a spell checker as part of the build process, or notify a mailing list of a new version of the document. Hopefully, however, this has been enough to get you started - happy writing!

[^1]: https://jenkins-ci.org/
[^2]: https://github.com/rcgroot/jenkins-publish-over-dropbox-plugin