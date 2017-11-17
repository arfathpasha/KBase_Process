Checklist for developing KBase Apps:
------------------------------------

1. Plan ahead on making PRs that are no more than 400 lines of code so reviewers can be more effective.

2. Fetch and merge latest revision from upstream kbaseapps repo into your personal github account, or make a new fork of upstream repo.

3. Create a separate branch.

4. Run unit tests as baseline and fix any existing failuers/errors that may exist.

5. Implement the required functionality.

6. Check for division by 0 errors!

7. Make judicious (re)use of utils modules like DatafileUtil, GenomeFileUtil, ReadsAlignmentUtil etc. 

8. If parallelization is required, use kb_parallel (see kb_bowtie for its use of kb_parallel).

9. Write unit tests to cover the newly implemented code.

10. Check to make sure provenance information is captured in the result.

11. Check to make sure your code is well documented.

12.  Make sure all unit test data is local to the module.

13.  Set up a [travis build](/travis.md) for the app.

14. Make sure your code has at least 85% unit test coverage.

15. Apply [coding best practices](/coding_best_practices.md).

16. Add UI narrative interface metadata (if required) in ui/narrative/methods dir.

17. If it is a newly created kbase module, make sure to rename the dir ui/narrative/methods/example_method to the appropriate method name in the module spec.

18. Update readme.md with introductory information about the app that app developers might find useful.

19. Add module function description + examples in kbase.yml that app users might find useful (this info is presented on the narrative).

20. Increase kbase app version number in kbase.yml.

21. If another app is being wrapped as a kbase app, make sure to add wrapped app version number to module-description in kbase.yml.

22. Add changelog in release notes (release_notes.md).

23. Before making a PR, check upstream repo for additional commits since some time may have elapsed since your initial fetch. If present, fetch, merge, retest against upstream commits.

24. If your branch has a [messy commit history](https://github.com/blog/2141-squash-your-commits), you may wish to [squash commits](https://makandracards.com/makandra/527-squash-several-git-commits-into-a-single-commit) before making a PR to make the PR easier to review.

25. Add Jira ticket number to PR title.

26. Once PR is merged, register in CI and appdev.

27. Verify output report presentation on module catalog and on narrative.

28. Test app on CI and appdev narrative interfaces.

29. Make narrative public and add narrative URL containing a successful run to the jira ticket and move ticket to Review state.

30. Once PR is reviewed, upgrade development version to beta version on CI and appdev.

31. Run through this checklist again for each iterative refinement that may need to be applied to the app.
