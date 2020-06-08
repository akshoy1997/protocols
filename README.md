# Gmail Automater Developer Onboarding


Hi! Welcome to building for Gmail Automater. This document contains a list of tools the gmail automater team uses, a list of terms that will get thrown around a lot, and a simple protocol to get started with contributing to the gmail automater codebase.


### Tools we use

[Gmail Automater Trello Board](https://trello.com/b/b2VTL37v/) A scrum board for produt sprints, used to communicate what features are to be built, how, by whom, and to track their progress. Ask for an invite if you're not already there.

**Gmail Automater Codebase** hosts the codebase for our [Extension](https://github.com/sarthak-patidar/gmail-automater-extension), [API](https://github.com/sarthak-patidar/gmail-automater-api) and [NLP Engine](https://github.com/sarthak-patidar/gmail-automater-nlp-engine).

**Design Repository** for all design collaters for the product. <to be added>

### Terminology

1. `gmail-automater-extension`, `gmail-automater-api` and `gmail-automater-nlp-engine`: Three project repos with all the codebase of the product, self explanatory.
2. `Repository or Project`: Every component of the gmail automater codebase is stored in a git repository and hosted on Github.
3. `Develop Branch`: The main development branch of every repository. Can contain unstable code between releases.
4. `feature/` or `fix/` branch: Any feature branch that is necessarily to be named as `feature/feature-name` and a fix branch as `fix/fix-name`.
5. `pull-request`: A request to review a code merge from one brand to another.
6. `test branch`: A branch to build a test application or run automated tests scripts. Can be pushed into from any branch for testing.
7. `master branch`: Release ready code with production tags. Contains auto-deploy scripts on push to master, with only the project owners having permission to deploy.
8. `tags`: Every release (Internal or External) should be accompanied by tagging. Helps deploy rollbacks and have easy reference to deployed code.

### Development Protocol

#### *Getting Started*

1. Get assigned to one of the tasks for the product.
2. Clone the repository([Extension](https://github.com/sarthak-patidar/gmail-automater-extension), [API](https://github.com/sarthak-patidar/gmail-automater-api) or [NLP Engine](https://github.com/sarthak-patidar/gmail-automater-nlp-engine)) relevant to your task.
3. Read the README for the project to understand how to setup and run the project on your local machine.
4. If you want to know more about how git works, google up. Its a version control system to manage your codebase. A must read for all developers.
5. Every Repository will have a `master branch` that has the deployed/stable code, and a `develop branch`, where all the development code is being committed. This branch is up-to-date with latest changes.
6. Run `git checkout develop` in the project folder on your computer through terminal. Now you have the codebase in the develop branch of the project.


#### *Development*

1. Before starting new feature, `git checkout develop` and `git pull develop` to get the latest codebase.
2. Create a branch from develop for the feature or fix you are about to build with proper nomenclature: `feature/feature-name-is-this` or `fix/fix-name-is-this`.
3. Now write code and make commits to your branch till you think your feature or fix is ready to merge.
4. Few NON NEGOTIABLE coding/committing practices:
    
    * **Code Structure**
        ```
            * We use tabs (if you have a problem with this, then you can register a formal complaint with the project owners. EDIT: Its a pointless debate anyway, so lets do it this way.)
            * We use camelCase for naming functions, classes and variables (same as above).
            * All projects will follow a common linting or indentation process, so don't introduce anything new on your own. Ask the project owner.
            * Don't change other people's code indentation.
            * Write modular code. (Barfing all logic in a single file is not acceptable. Yes, we've all been at the receiving end of it. Yes, we've all made enemies.)
        ```

    * **Commits**
        ```
            * Make small commits with proper message.
            * Keep a 50 character length for each commit message.
            * Push your code to the project instead of keeping code in local for long. You have a risk of losing it.
            * try to make each commit runnable, even if its not releasable.
        ```
        
    * **Documentation**
        ```
            * Mention all hacks as <comment> Fix Me </comment> or <comment> ToDo </comment> above the code where this is mentioned.
            * Mention API documentation right above the documentation.
        ```
        
    1. Update your feature or fix branch everyday by pulling the develop branch into it. Will help preventing big merge conflicts later.
    2. Now once you are done developing the feature/fix, pull from develop one last time to update your branch.
    3. Use `git merge-tool` to pull up SourceTree or `git-kraken` in mac, or `meld` in linux for easily resolving merge conflicts. In case this doesn't work, meet the developer in question (mostly 10m or a phone call away).
    4. Create a `pull-request` from your branch to the develop branch. Mention all the things you want a developer to specifically check and a tester to specifically test. Egs.
    
        ```
            6fd91899: Mege branch 'fix-ota_file_corruption' into 'develop'
            
                Fix ota file corruption.
                
                To Check:
                - A
                - B
                - C
                
                To Test:
                - X
                - Y
                - Z
        ```
        
    1. Get your code reviewed from at least two developers in the team. Two developers must sign off on your PR for it to be merged.
    2. 1 test engineer needs to sign off on your PR before it is merged. His/Her role is to build and check the code for test cases, and document these test cases somewhere for future reference.
    3. If there are bugs to be solved in the features built, the tester will mention it in the pull-request.
    4. The developer must resolve these bugs in the same branch, re-update branch with the develop branch by pulling it, and re-open the PR.
    5. If all tests pass, the merge can be carried out.
    

#### *Internal/Test Release*

1. Every project has a `test` deployment and a `production` deployment. Pushing from `develop` to the `test` branch will deploy the code on the test url. See README on how to access the test url for each project.
2. `gmail-automater-extension` is the consumer of the services built on `gmail-automater-api`. So the features of API are always planned and released one cycle (1 week/2 weeks) ahead of the extension. So ideally, a service will be live on test server and production server for its extension UI to be developed.
3. Now let us say a combination of 3/4 features/fixes are ready. They should be deployed internally for testing.
4. Project Owner makes a list of features/fixes developed that are ready to be released.
5. Test Engineer tests a release build locally from the develop branch with all the listed features/fixes tested once manually.
6. Project owner updates the version code of the release in the code. `Version Code` is integer incremented on every internal or external release and `Version Name` is incremented only on an external release.
7. Version Name follows the `Major.Minor.Patch` nomenclature.
8. Project owner pushes to the test branch to deploy the release internally.
9. Project owner tags the commit as `vMAJOR.MINOR.PATCH_VERSIONCODE` (v1.1.2_42)

    ```
    NOTE: 
        
        * All developer testing of the gmail-automater-extension are to be done pointing to the Test API Server.
        * All internal releases of the gmail-automater-extension are to be done pointing to the Production API Server.
        * This should be added as a part of the config for each project. Please ask the project owner if this is not setup yet.
        * Test API Server is updated when Internal Release of `gmail-automater-api` takes place.
        * Production API Derver is updated when External Release of `gmail-automater-api` takes place.
    ```

#### *External/Production Release*

1. Developers carry out any bug fixes noted from Internal Release.
2. Project owner creates a release build with updated Version Name & Version Code from the Develop branch.
3. Test Engineer tests the release build one last time manually.
4. Project Owner updates the version code and version name of the release in the code. `Version Code` is integer incremented on every internal or external release and `Version Name` is incremented only on an external release.
5. Project Owner merges the Develop code to Master and tags the release commit with version of the app as (Must add “Release” as prefix if external release):
    `vRelease_MAJOR.MINOR.PATCH_VERSIONCODE ((vRelease_1.1.3_43))`
6. Pushing to Master should auto-deploy the build to production.
7. Team check if go-live was successful on production servers.
