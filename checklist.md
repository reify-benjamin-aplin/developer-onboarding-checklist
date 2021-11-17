This checklist walks a new developer through our projects and build processes._
# First Steps Checklist
* [x] Slack our IT administator (currently Rich) to schedule a 30 minute call to walk through our policy for securely managing your laptop
* [x] Create a new Reify-specific GitHub account.
* [x] Create a [Access Request card](https://reifyhealth.atlassian.net/wiki/spaces/IT/pages/1075970084/How+to+request+account+access+revocation) to be invited to the Reify Github org. Be sure to include your username.
* [x] Ensure you have a private reify directory in your home directory: `mkdir -p ~/.reify`
* [x] Install Java JDK 11 or newer: `brew install openjdk@11`
* [ ] Set up SSH per the instructions in [`lein-git-down`](https://github.com/reifyhealth/lein-git-down/#private-repositories-ssh-authentication):
  * [x] Generate SSH key and add it to the ssh-agent as per [this doc](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (*Important Note*: add `-m PEM` as an argument to the command `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` as in `ssh-keygen -t rsa -b 4096 -m PEM -C "your_email@example.com"`)
  * [x] [Create a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/). Please make sure your SSH key is stored safely. This key should be strictly used for business purposes. Do not use this key on any of your personal accounts.

## Development Data Setup
Each app will have its own dependencies (direnv, nodejs etc). Both apps will be using github packages and homegrown tools so make sure that you start with the Bengal setup so that you'll be able to automatically pull in those dependencies with the required config variables.

# First End to End Run
You need Bengal and Salk up and running in order to have StudyTeam fully functional. Follow the below docs in order to get those up and running and visit `http://studyteamapp.local:2999/site/site-selector?demo=0` for the ["remote"](https://github.com/reifyhealth/salk#demo-vs-remote-mode) version of the app that interacts with a live local Bengal backend.

### Bengal Specific Instructions
To set up your development environment for the first time, follow [these instructions](https://github.com/reifyhealth/bengal#set-up-development-environment). You should be able to do the following three things:
  * [ ] [Set up development and test database](#development-data-setup)
  * [ ] [Run tests](https://github.com/reifyhealth/bengal#testing)
  * [ ] [Run the REPL](https://github.com/reifyhealth/bengal#repl-startup)

### Salk Specific Instructions
Once you've confirmed that you can run `bengal` in the command line and you have local databases set up, follow the setup instructions for [`salk`](https://github.com/reifyhealth/salk#local-development-quick-start). You should be able to do the following things:
* [ ] Set up [`salk` and `salk-sponsor`,](https://github.com/reifyhealth/salk)
  * [ ] Set up [styling](https://github.com/reifyhealth/salk#compiling-the-css-stylesheet) and build CSS/SASS assets
  * [ ] Run [tests](https://github.com/reifyhealth/salk#testing) for all targets, including remote integration tests
  * [ ] [Run the apps](https://github.com/reifyhealth/salk#compiling-and-running-applications) in demo mode

After launching `salk` and logging in, you should be able to see the trial and other patient data automatically generated. You should also be able to add additional users to your trial. When logging in as a sponsor user, you should also be able to see the trial overview. There are two apps here that you would need to run independently:
  * [ ] Run `salk` app as dev build in [remote mode](https://github.com/reifyhealth/salk#demo-vs-remote-mode). Visit it in your browser.
  * [ ] Run `salk-sponsor` app as dev build in remote mode. Visit it in your browser.
  * [ ] Run `salk` and `salk-sponsor` apps as prod build and then try visiting them both in your browser while the Bengal server is running.
  * [ ] Read through all the architecture docs in the ReadME.

## StudyTeam Documents

### Backend services - eDOA and eSource

The setup of both projects [`eDOA`](https://github.com/reifyhealth/edoa-service) and [`eSource`](https://github.com/reifyhealth/esource-service) requires the installation of these tools, as described in the Readme of [eSource](https://github.com/reifyhealth/esource-service#requirements) project. As those projects work the same, you can apply the same bellow for both:
  * [ ] [Quickstart and REPL](https://github.com/reifyhealth/esource-service#quickstart)
  * [ ] [Run Tests](https://github.com/reifyhealth/esource-service#test)

### Frontend services - Study Sheet and eDOA React Components

Once getting the Backend services running, you can start the [`Study Sheet`](https://github.com/reifyhealth/study-sheet) service, that its the frontend of StudyTeam Documents product.
  * [ ] [Requirements](https://github.com/reifyhealth/study-sheet#requirements)
  * [ ] [Quickstart](https://github.com/reifyhealth/study-sheet#requirements)
  * [ ] [Commands](https://github.com/reifyhealth/study-sheet#requirements)

# Miscellaneous
* [ ] Set up [pantry](https://github.com/reifyhealth/pantry) which is a shared package of spec definitions and other utility function used in Bengal and Salk. This will already be pulled into Salk and Bengal but you can peruse it locally if you ever end up contributing to it.
  * [ ] Run tests
* [ ] Check out [serde](https://github.com/reifyhealth/serde) for another shared resource of de-serialization utilities that are shared across applications.
* [ ] If you haven't had a product walkthrough, try some of the features using the [QA scripts](https://github.com/reifyhealth/qa-docs/blob/master/QA.md#areas-to-qa) as a guide. Please reach out to the QA team if you have questions on what is most useful or interesting to QA.
* [ ] Set up and try [hooke](https://github.com/reifyhealth/hooke), the admin application
  * [ ] Install [yarn](https://yarnpkg.com/) and build `hooke`
  * [ ] Add `{"role": "reifyadmin"}` under `app_metadata` to the admin Auth0 user (`<name>+admin-local@reifyhealth.com`) on the [Users page](https://manage.auth0.com/#/users)
  * [ ] Run `hooke` server
  * [ ] Run `bengal` server and verify `hooke` can interact with `bengal`
  * [ ] Try a couple of workflows mentioned in [this guide](https://reifyhealth.atlassian.net/wiki/spaces/QA/pages/253132897/StudyTeam+Configuration+Guide)

## Setup StudyTeam accounts

### Testing accounts

1. Provide a fellow engineer with your templated local account email address, e.g. first.last+admin-local@reifyhealth.com
2. Ask them to create an admin user for you in Hooke, e.g. first.last+admin-testing@reifyhealth.com
   1. Now your user has been created in the database and in the "reify-us-testing" Auth0 tenant
3. Ask them to enable admin-app rights for you. Can be done either:
   1. via Retool > Onboarding > Admin
   2. via adding app_metadata `"role": "reifyadmin"` in "reify-us-testing" Auth0 tenant
4. At this point you should be able to log into Hooke (perhaps requiring a password reset first)
   1. Now you can create your sponsor/site users in User Configuration
   2. Finally, you can give appropriate Site Grant and Trial Grant entries via Site Configuration and Sponsor Configuration.

### Staging and production accounts

1. Slack any of the tech leads with a request to create your staging account. They will
create accounts with dummy passwords. Note to tech leads:
   * Create accounts in Hooke. Email suffix convention to use for each new account: `$reify_email+$app-$environment` e.g. `khiem+site-staging@reifyhealth.com`. /site/, /sponsor/ and /admin/ respectively have $app values of 'site', 'sponsor' and 'admin'. $environment values are 'staging' and 'production'.
   * Set up example data for each account e.g. make it an admin or give it a Site Grant or Trial Grant.
   * Give the requester the emails you have created along with dummy password.
1. With given emails, log in and confirm example data in account.
1. For each account, reset its password from the login page. Save updated password to 1Password.

* [ ] Confirm StudyTeam [testing](https://testing.studyteamapp.com) login works and that you can see example data.
* [ ] Confirm StudyTeam [staging](https://staging.studyteamapp.com) login works and that you can see example data.
