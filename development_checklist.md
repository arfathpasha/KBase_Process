Checklist for developing KBase Apps:
------------------------------------

1. Fetch and merge latest revision from upstream kbaseapps repo into your personal github account, or make a new fork of upstream repo

2. Create a separate branch

3. Run unit tests as baseline and fix any existing failuers/errors that may exist

4. Implement the required functionality

5. Check for division by 0 errors!

6. Make judicious (re)use of utils modules like DatafileUtil, GenomeFileUtil, ReadsAlignmentUtil etc. 

7. If parallelization is required, use kb_parallel (see kb_bowtie for its use of kb_parallel)

8. Write unit tests to cover the newly implemented code

9. Check to make sure provenance information is captured in the result

10. Check to make sure your code is well documented

11.  Make sure all unit test data is local to the module

12.  Set up a (travis build)[/travis.md] for the app

13. Make sure your code has at least 85% unit test coverage

14. Run flake8 linter https://github.com/kbase/project_guides/blob/master/RecommendedEditors.md

15. Add UI narrative interface metadata (if required) in ui/narrative/methods dir

16. If it is a newly created kbase module, make sure to rename the dir ui/narrative/methods/example_method to the appropriate method name in the module spec.

17. Update readme.md with introductory information about the app that app developers might find useful

18. Add module function description + examples in kbase.yml that app users might find useful (this info is presented on the narrative)

19. Increase kbase app version number in kbase.yml

20. If another app is being wrapped as a kbase app, make sure to add wrapped app version number to module-description in kbase.yml

21. Add changelog in release notes (release_notes.md)

22. Before making a PR, check upstream repo for additional commits since some time may have elapsed since your initial fetch. If present, fetch, merge, retest against upstream commits.

23. [Squash commits](https://makandracards.com/makandra/527-squash-several-git-commits-into-a-single-commit) before making a PR to make the PR easier to review

24. Add Jira ticket number to PR title

25. Once PR is merged, register in CI and appdev

26. Verify output report presentation on module catalog and on narrative

27. Test app on CI and appdev narrative interfaces

28. Make narrative public and add narrative URL containing a successful run to the jira ticket and move ticket to Review state

29. Once PR is reviewed, upgrade development version to beta version on CI and appdev

30. Run through this checklist again for each iterative refinement that may need to be applied to the app
