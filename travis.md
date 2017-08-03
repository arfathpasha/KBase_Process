Adding Travis and Coveralls coverage to your KBase Apps (2 hours):
-------------------------------------------------------------------
Prerequisites: <br>

A) Make sure you have the [Gem](https://rubygems.org/pages/download/) Ruby Package Manager. You will need this to encrypt your auth token.<br>

B) Install the travis tool with command ```gem install travis``` <br>

C) If you are setting up a python module, make sure your module's docker file has ```RUN pip install coverage```. Coveralls dependencies for other languages can be found [here](https://coveralls.zendesk.com/hc/en-us).

Steps:
1) Run unit tests to make sure all tests pass. 

2) Follow instructions in sections
   * [To Get Started with Travis CI](https://docs.travis-ci.com/user/getting-started/#To-get-started-with-Travis-CI) and, 
   * [Selecting-a-programming-language](https://docs.travis-ci.com/user/getting-started/#Selecting-a-programming-language)

3) Copy-paste from line 6 (sudo: required) of this [normative travis file](https://github.com/kbaseapps/kb_ballgown/blob/master/.travis.yml) into your module's .travis.yml and make the following changes. 
   * Change email in notifications section
   * Remove the line that begins with "secure:" that contains the encrypted auth token.
   * Add an encrypted auth token using the instruction ```travis encrypt TEST_TOKEN="[YOUR_TOKEN_HERE]" --add```
      * Make sure to add [YOUR_TOKEN_HERE] in the instruction above.
      * *Ideally*, you should use a long living service token. If you do not have one, then use your existing auth token and then create a ticket for a sys admin to redo this step for you with a service token. If you are using a service token, be aware of [these guidelines](/service_token.md).
   * Find-replace-all "kb_ballgown" with your module name.
   * You must start with getting travis to clone from your personal repo while you are setting it all up. So change the line, <br>"git clone https://github.com/kbaseapps/[YOUR_MODULE_NAME].git" to 
<br>"git clone https://github.com/[YOUR_GITHUB_NAME]/[YOUR_MODULE_NAME].git"
   
4) Copy-paste this [normative .coveragerc file](https://github.com/arfathpasha/kb_ballgown/blob/master/.coveragerc) into your module's root dir and make the following changes.
   * Find-replace-all "kb_ballgown" with your module name.
   
5) In your module's makefile, go to the "build-test-script:" target and add the following lines at the end of this target. Make sure to replace the string "[YOUR_MODULE_NAME]" in the last line with your module name. <br>
<pre>
   echo 'cp /kb/module/.coveragerc .' >> $(TEST_DIR)/$(TEST_SCRIPT_NAME) 
   echo 'coverage report -m' >> $(TEST_DIR)/$(TEST_SCRIPT_NAME) 
   echo 'cp .coverage /kb/module/work/' >> $(TEST_DIR)/$(TEST_SCRIPT_NAME) 
   echo 'mkdir -p /kb/module/work/kb/module/lib/' >> $(TEST_DIR)/$(TEST_SCRIPT_NAME) 
   echo 'cp -R /kb/module/lib/[YOUR_MODULE_NAME]/ /kb/module/work/kb/module/lib/' >> $(TEST_DIR)/$(TEST_SCRIPT_NAME) 
</pre>

6) Run ```make all``` to update test scripts.

7) Run ```kb-sdk test``` to check if coverage output is being displayed in stdout. The end of the output should look something like the output below. Note only kb_ballgown implementation files are being reported on. 
<pre>
Name                                               Stmts   Miss  Cover   Missing
    --------------------------------------------------------------------------------
    /kb/module/lib/kb_ballgown/__init__.py                 0      0   100%
    /kb/module/lib/kb_ballgown/core/__init__.py            0      0   100%
    /kb/module/lib/kb_ballgown/core/ballgown_util.py     229     23    90%   50, 57, 60-64, 204, 207, 216-217, 253-255, 265-267, 305-307, 324, 335, 339, 345, 425
    /kb/module/lib/kb_ballgown/kb_ballgownImpl.py         26      3    88%   90, 96-102
    --------------------------------------------------------------------------------
    TOTAL                                                255     26    90%
    Shutting down callback server...
</pre>

8) Turn on your module's repo in travis from the url https://travis-ci.org/profile/[YOUR_GITHUB_NAME]. Replace [YOUR_GITHUB_NAME] with your github name in the URL. If your repo name does not show up, click on the "Sync account" link on the top right.

9) Turn on your module's repo in coveralls from the url https://coveralls.io/repos/new. If your repo name does not show up, click on the "sync repos" link on the top right. 

10) Add the following markdown for the badges at the top of your module's README.md file. Make sure to replace the strings "<YOUR_GITHUB_NAME>" and "<YOUR_MODULE_NAME>" with your github and module's name.

<pre>
Build status:<br>
master: [![Coverage Status](https://coveralls.io/repos/github/[YOUR_GITHUB_NAME]/[YOUR_MODULE_NAME]/badge.svg?branch=master)](https://coveralls.io/github/[YOUR_GITHUB_NAME]/[YOUR_MODULE_NAME]?branch=master)<br>
master:  [![Build Status](https://travis-ci.org/[YOUR_GITHUB_NAME]/[YOUR_MODULE_NAME].svg?branch=master)](https://travis-ci.org/[YOUR_GITHUB_NAME]/[YOUR_MODULE_NAME])<br>
</pre>

11) Commit and push your changes to your forked github repo. You should now see an orange icon appear next to your commit log in github's commit log page. Clicking on this icon will take you to the travis build page. If the build is successful, the icon turns to a green check mark. The status of your build will be reported on the readme badges. 

12) To set up nightly builds, go to https://travis-ci.org/[YOUR_GITHUB_NAME]/[YOUR_MODULE_NAME]. Make sure to replace the strings [YOUR_GITHUB_NAME] and [YOUR_MODULE_NAME] in the URL. Follow the link "More Options"->"Settings" on the top right. Add a cron job to run daily.

13) Once you have it all set up and working through your forked repo, you may change the ``` git clone``` line in your .travis.yml file to clone your module from the "kbaseapps" github account instead of your personal account. Then make a commit, push and create a pull request. Once your changes have been merged to "kbaseapps", your CI test setup will begin testing the upstream "kbaseapps" repo each time a new revision is created and when the nightly build is triggered.  


Q&A:
----
1) <b>Q</b>: Why use travis? <br>
   Your software will almost always depend on other software. When these dependencies change, they can cause a cascading effect that breaks your software. With nightly builds setup through travis, you will be notified within 24 hours of a change that broke your software. It is much easier to fix the break right when it occurs than it is to fix weeks or months after the break occurs. 
 
 2) <b>Q</b>: Why use coveralls? <br>
    Stakeholders can get a quick idea of how reliable and maintainable a piece of software is from the coverage report. 
