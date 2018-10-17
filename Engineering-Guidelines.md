Engineering guidelines
======================

* [Basics](#basics)
* [Source code management](#source-code-management)
* [Coding guidelines](#coding-guidelines)
* [Testing PRs](#testing-prs)
* [Product planning and issue tracking](#product-planning-and-issue-tracking)
* [Breaking changes](#breaking-changes)
* [Tips and tricks](#tips-and-tricks)
* [Keep an eye on the CI](#keep-an-eye-on-the-ci)

## Basics

### Copyright header and license notice

All source code files (mostly `src/**/*.cs` and `test/**/*.cs`) require this exact header (please do not make any changes to it):

```c#
// Copyright (c) .NET Foundation. All rights reserved.
// Licensed under the Apache License, Version 2.0. See License.txt in the project root for license information.
```

It is ok to skip it on generated files, such as `*.designer.cs`.

Every repo also needs the Apache 2.0 License in a file called LICENSE.txt in the root of the repo. Please use only identical copies to what we have in other repos.

(There are some exceptions to this, but they need to be approved by @eilon.)


### External dependencies

This refers to dependencies on projects (i.e. NuGet packages) outside of the `aspnet` repo, and especially outside of Microsoft. Because these repos are a core part of all ASP.NET/EF apps, it is important that we be careful and manage our dependencies properly.

*Adding* or *updating* any external dependency requires approval from @eilon and @damianedwards. After you have gotten approval you must also update [this](https://github.com/aspnet/Universe/blob/master/build/external-dependencies.props) file to contain the dependency you're adding.

Dependencies that are used only in test projects and build tools are not nearly as rigid, but still require approval from @eilon.

There is also an OSS-approval process that has to be followed (to be done by @eilon).

### Code reviews and checkins

To help ensure that only the highest quality code makes its way into the project, please submit all your code changes to GitHub as PRs. This includes runtime code changes, unit test updates, and updates to official samples (e.g. Music Store). For example, sending a PR for just an update to a unit test might seem like a waste of time but the unit tests are just as important as the product code and as such, reviewing changes to them is also just as important. This also helps create visibility for your changes so that others can observe what is going on.

The advantages are numerous: improving code quality, more visibility on changes and their potential impact, avoiding duplication of effort, and creating general awareness of progress being made in various areas.

In general a PR should be signed off (using GitHub's "approve" feature) by the Subject Matter Expert (SME) of that code. For example, a change to the Banana project should be signed off by `@MrMonkey`, and not by `@MrsGiraffe`. If you don't know the SME, please talk to one of the engineering leads and they will be happy to help you identify the SME. Of course, sometimes it's the SME who is making a change, in which case a secondary person will have to sign off on the change (e.g. `@JuniorMonkey`).

To commit the PR to the repo either use GitHub's "Squash and Merge" button on the main PR page, or do a typical push that you would use with Git (e.g. local pull, rebase, merge, push).


## Source code management

:grey_exclamation: The *structure* of the code that we write and the *tools* that we use to write the code.


### Repos

To create a new repo in the https://github.com/aspnet/ org, contact @eilon.


### Build numbers

By default, builds of Library Manager projects will produce versions based on using [Nerdbank.GitVersioning](https://github.com/AArnott/Nerdbank.GitVersioning).

### Branch strategy

In general:

* `master` has the code that is being worked on but not yet released. This is the branch into which developers normally submit pull requests and merge changes into.
  - Currently `master` contains work for the Dev16.0 release.
* `release/Dev<major>.<minor>` contains code that is intended for release. The `<major>.<minor>` part of the branch name indicates the VS release that the branch is targeting for release. The branch may be used for several patch releases with the same major.minor number.
  - External contributors do not normally need to make pull requests to these branches. However, when multiple releases are in simultaneous development, targeting a release branch may be preferred.

#### Making changes to release branches

If you make a change to a `release/*` branch directly, you typically also need to merge those changes back to `master`. This often causes some merge conflicts, so make sure to proceed carefully. If you're not sure how to do this, follow these steps.

##### Manual merges to master

```sh
# Make your changes to release/x.y
git checkout release/x.y    
git merge --ff-only your-name/my-approved-PR-branch
git push

# Make sure master is up to date first
git checkout master
git pull 

# Prepare your merge on a separate branch

git checkout --branch your-name/merge-release-x-y-to-master
git merge --no-commit release/x.y

# This is where you need to manually check your changes are good

git commit -m "Merge branch release/x.y into master"
git push -u origin your-name/merge-release-x-y-to-master

# Open a PR to review the changes

# Once approved
git checkout master
git merge --ff-only your-name/merge-release-x-y-to-master
git push
```

### Solution and project folder structure and naming

Solution files go in the repo root.

Solutions need to contain solution folders that match the physical folders (`src`, `test`, etc.).

For example, in the `Fruit` repo with the `Banana` and `Lychee` projects you would have these files checked in:

```
/Fruit.sln
/src/Microsoft.AspNet.Banana/Banana.csproj
/src/Microsoft.AspNet.Banana/Banana.cs
/src/Microsoft.AspNet.Banana/Util/BananaUtil.cs
/src/Microsoft.AspNet.Lychee/Lychee.csproj
/src/Microsoft.AspNet.Lychee/Lychee.cs
/src/Microsoft.AspNet.Lychee/Util/LycheeUtil.cs
/test/Microsoft.AspNet.Banana.Tests/BananaTest.csproj
/test/Microsoft.AspNet.Banana.Tests/BananaTest.cs
/test/Microsoft.AspNet.Banana.Tests/Util/BananaUtilTest.cs
```


### Conditional compilation for multiple Target Frameworks

Code sometimes has to be written to be target framework-specific due to API changes between frameworks. Use `#if` statements to create these conditional code segments:
Desktop:

```c#
#if NET46
            Console.WriteLine("Hi .NET 4.6");
#elif NETCOREAPP2_0
            Console.WriteLine("Hi .NET Standard 2.0");
#else
#error Target framework needs to be updated
#endif
```

Note the `#error` section that is present in case the target frameworks change - this ensure that we don't have dead code in the projects, and also no missing conditions.


### Assembly naming pattern

The general naming pattern is `Microsoft.Web.LibraryManager.<Platform>`, where `<Platform>` refers to the environment in which the tool is exposed.

### Unit tests

We use VSTest for all unit testing.

### Integration tests

We use an automation framework built internally for automating Visual Studio, named Apex.  Binaries for this library are made available publicly through MyGet.

### Repo-specific Samples

Some repos will have their own sample projects that are used for testing purposes and experimentation. Please ensure that these go in a `samples/` sub-folder in the repo.


## Coding guidelines

:grey_exclamation: The *content* of the code that we write.


### Coding style guidelines – general

The most general guideline is that we use all the VS default settings in terms of code formatting, except that we put `System` namespaces before other namespaces (this used to be the default in VS, but it changed in a more recent version of VS).

1. Use four spaces of indentation (no tabs)
2. Use `_camelCase` for private fields
3. Avoid `this.` unless absolutely necessary
4. Always specify member visibility, even if it's the default (i.e. `private string _foo;` not `string _foo;`)
5. Open-braces (`{`) go on a new line
6. Use any language features available to you (expression-bodied members, throw expressions, tuples, etc.) as long as they make for readable, manageable code.
   * This is pretty bad: `public (int, string) GetData(string filter) => (Data.Status, Data.GetWithFilter(filter ?? throw new ArgumentNullException(nameof(filter))));`


### Usage of the var keyword

The `var` keyword is to be used only when the return type of a method is apparent. For example, these are correct:

```c#
string fruit = "Lychee";
var fruits = new List<Fruit>();
bool tasty = fruit.IsTasty();
string fruit = null; // can't use "var" because the type isn't known (though you could do (string)null, don't!)
const string expectedName = "name"; // can't use "var" with const
```

The following are incorrect:

```c#
var fruit = "Lychee"; // don't use var for built-in types
List<Fruit> fruits = new List<Fruit>();  // when the type is apparent, var can be used
FruitFlavor flavor = fruit.GetFlavor();
```


### Use C# type keywords in favor of .NET type names

When using a type that has a C# keyword the keyword is used in favor of the .NET type name. For example, these are correct:

```c#
public string TrimString(string s) {
    return string.IsNullOrEmpty(s)
        ? null
        : s.Trim();
}

var intTypeName = nameof(Int32); // can't use C# type keywords with nameof
```

The following are incorrect:

```c#
public String TrimString(String s) {
    return String.IsNullOrEmpty(s)
        ? null
        : s.Trim();
}
```

### Cross-platform coding

Our frameworks should work on CoreCLR, which supports multiple operating systems. Don't assume we only run (and develop) on Windows. Code should be sensitive to the differences between OS's. Here are some specifics to consider.

#### Line breaks
Windows uses `\r\n`, OS X and Linux uses `\n`. When it is important, use `Environment.NewLine` instead of hard-coding the line break.

Note: this may not always be possible or necessary. 

Be aware that these line-endings may cause problems in code when using `@""` text blocks with line breaks.

#### Environment Variables

OS's use different variable names to represent similar settings. Code should consider these differences.

For example, when looking for the user's home directory, on Windows the variable is `USERPROFILE` but on most Linux systems it is `HOME`.

```c#
var homeDir = Environment.GetEnvironmentVariable("USERPROFILE") 
                  ?? Environment.GetEnvironmentVariable("HOME");
```

#### File path separators

Windows uses `\` and OS X and Linux use `/` to separate directories. Instead of hard-coding either type of slash, use [`Path.Combine()`](https://msdn.microsoft.com/en-us/library/system.io.path.combine(v=vs.110).aspx) or [`Path.DirectorySeparatorChar`](https://msdn.microsoft.com/en-us/library/system.io.path.directoryseparatorchar(v=vs.110).aspx).

If this is not possible (such as in scripting), use a forward slash. Windows is more forgiving than Linux in this regard.


### When to use internals vs. public and when to use InternalsVisibleTo

As a modern set of frameworks, usage of internal types and members is allowed, but discouraged.

`InternalsVisibleTo` is used only to allow a unit test to test internal types and members of its runtime assembly. We do not use `InternalsVisibleTo` between two runtime assemblies.

If two runtime assemblies need to share common helpers then we will use a "shared source" solution with build-time only packages. Check out the some of the projects in https://github.com/aspnet/Common/ and how they are referenced from other solutions.

If two runtime assemblies need to call each other's APIs, the APIs must be public. If we need it, it is likely that our customers need it.


### Async method patterns

By default all async methods must have the `Async` suffix. There are some exceptional circumstances where a method name from a previous framework will be grandfathered in.

Passing cancellation tokens is done with an optional parameter with a value of `default(CancellationToken)`, which is equivalent to `CancellationToken.None` (one of the few places that we use optional parameters). The main exception to this is in web scenarios where there is already an `HttpContext` being passed around, in which case the context has its own cancellation token that can be used when needed.

Sample async method:

```c#
public Task GetDataAsync(
    QueryParams query,
    int maxData,
    CancellationToken cancellationToken = default(CancellationToken))
{
    ...
}
```


### Extension method patterns

The general rule is: if a regular static method would suffice, avoid extension methods.

Extension methods are often useful to create chainable method calls, for example, when constructing complex objects, or creating queries.

Internal extension methods are allowed, but bear in mind the previous guideline: ask yourself if an extension method is truly the most appropriate pattern.

The namespace of the extension method class should generally be the namespace that represents the functionality of the extension method, as opposed to the namespace of the target type. One common exception to this is that the namespace for middleware extension methods is normally always the same is the namespace of `IAppBuilder`.

The class name of an extension method container (also known as a "sponsor type") should generally follow the pattern of `<Feature>Extensions`, `<Target><Feature>Extensions`, or `<Feature><Target>Extensions`. For example:

```c#
namespace Food {
    class Fruit { ... }
}

namespace Fruit.Eating {
    class FruitExtensions { public static void Eat(this Fruit fruit); }
  OR
    class FruitEatingExtensions { public static void Eat(this Fruit fruit); }
  OR
    class EatingFruitExtensions { public static void Eat(this Fruit fruit); }
}
```

When writing extension methods for an interface the sponsor type name must not start with an `I`.


### Doc comments

The person writing the code will write the doc comments. Public APIs only. No need for doc comments on non-public types.

Note: Public means callable by a customer, so it includes protected APIs. However, some public APIs might still be "for internal use only" but need to be public for technical reasons. We will still have doc comments for these APIs but they will be documented as appropriate.


### Unit tests and functional tests


#### Assembly naming

The unit tests for the `Microsoft.Fruit` assembly live in the `Microsoft.Fruit.Tests` assembly.

The functional tests for the `Microsoft.Fruit` assembly live in the `Microsoft.Fruit.IntegrationTests` assembly.

In general there should be exactly one unit test assembly for each product runtime assembly. In general there should be one functional test assembly per repo. Exceptions can be made for both.


#### Unit test class naming

Test class names end with `Test` and live in the same namespace as the class being tested. For example, the unit tests for the `Microsoft.Fruit.Banana` class would be in a `Microsoft.Fruit.BananaTest` class in the test assembly.


#### Unit test method naming

Unit test method names must be descriptive about *what is being tested*, *under what conditions*, and *what the expectations are*. Pascal casing and underscores can be used to improve readability. The following test names are correct:

```
PublicApiArgumentsShouldHaveNotNullAnnotation
Public_api_arguments_should_have_not_null_annotation
```

The following test names are incorrect:

```
Test1
Constructor
FormatString
GetData
```


#### Unit test structure

The contents of every unit test should be split into three distinct stages, optionally separated by these comments:

```c#
// Arrange  
// Act  
// Assert 
```

The crucial thing here is that the `Act` stage is exactly one statement. That one statement is nothing more than a call to the one method that you are trying to test. Keeping that one statement as simple as possible is also very important. For example, this is not ideal:

```c#
int result = myObj.CallSomeMethod(GetComplexParam1(), GetComplexParam2(), GetComplexParam3());
```

This style is not recommended because way too many things can go wrong in this one statement. All the `GetComplexParamN()` calls can throw for a variety of reasons unrelated to the test itself. It is thus unclear to someone running into a problem why the failure occurred.

The ideal pattern is to move the complex parameter building into the `Arrange` section:

```c#
// Arrange
P1 p1 = GetComplexParam1();
P2 p2 = GetComplexParam2();
P3 p3 = GetComplexParam3();

// Act
int result = myObj.CallSomeMethod(p1, p2, p3);

// Assert
Assert.AreEqual(1234, result);
```

Now the only reason the line with `CallSomeMethod()` can fail is if the method itself blew up. This is especially important when you're using helpers such as `ExceptionHelper`, where the delegate you pass into it must fail for exactly one reason.


### Testing exception messages

In general testing the specific exception message in a unit test is important. This ensures that the exact desired exception is what is being tested rather than a different exception of the same type. In order to verify the exact exception it is important to verify the message.

To make writing unit tests easier it is recommended to compare the error message to the RESX resource. However, comparing against a string literal is also permitted.

```c#
var ex = Assert.Throws<InvalidOperationException>(
    () => fruitBasket.GetBananaById(1234));
Assert.Equal(
    Strings.FormatInvalidBananaID(1234),
    ex.Message);
```

#### Parallel tests

By default all unit test assemblies should run in parallel mode, which is the default. Unit tests shouldn't depend on any shared state, and so should generally be runnable in parallel. If the tests fail in parallel, the first thing to do is to figure out *why*; do not just disable parallel tests!

For functional tests it is reasonable to disable parallel tests.


### Use only complete words or common/standard abbreviations in public APIs

Public namespaces, type names, member names, and parameter names must use complete words or common/standard abbreviations.

These are correct:
```c#
public void AddReference(AssemblyReference reference);
public EcmaScriptObject SomeObject { get; }
```

These are incorrect:
```c#
public void AddRef(AssemblyReference ref);
public EcmaScriptObject SomeObj { get; }
```


## Testing PRs

Though it's expected that you run tests locally for your PR, tests will also run on the appveyor server automatically on any PR you send to GitHub.


## Product planning and issue tracking

:grey_exclamation: How we track what work there is to do.


### Issue tracking

Bug management takes place in GitHub. Each repo has its own issue tracker. Bugs cannot be moved between repos so make sure you open a bug in the right repo. To "port" a bug to another repo, consider using a tool such as https://github-issue-mover.appspot.com/.

We use the HuBoard pattern for issue tags. Look at the numerical tags that SignalR uses for an idea: https://github.com/SignalR/SignalR/issues


### Breaking changes

In general, breaking changes can be made only in a new **major** product version, e.g. moving from `1.x.x` to `2.0.0`. Even still, we generally try to avoid breaking changes because they can incur large costs for anyone using these products.

Breaking changes in major versions need to be approved by an engineering manager.

If there is a case where a breaking change needs to be made *not* in a major product update, the change must be approved by at least @Eilon and @DamianEdwards.

For the normal case of breaking changes in major versions, this is the ideal process:

1. Provide some new alternative API (if necessary)
2. Mark the old type/member as `[Obsolete]` to alert users (see below), and to point them at the new alternative API (if applicable)
 * If the old API really doesn't/can't work at all, please discuss with engineering team
3. Update the XML doc comments to indicate the type/member is obsolete, plus what the alternative is. This is typically exactly the same as the obsolete attribute message.
4. File a bug in the next major milestone (e.g. 2.0.0) to remove the type/member
 * Mark this bug with a red `[breaking-change]` label (use exact casing, hyphenation, etc.). Create the label in the repo if it's not there.

Example of obsoleted API:

```c#
    /// <summary>
    /// <para>
    ///     This method/property/type is obsolete and will be removed in a future version.
    ///     The recommended alternative is Microsoft.SomethingCore.SomeType.SomeNewMethod.
    /// </para>
    /// <para>
    ///     ... old docs...
    /// </para>
    /// </summary>
    [Obsolete("This method/property/type is obsolete and will be removed in a future version. The recommended alternative is Microsoft.SomethingCore.SomeType.SomeNewMethod.")]
    public void SomeOldMethod(...)
    {
        ...
    }
```

## Tips and tricks

:grey_exclamation: The *structure* of the code that we write and the *tools* that we use to write the code.


### I've broken my build and I can't get up!

The build system is brand new, so problems can catch us by surprise. As such, you'll sometimes end up in a broken state and can't build. The following steps should fix most broken builds:

```
git clean -xdf (clean all non-source controlled files)
build (this will run the build and will pull in NuGet packages, etc.)
```


### GitHub Flavored Markdown

GitHub supports Markdown in many places throughout the system (issues, comments, etc.). However, there are a few differences from regular Markdown that are described here:

	https://help.github.com/articles/github-flavored-markdown


### Including people in a GitHub discussion

To include another team member in a discussion on GitHub you can use an `@ mention` to cause a notification to be sent to that person. This will automatically send a notification email to that person (assuming they have not altered their GitHub account settings). For example, in a PR's discussion thread or in an issue tracker comment you can type `@username` to have them receive a notification. This is useful when you want to "include" someone in a code review in a PR, or if you want to get another opinion on an issue in the issue tracker.

## Keep an eye on the CI
When you merge a commit into a master or release branch you should keep an eye on [Update Universe](http://aspnetci/viewType.html?buildTypeId=Coherence_UpdateUniverse) until your commit has passed it. Update Universe takes about 30-45 minutes to run when it passes, all you really need to do is ensure that it does. If Update Universe DOESN'T pass, create a thread in the ASPNet-CI Teams channel (regardless of if it was your commits fault) and make sure that I see it.

