# CS296N Example: BookReviews
Book Review example from LCC-CIT/CS295N-Example-BookReviews migrated to ASP.NET 6.0 MVC
The last two branches have been updated to .NET 10

This example uses a MySQL database. This guide shows how to set up a MySQL database server on Azure: https://lcc-cit.github.io/CS295N-CourseMaterials/Notes/AzureMySqlSetupGuide.html

## Branchs
- 01-FromLastTerm.
- 02-Identity
- 03-Authentication
- 04-Authorization
- 04B-Auth+SeedUsersWRoles
- 05-Async
- 06
- 07-ComplexDomain
- 08-Validation
  - Added validation attributes to the models
  - Revised Review.cshtml to use the Review model and to get the book title from the ViewBag
- W26-Validation  
  Updated this branch to use .NET 10.0 and added code to validate the input when creating a new review.
- W26-NET10-Authentication
  Added code to authenticate users using ASP.NET Identity
- W26-NET10-Authorization
  Added code to authorize users using ASP.NET Identity
- CI A branch with the GitHub Actions workflow file
