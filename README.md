# Documentation
Personal documentation on processes and scripts.

## Reading
- Clean Code (Blog): <https://blog.cleancoder.com>
- Clean Code (Book): <https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882>
- Clean Architecture: <https://khalilstemmler.com/articles/software-design-architecture/organizing-app-logic/>
- Javascript Weekly <https://javascriptweekly.com>
- React Newsletter: <http://reactjsnewsletter.com>
- Agile Culture: <https://docs.microsoft.com/en-us/azure/devops/learn/agile/agile-culture>
- Semantic Versioning: <https://semver.org/>

## Coding Practices
- Only 1 return statement per function
- Minimize use switch case statements, prefer object structures
- Name constants that aren't clear.
  + What is `LL` for a date format? Assign to good variable name and leave comment that shows a sample rendered date
- Variable names should spelled out, rarely use abbreviations
- No types in variable names. prefer `names` vs `namesArray`
- no `log` messages for normal code paths/flow. Use sparingly and good use cases, prefer logging `error` and `warn` messages vs `info`

### JavaScript
  + `export` statement should be last line of file, don't use export defaults 
  + <https://humanwhocodes.com/blog/2019/01/stop-using-default-exports-javascript-module/>
