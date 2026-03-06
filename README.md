# CS296N-Example-BookReviews-DotNet6

- Book Review example code from LCC-CIT/CS295N-Example-BookReviews was migrated to ASP.NET 6.0 MVC.  
  The migration process is described in https://lcc-cit.github.io/CS295N-CourseMaterials/Notes/UpgradeMvcAppToDotNeT6.html
- This example uses both MySQL and SQLite database providers--selectable by preprocessor directives.  
  This guide shows how to set up a MySQL database server on Azure: https://lcc-cit.github.io/CS295N-CourseMaterials/Notes/AzureMySqlSetupGuide.html
- Winter term 2026 some branches were updated to .NET 10.0.

 ## Branchs
 - 7-RepositoryAndUnitTests  
  The repository pattern is implemented to facilitate unit testing of controller methods.  
  A ReviewRepository was added and the ReviewController was refactored to use it. A FakeReviewRepository was added and unit tests were written that use it.
- 8A-SeedData  
  Code to seed the database with some initial book reviews was added.
- 8B-LinqFiltering  
  Added code to filter reviews by book title or reviewer.
- W26-Validation  
  Updated this branch to use .NET 10.0 and added code to validate the input when creating a new review.
- W26-NET10-Authentication
  Added code to authenticate users using ASP.NET Identity
- W26-NET10-Authorization
  Added code to authorize users using ASP.NET Identity