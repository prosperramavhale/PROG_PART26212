# RaceDay troubleshooting

## The solution does not build
- Install the .NET 8 SDK (Visual Studio Installer can add the ASP.NET and web development workload).
- In Visual Studio, use Build > Restore NuGet Packages, then Build > Rebuild Solution.
- If the error mentions a package source, check internet access and restore again.
- Copy the first actual error from the Error List or Output window. Do not rely only on the last cascading error.

## The API opens but the database fails
- The project uses SQL Server LocalDB by default: `(localdb)\MSSQLLocalDB`.
- Install **SQL Server Express LocalDB** using Visual Studio Installer > Modify > Individual components, or change the connection string in `RaceDay.API/appsettings.json` to your SQL Server instance.
- The API applies its initial migration at startup. Do not run the destructive Part 1 SQL script against a database containing data you need.

## Swagger does not open
- Confirm `RaceDay.API` is the startup project and the launch profile is `RaceDay.API`.
- Run with F5 or Ctrl+F5. Use the URL shown in the terminal/Output window and append `/swagger`.
- Swagger is enabled in Development and Testing environments only.

## Tests fail
- Run `RUN-TESTS.bat` or `dotnet test RaceDay.sln --configuration Release` from the solution folder.
- The tests use EF Core InMemory and do not require LocalDB.
- Fix errors before capturing any test evidence. Do not present a failed run as successful.
