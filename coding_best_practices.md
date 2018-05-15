Python:
-------
1. Run flake8 linter https://github.com/kbase/project_guides/blob/master/RecommendedEditors.md.

Java:
-----
1. Make sure PR is made to dev branch.
2. Check for Merge conflicts.
3. Add release notes
4. previous review comments addressed
5. All tests exist in build.xml test class list.
6. All tests pass and coverage is not negative.
7. Test coverge must include exception code.
8. Code is well documented.
9. Code formatting, 
  </br><ul>- Code lines are within the 100 char limit.</ul>
  </br><ul>- methods are within the 150 line limit. </ul>
10 Remove unused import statements and other unused code. 
11. Ensure that the right set of exceptions are caught and no high level exceptions that cast a broad net are being used.
12. Typos in documentation.
13. Check for DRY.
14. Use final for all vars to ensure 100% immutability.
15. Local vars are private.
16. Always use brackets code blocks (even for inline statements)
17. Add spaces after keywords like if, else, for, throw etc. to differentiate them from function calls. 
      </br><ul>- Search for "for(" "if(" "switch(" "while(".</ul>
18. Use [Utils.notNullorEmpty() or Utils.notNull()](https://github.com/kbase/KBaseSearchEngine/blob/master/lib/src/kbasesearchengine/tools/Utils.java) type utilities. Better still, use [Guava](https://github.com/google/guava/wiki) for proper treatment of optional vars.
19. Use "public/private static final String" declarations instead of string literals in code. 
