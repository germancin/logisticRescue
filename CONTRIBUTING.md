# Contributing to jQuery

1. [Getting Involved](#getting-involved)
2. [Questions and Discussion](#questions-and-discussion)
3. [How To Report Bugs](#how-to-report-bugs)
4. [Tips for Bug Patching](#tips-for-bug-patching)

Note: This is the code development repository for *jQuery Core* only. Before opening an issue or making a pull request, be sure you're in the right place.
* jQuery plugin issues should be reported to the author of the plugin.
* jQuery Core API documentation issues can be filed [at the API repo](https://github.com/jquery/api.jquery.com/issues).
* Bugs or suggestions for other jQuery organization projects should be filed in [their respective repos](https://github.com/jquery/).

## Getting Involved

[API design principles](https://github.com/jquery/jquery/wiki/API-design-guidelines)

We're always looking for help [identifying bugs](#how-to-report-bugs), writing and reducing test cases, and improving documentation. And although new features are rare, anything passing our [guidelines](https://github.com/jquery/jquery/wiki/Adding-new-features) will be considered.

More information on how to contribute to this and other jQuery organization projects is at [contribute.jquery.org](https://contribute.jquery.org), including a short guide with tips, tricks, and ideas on [getting started with open source](https://contribute.jquery.org/open-source/). Please review our [commit & pull request guide](https://contribute.jquery.org/commits-and-pull-requests/) and [style guides](https://contribute.jquery.org/style-guide/) for instructions on how to maintain a fork and submit patches. Before we can merge any pull request, we'll also need you to sign our [contributor license agreement](https://contribute.jquery.org/cla/).


## Questions and Discussion

### Forum and IRC

jQuery is so popular that many developers have knowledge of its capabilities and limitations. Most questions about using jQuery can be answered on popular forums such as [Stack Overflow](https://stackoverflow.com). Please start there when you have questions, even if you think you've found a bug.

The jQuery Core team watches the [jQuery Development Forum](https://forum.jquery.com/developing-jquery-core). If you have longer posts or questions that can't be answered in places such as Stack Overflow, please feel free to post them there. If you think you've found a bug, please [file it in the bug tracker](#how-to-report-bugs). The Core team can be found in the [#jquery-dev](https://webchat.freenode.net/?channels=jquery-dev) IRC channel on irc.freenode.net.

### Weekly Status Meetings

The jQuery Core team has a weekly meeting to discuss the progress of current work. The meeting is held in the [#jquery-meeting](https://webchat.freenode.net/?channels=jquery-meeting) IRC channel on irc.freenode.net at [Noon EST](https://www.timeanddate.com/worldclock/fixedtime.html?month=1&day=17&year=2011&hour=12&min=0&sec=0&p1=43) on Mondays.

[jQuery Core Meeting Notes](https://meetings.jquery.org/category/core/)


## How to Report Bugs

### Make sure it is a jQuery bug

Most bugs reported to our bug tracker are actually bugs in user code, not in jQuery code. Keep in mind that just because your code throws an error inside of jQuery, this does *not* mean the bug is a jQuery bug.

Ask for help first in the [Using jQuery Forum](https://forum.jquery.com/using-jquery) or another discussion forum like [Stack Overflow](https://stackoverflow.com/). You will get much quicker support, and you will help avoid tying up the jQuery team with invalid bug reports.

### Disable browser extensions

Make sure you have reproduced the bug with all browser extensions and add-ons disabled, as these can sometimes cause things to break in interesting and unpredictable ways. Try using incognito, stealth or anonymous browsing modes.

### Try the latest version of jQuery

Bugs in old versions of jQuery may have already been fixed. In order to avoid reporting known issues, make sure you are always testing against the [latest build](https://code.jquery.com/jquery.js). We cannot fix bugs in older released files, if a bug has been fixed in a subsequent version of jQuery the site should upgrade.

### Simplify the test case

When experiencing a problem, [reduce your code](https://webkit.org/quality/reduction.html) to the bare minimum required to reproduce the issue. This makes it *much* easier to isolate and fix the offending code. Bugs reported without reduced test cases take on average 9001% longer to fix than bugs that are submitted with them, so you really should try to do this if at all possible.

### Search for related or duplicate issues

Go to the [jQuery Core issue tracker](https://github.com/jquery/jquery/issues) and make sure the problem hasn't already been reported. If not, create a new issue there and include your test case.


## Tips For Bug Patching

We *love* when people contribute back to the project by patching the bugs they find. Since jQuery is used by so many people, we are cautious about the patches we accept and want to be sure they don't have a negative impact on the millions of people using jQuery each day. For that reason it can take a while for any suggested patch to work its way through the review and release process. The reward for you is knowing that the problem you fixed will improve things for millions of sites and billions of visits per day.

### Build a Local Copy of jQuery

Create a fork of the jQuery repo on github at https://github.com/jquery/jquery

Change directory to your web root directory, whatever that might be:

```bash
$ cd /path/to/your/www/root/
```

Clone your jQuery fork to work locally

```bash
$ git clone git@github.com:username/jquery.git
```

Change directory to the newly created dir jquery/

```bash
$ cd jquery
```

Add the jQuery master as a remote. I label mine "upstream"

```bash
$ git remote add upstream git://github.com/jquery/jquery.git
```

Get in the habit of pulling in the "upstream" master to stay up to date as jQuery receives new commits

```bash
$ git pull upstream master
```

Run the build script

```bash
$ npm run build
```

Now open the jQuery test suite in a browser at http://localhost/test. If there is a port, be sure to include it.

Success! You just built and tested jQuery!


### Test Suite Tips...

During the process of writing your patch, you will run the test suite MANY times. You can speed up the process by narrowing the running test suite down to the module you are testing by either double clicking the title of the test or appending it to the url. The following examples assume you're working on a local repo, hosted on your localhost server.

Example:

http://localhost/test/?module=css

This will only run the "css" module tests. This will significantly speed up your development and debugging.

**ALWAYS RUN THE FULL SUITE BEFORE COMMITTING AND PUSHING A PATCH!**


#### Loading changes on the test page

Rather than rebuilding jQuery with `grunt` every time you make a change, you can use the included `grunt watch` task to rebuild distribution files whenever a file is saved.

```bash
$ grunt watch
```

Alternatively, you can **load tests in AMD** to avoid the need for rebuilding altogether.

Click "Load with AMD" after loading the test page.


### Repo organization

The jQuery source is organized with AMD modules and then concatenated and compiled at build time.

jQuery also contains some special modules we call "var modules", which are placed in folders named "var". At build time, these small modules are compiled to simple var statements. This makes it easy for us to share variables across modules. Browse the "src" folder for examples.

### Browser support

Remember that jQuery supports multiple browsers and their versions; any contributed code must work in all of them. You can refer to the [browser support page](https://jquery.com/browser-support/) for the current list of supported browsers.


# How to contribute

Third-party patches are essential for keeping Puppet great. We simply can't
access the huge number of platforms and myriad configurations for running
Puppet. We want to keep it as easy as possible to contribute changes that
get things working in your environment. There are a few guidelines that we
need contributors to follow so that we can have a chance of keeping on
top of things.

## Puppet Core vs Modules

New functionality is typically directed toward modules to provide a slimmer
Puppet Core, reducing its surface area, and to allow greater freedom for
module maintainers to ship releases at their own cadence, rather than
being held to the cadence of Puppet releases. With Puppet 4's "all in one"
packaging, a list of modules at specific versions will be packaged with the
core so that popular types and providers will still be available as part of
the "out of the box" experience.

Generally, new types and new OS-specific providers for existing types should
be added in modules. Exceptions would be things like new cross-OS providers
and updates to existing core types.

If you are unsure of whether your contribution should be implemented as a
module or part of Puppet Core, you may visit
[#puppet-dev on Freenode IRC](https://freenode.net) or ask on the
[puppet-dev mailing list](https://groups.google.com/forum/#!forum/puppet-dev)
for advice.

## Getting Started

* Make sure you have a [Jira account](https://tickets.puppetlabs.com)
* Make sure you have a [GitHub account](https://github.com/signup/free)
* Submit a ticket for your issue, assuming one does not already exist.
  * Clearly describe the issue including steps to reproduce when it is a bug.
  * Make sure you fill in the earliest version that you know has the issue.
* Fork the repository on GitHub

## Making Changes

* Create a topic branch from where you want to base your work.
  * This is usually the master branch.
  * Only target release branches if you are certain your fix must be on that
    branch.
  * To quickly create a topic branch based on master; `git checkout -b
    fix/master/my_contribution master`. Please avoid working directly on the
    `master` branch.
* Make commits of logical units.
* Check for unnecessary whitespace with `git diff --check` before committing.
* Make sure your commit messages are in the proper format.

````
    (PUP-1234) Make the example in CONTRIBUTING imperative and concrete

    Without this patch applied the example commit message in the CONTRIBUTING
    document is not a concrete example.  This is a problem because the
    contributor is left to imagine what the commit message should look like
    based on a description rather than an example.  This patch fixes the
    problem by making the example concrete and imperative.

    The first line is a real life imperative statement with a ticket number
    from our issue tracker.  The body describes the behavior without the patch,
    why this is a problem, and how the patch fixes the problem when applied.
````

* Make sure you have added the necessary tests for your changes.
* Run _all_ the tests to assure nothing else was accidentally broken.

## Making Trivial Changes

### Documentation

For changes of a trivial nature to comments and documentation, it is not
always necessary to create a new ticket in Jira. In this case, it is
appropriate to start the first line of a commit with '(doc)' instead of
a ticket number.

````
    (doc) Add documentation commit example to CONTRIBUTING

    There is no example for contributing a documentation commit
    to the Puppet repository. This is a problem because the contributor
    is left to assume how a commit of this nature may appear.

    The first line is a real life imperative statement with '(doc)' in
    place of what would have been the ticket number in a
    non-documentation related commit. The body describes the nature of
    the new documentation or comments added.
````

## Submitting Changes

* Sign the [Contributor License Agreement](http://links.puppet.com/cla).
* Push your changes to a topic branch in your fork of the repository.
* Submit a pull request to the repository in the puppetlabs organization.
* Update your Jira ticket to mark that you have submitted code and are ready for it to be reviewed (Status: Ready for Merge).
  * Include a link to the pull request in the ticket.
* The core team looks at Pull Requests on a regular basis in a weekly triage
  meeting that we hold in a public Google Hangout. The hangout is announced in
  the weekly status updates that are sent to the puppet-dev list. Notes are
  posted to the [Puppet Community community-triage
  repo](https://github.com/puppet-community/community-triage/tree/master/core/notes)
  and include a link to a YouTube recording of the hangout.
* After feedback has been given we expect responses within two weeks. After two
  weeks we may close the pull request if it isn't showing any activity.

## Revert Policy
By running tests in advance and by engaging with peer review for prospective
changes, your contributions have a high probability of becoming long lived
parts of the the project. After being merged, the code will run through a
series of testing pipelines on a large number of operating system
environments. These pipelines can reveal incompatibilities that are difficult
to detect in advance.

If the code change results in a test failure, we will make our best effort to
correct the error. If a fix cannot be determined and committed within 24 hours
of its discovery, the commit(s) responsible _may_ be reverted, at the
discretion of the committer and Puppet maintainers. This action would be taken
to help maintain passing states in our testing pipelines.

The original contributor will be notified of the revert in the Jira ticket
associated with the change. A reference to the test(s) and operating system(s)
that failed as a result of the code change will also be added to the Jira
ticket. This test(s) should be used to check future submissions of the code to
ensure the issue has been resolved.

### Summary
* Changes resulting in test pipeline failures will be reverted if they cannot
  be resolved within one business day.

# Additional Resources

* [Puppet community guidelines](https://docs.puppet.com/community/community_guidelines.html)
* [Bug tracker (Jira)](https://tickets.puppetlabs.com)
* [Contributor License Agreement](http://links.puppet.com/cla)
* [General GitHub documentation](https://help.github.com/)
* [GitHub pull request documentation](https://help.github.com/articles/creating-a-pull-request/)
* #puppet-dev IRC channel on freenode.org ([Archive](https://botbot.me/freenode/puppet-dev/))
* [puppet-dev mailing list](https://groups.google.com/forum/#!forum/puppet-dev)
* [Community PR Triage notes](https://github.com/puppet-community/community-triage/tree/master/core/notes)


