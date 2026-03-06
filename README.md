# CS296N-Example-BookReviews-DotNet6

- Book Review example code from LCC-CIT/CS295N-Example-BookReviews was migrated to ASP.NET 6.0 MVC.  
  - The migration process is described in https://lcc-cit.github.io/CS295N-CourseMaterials/Notes/UpgradeMvcAppToDotNeT6.html
- This example uses both MySQL and SQLite database providers--selectable by preprocessor directives.  
  - This guide shows how to set up a MySQL database server on Azure: https://lcc-cit.github.io/CS295N-CourseMaterials/Notes/AzureMySqlSetupGuide.html
- Winter term 2026 some branches were updated to .NET 10.0.

## Branchs
- 01-FromLastTerm
  - This is the code from CS 295N (last term.)
- 02-Identity
- 03-Authentication
- 04-Authorization
- 04B-Auth+SeedUsersWRoles
- 05-Async
- 07-ComplexDomain
- 08-Validation
  - Added validation attributes to the models
  - Revised Review.cshtml to use the Review model and to get the book title from the ViewBag
- W26-Validation  
  - Updated this branch to use .NET 10.0 and added code to validate the input when creating a new review.
- W26-NET10-Authentication
  - Added code to authenticate users using ASP.NET Identity
- W26-NET10-Authorization
  - Added code to authorize users using ASP.NET Identity

